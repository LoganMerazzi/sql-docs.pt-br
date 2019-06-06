---
title: Criar e executar trabalhos do SQL Server no Linux | Microsoft Docs
description: Este tutorial mostra como executar o trabalho do SQL Server Agent no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.openlocfilehash: d7df0ed46d9ded592a8cebc6571c5ec1e1b1f486
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705121"
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Criar e executar trabalhos do SQL Server Agent no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Trabalhos do SQL Server são usados para executar regularmente a mesma sequência de comandos no banco de dados do SQL Server. Este tutorial fornece um exemplo de como criar um trabalho do SQL Server Agent no Linux usando o Transact-SQL e SQL Server Management Studio (SSMS).

> [!div class="checklist"]
> * Instalar o SQL Server Agent no Linux
> * Criar um novo trabalho para executar backups de banco de dados diários
> * Agendar e executar o trabalho
> * Execute as mesmas etapas no SSMS (opcional)

Para problemas conhecidos com o SQL Server Agent no Linux, consulte o [notas de versão](sql-server-linux-release-notes.md).

## <a name="prerequisites"></a>Prerequisites

Os seguintes pré-requisitos são necessários para concluir este tutorial:

* Computador Linux com os seguintes pré-requisitos:
  * SQL Server ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), ou [Ubuntu](quickstart-install-connect-ubuntu.md)) com as ferramentas de linha de comando.

Os seguintes pré-requisitos são opcionais:

* Computador Windows com o SSMS:
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para etapas opcionais do SSMS.

## <a name="enable-sql-server-agent"></a>Habilitar o SQL Server Agent

Para usar o SQL Server Agent no Linux, você deve primeiro habilitar o SQL Server Agent em um computador que já tenha o SQL Server instalado.

1. Para habilitar o SQL Server Agent, siga a etapa abaixo.
  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  ```

1. Reinicie o SQL Server com o seguinte comando:
  ```bash
  sudo systemctl restart mssql-server
  ```

> [!NOTE]
> Começando com o SQL Server 2017 CU4, SQL Server Agent está incluído com o **mssql-server** empacotar e é desabilitada por padrão. Para o agente configurado antes da visita de CU4 [instalar o SQL Server Agent no Linux](sql-server-linux-setup-sql-agent.md).

## <a name="create-a-sample-database"></a>Criar banco de dados de exemplo

Use as seguintes etapas para criar um banco de dados de exemplo denominado **SampleDB**. Este banco de dados é usado para o trabalho de backup diário.

1. Em seu computador Linux, abra uma sessão de terminal bash.

1. Use **sqlcmd** para executar um Transact-SQL **criar banco de dados** comando.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. Verifique se que o banco de dados é criado, listando os bancos de dados em seu servidor.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>Criar um trabalho com o Transact-SQL

As seguintes etapas criam um trabalho do SQL Server Agent no Linux com comandos Transact-SQL. O trabalho é executado um backup diário do banco de dados de exemplo, **SampleDB**.

> [!TIP]
> Você pode usar qualquer cliente de T-SQL para executar esses comandos. Por exemplo, no Linux você pode usar [sqlcmd](sql-server-linux-setup-tools.md) ou [Visual Studio Code](sql-server-linux-develop-use-vscode.md). De um servidor remoto do Windows, você também pode executar consultas no SQL Server Management Studio (SSMS) ou usar a interface do usuário para o gerenciamento de trabalho, que é descrito na próxima seção.

1. Use [sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md) para criar um trabalho denominado `Daily SampleDB Backup`.

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. Chame [sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md) para criar uma etapa de trabalho que cria um backup do `SampleDB` banco de dados.

   ```sql
   -- Adds a step (operation) to the job
   EXEC sp_add_jobstep
      @job_name = N'Daily SampleDB Backup',
      @step_name = N'Backup database',
      @subsystem = N'TSQL',
      @command = N'BACKUP DATABASE SampleDB TO DISK = \
         N''/var/opt/mssql/data/SampleDB.bak'' WITH NOFORMAT, NOINIT, \
         NAME = ''SampleDB-full'', SKIP, NOREWIND, NOUNLOAD, STATS = 10',
      @retry_attempts = 5,
      @retry_interval = 5 ;
   GO
   ```

1. Em seguida, crie uma agenda diária para o trabalho com [sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md).

   ```sql
   -- Creates a schedule called 'Daily'
   EXEC dbo.sp_add_schedule
      @schedule_name = N'Daily SampleDB',
      @freq_type = 4,
      @freq_interval = 1,
      @active_start_time = 233000 ;
   USE msdb ;
   GO
   ```

1. Anexar a agenda de trabalho ao trabalho com [sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md).

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. Use [sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md) para atribuir o trabalho a um servidor de destino. Neste exemplo, o destino é o servidor local.

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. Iniciar o trabalho com [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>Criar um trabalho com o SSMS

Você também pode criar e gerenciar trabalhos remotamente usando o SQL Server Management Studio (SSMS) no Windows.

1. Inicie o SSMS no Windows e conecte-se à instância do SQL Server do Linux. Para obter mais informações, consulte [gerenciar o SQL Server no Linux com o SSMS](sql-server-linux-manage-ssms.md).

1. Verifique se que você tenha criado um banco de dados de exemplo denominado **SampleDB**.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. Verifique se o SQL Agent foi [instalado](sql-server-linux-setup-sql-agent.md) e configurado corretamente. Procure no sinal de adição ao lado do SQL Server Agent no Pesquisador de objetos. Se o SQL Server Agent não estiver habilitado, tente reiniciar o **mssql-server** serviço no Linux.

   ![Verifique se o que SQL Server Agent foi instalado](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. Crie um novo trabalho.

   ![Criar um novo trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. Dê um nome ao seu trabalho e crie sua etapa de trabalho.

   ![Criar uma etapa de trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. Especifique quais subsistema que você deseja usar e o que fazer a etapa de trabalho.

   ![Subsistema de trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![Ação da etapa de trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. Crie uma nova agenda de trabalho.

   ![Agenda do trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![Agenda do trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. Inicie seu trabalho.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Instalar o SQL Server Agent no Linux
> * Use o Transact-SQL e sistema de procedimentos armazenados para criar trabalhos
> * Criar um trabalho que realiza os backups de banco de dados diária
> * Use o SSMS UI para criar e gerenciar trabalhos

Em seguida, explore outros recursos para criar e gerenciar trabalhos:

> [!div class="nextstepaction"]
>[Documentação do SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
