---
title: 'Amostra: Criar um alerta do SQL Server Agent com o provedor WMI | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SQL Server Agent [WMI]
- WMI Provider for Server Events, samples
- sample applications [WMI]
ms.assetid: d44811c7-cd46-4017-b284-c863ca088e8f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 875751bd4b2dffd0039ffb40aa884bb9731a75d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139488"
---
# <a name="sample-creating-a-sql-server-agent-alert-with-the-wmi-provider"></a>Amostra: Criar um alerta do SQL Server Agent com o Provedor WMI
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Uma forma comum de usar o Provedor de eventos de WMI é criar alertas do SQL Server Agent que respondem a eventos específicos. O seguinte exemplo apresenta um alerta simples que salva eventos de gráfico de deadlock XML em uma tabela para análise posterior. O SQL Server Agent envia uma solicitação WQL, recebe eventos WMI, e executa um trabalho em resposta ao evento. Observe que, embora vários objetos do Service Broker estejam envolvidos no processamento da mensagem de notificação, o Provedor de eventos de WMI manipula os detalhes da criação e do gerenciamento desses objetos.  
  
## <a name="example"></a>Exemplo  
 Primeiro, uma tabela é criada no banco de dados `AdventureWorks` para conter o evento de gráfico de deadlock. A tabela contém duas colunas: O `AlertTime` coluna contém a hora em que o alerta é executado, e o `DeadlockGraph` coluna contém o documento XML que contém o gráfico de deadlock.  
  
 Então, o alerta é criado. Primeiro, o script cria o trabalho que o alerta irá executar, depois adiciona uma etapa de trabalho ao trabalho e direciona o trabalho para a instância atual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Então, o script cria o alerta.  
  
 A etapa de trabalho recupera o **TextData** propriedade da instância de evento do WMI e insere esse valor na **DeadlockGraph** coluna do **DeadlockEvents** tabela. Observe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte implicitamente a cadeia de caracteres para o formato XML. Como a etapa de trabalho usa o subsistema [!INCLUDE[tsql](../../includes/tsql-md.md)], ela não especifica um proxy.  
  
 O alerta executa o trabalho sempre que um evento de rastreamento do grafo deadlock é registrado. Para um alerta de WMI, o SQL Server Agent cria uma consulta de notificação que usa o namespace e a instrução WQL especificados. Para esse alerta, o SQL Server Agent monitora a instância padrão no computador local. A instrução WQL solicita quaisquer eventos `DEADLOCK_GRAPH` na instância padrão. Para alterar a instância que o alerta monitora, substitua o nome de instância para `MSSQLSERVER` no `@wmi_namespace` para o alerta.  
  
> [!NOTE]  
>  Para o SQL Server Agent receber eventos de WMI [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve ser habilitada no **msdb** e [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks ;  
GO  
  
IF OBJECT_ID('DeadlockEvents', 'U') IS NOT NULL  
BEGIN  
    DROP TABLE DeadlockEvents ;  
END ;  
GO  
  
CREATE TABLE DeadlockEvents  
    (AlertTime DATETIME, DeadlockGraph XML) ;  
GO  
-- Add a job for the alert to run.  
  
EXEC  msdb.dbo.sp_add_job @job_name=N'Capture Deadlock Graph',   
    @enabled=1,   
    @description=N'Job for responding to DEADLOCK_GRAPH events' ;  
GO  
  
-- Add a jobstep that inserts the current time and the deadlock graph into  
-- the DeadlockEvents table.  
  
EXEC msdb.dbo.sp_add_jobstep  
    @job_name = N'Capture Deadlock Graph',  
    @step_name=N'Insert graph into LogEvents',  
    @step_id=1,   
    @on_success_action=1,   
    @on_fail_action=2,   
    @subsystem=N'TSQL',   
    @command= N'INSERT INTO DeadlockEvents  
                (AlertTime, DeadlockGraph)  
                VALUES (getdate(), N''$(ESCAPE_SQUOTE(WMI(TextData)))'')',  
    @database_name=N'AdventureWorks' ;  
GO  
  
-- Set the job server for the job to the current instance of SQL Server.  
  
EXEC msdb.dbo.sp_add_jobserver @job_name = N'Capture Deadlock Graph' ;  
GO  
  
-- Add an alert that responds to all DEADLOCK_GRAPH events for  
-- the default instance. To monitor deadlocks for a different instance,  
-- change MSSQLSERVER to the name of the instance.  
  
EXEC msdb.dbo.sp_add_alert @name=N'Respond to DEADLOCK_GRAPH',   
@wmi_namespace=N'\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER',   
    @wmi_query=N'SELECT * FROM DEADLOCK_GRAPH',   
    @job_name='Capture Deadlock Graph' ;  
GO  
```  
  
## <a name="testing-the-sample"></a>Testando o exemplo  
 Para ver a execução do trabalho, provoque um deadlock. Na [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra duas **consulta SQL** guias e conecte ambas consultas à mesma instância. Execute o seguinte script em um das guias de consulta. Este script produz um conjunto de resultados e é encerrado.  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 Execute o seguinte script na segunda guia consulta. Este script produz um conjunto de resultados e, em seguida, bloqueie, esperando para adquirir um bloqueio em `Production.Product`.  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 Execute o seguinte script na primeira guia de consulta. Este script fica bloqueado, aguardando para adquirir um bloqueio em `Production.Location`. Depois de um tempo limite curto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escolherá este script ou o script no exemplo como a vítima de deadlock e encerrará a transação.  
  
```  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
```  
  
 Depois de provocar o deadlock, aguarde algum tempo para o SQL Server Agent ativar o alerta e executar o trabalho. Examine o conteúdo da tabela `DeadlockEvents` executando o seguinte script:  
  
```  
SELECT * FROM DeadlockEvents ;  
GO  
```  
  
 A coluna `DeadlockGraph` deve conter um documento XML que mostra todas as propriedades do evento do gráfico de deadlock.  
  
## <a name="see-also"></a>Consulte também  
 [Provedor WMI para conceitos de eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
