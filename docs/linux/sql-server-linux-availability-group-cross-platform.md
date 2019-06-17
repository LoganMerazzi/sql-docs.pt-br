---
title: Configurar o SQL Server sempre no grupo de disponibilidade no Windows e Linux | Microsoft Docs
description: Configurar o grupo de disponibilidade de servidor de SQL com réplicas em Windows e Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/31/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 520866e80cd3526d7c039cd98e08f5cc8fc52798
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713389"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>Configurar SQL Server sempre no grupo de disponibilidade no Windows e Linux (plataformas)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Este artigo explica as etapas para criar um sempre no grupo de disponibilidade (AG) com uma réplica em um servidor Windows e a outra réplica em um servidor Linux. Essa configuração é multiplataforma, pois as réplicas estão em diferentes sistemas operacionais. Use essa configuração para a migração de uma plataforma para outra ou recuperação de desastres (DR). Essa configuração não dá suporte a alta disponibilidade porque não há nenhuma solução de cluster para gerenciar uma configuração de plataforma cruzada. 

![Híbrido None](./media/sql-server-linux-availability-group-overview/image1.png)

Antes de prosseguir, você deve estar familiarizado com a instalação e configuração para instâncias do SQL Server no Windows e Linux. 

## <a name="scenario"></a>Cenário

Nesse cenário, dois servidores estiverem em diferentes sistemas operacionais. Windows Server 2016 chamado `WinSQLInstance` hospeda a réplica primária. Um servidor Linux chamado `LinuxSQLInstance` hospedar a réplica secundária.

## <a name="configure-the-ag"></a>Configurar o grupo de disponibilidade 

As etapas para criar o grupo de disponibilidade são o mesmo que as etapas para criar um grupo de disponibilidade para cargas de trabalho de escala de leitura. O tipo de cluster do grupo de disponibilidade é NONE, porque não há nenhum Gerenciador de cluster. 

   >[!NOTE]
   >Para os scripts neste artigo, ângulo colchetes `<` e `>` identificar valores que você precisa substituir para o seu ambiente. Os colchetes angulares em si não são necessários para os scripts. 

1. Instalar o SQL Server 2017 no Windows Server 2016, habilitar grupos de disponibilidade AlwaysOn do SQL Server Configuration Manager e configurar a autenticação de modo misto. 

   >[!TIP]
   >Se você está validando essa solução no Azure, coloque ambos os servidores no mesma conjunto de disponibilidade para garantir que eles são separados no data center. 

   **Habilitar grupos de disponibilidade**

   Para obter instruções, consulte [habilitar e desabilitar grupos de disponibilidade AlwaysOn (SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).

   ![Habilitar grupos de disponibilidade](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   SQL Server Configuration Manager observa que o computador não é um nó em um cluster de failover. 

   Depois de habilitar grupos de disponibilidade, reinicie o SQL Server.

   **Conjunto de autenticação de modo misto**

   Para obter instruções, consulte [alterar modo de autenticação de servidor](../database-engine/configure-windows/change-server-authentication-mode.md#SSMSProcedure).

1. Instale o SQL Server 2017 no Linux. Para obter instruções, consulte [instalar o SQL Server](sql-server-linux-setup.md). Habilitar `hadr` via mssql-conf.

   Para habilitar `hadr` via mssql-conf em um prompt de shell, emita o seguinte comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   Depois de habilitar `hadr`, reinicie a instância do SQL Server.  

   A imagem a seguir mostra essa etapa concluída.

   ![Habilitar Linux de grupos de disponibilidade](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. Configurar o arquivo de hosts em ambos os servidores ou registrar os nomes do servidor DNS.

1. Abra as portas de firewall para TPC 1433 e 5022 no Windows e Linux.

1. Na réplica primária, crie um logon de banco de dados e a senha.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. Na réplica primária, crie uma chave mestra e um certificado e, em seguida, faça backup do certificado com uma chave privada.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
   BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
       );
   GO
   ```

1. Copiar o certificado e a chave privada para o servidor do Linux (réplica secundária) no `/var/opt/mssql/data`. Você pode usar `pscp` para copiar os arquivos para o servidor Linux. 

1. Definir o grupo e a propriedade de chave privada e o certificado a ser `mssql:mssql`.

   O script a seguir define o grupo e a propriedade dos arquivos. 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   No diagrama a seguir, propriedade e grupo estão definidas corretamente para o certificado e a chave.

   ![Habilitar Linux de grupos de disponibilidade](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. Na réplica secundária, crie um logon de banco de dados e a senha e crie uma chave mestra.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. Na réplica secundária, restaure o certificado que você copiou para `/var/opt/mssql/data`. 

   ```sql
   CREATE CERTIFICATE dbm_certificate   
       AUTHORIZATION dbm_user
       FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
       WITH PRIVATE KEY (
       FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
       DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
   )
   GO
   ```

1. Na réplica primária, crie um ponto de extremidade.

   ```sql
   CREATE ENDPOINT [Hadr_endpoint]
       AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
       FOR DATA_MIRRORING (
           ROLE = ALL,
           AUTHENTICATION = CERTIFICATE dbm_certificate,
           ENCRYPTION = REQUIRED ALGORITHM AES
           );
   ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
   GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]
   GO
   ```

   >[!IMPORTANT]
   >O firewall deve estar aberto para o porta TCP do ouvinte. No script anterior, a porta é 5022. Use qualquer porta TCP disponível. 

1. Na réplica secundária, crie o ponto de extremidade. Repita o script anterior na réplica secundária para criar o ponto de extremidade. 

1. Na réplica primária, crie o grupo de disponibilidade com `CLUSTER_TYPE = NONE`. O script de exemplo usa `SEEDING_MODE = AUTOMATIC` para criar o grupo de disponibilidade. 

   >[!NOTE]
   >Quando a instância do Windows do SQL Server usa diferentes caminhos para arquivos de log e de dados, a propagação falhar para a instância do SQL Server do Linux, porque esses caminhos não existem na réplica secundária automática. Para usar o script a seguir para um grupo de disponibilidade de plataforma cruzada, o banco de dados requer o mesmo caminho para os arquivos de log e de dados no servidor do Windows. Como alternativa, você pode atualizar o script para definir `SEEDING_MODE = MANUAL` e, em seguida, fazer backup e restaurar o banco de dados com `NORECOVERY` para propagar o banco de dados. 
   >
   >Esse comportamento se aplica a imagens do Azure Marketplace. 
   >
   >Para obter mais informações sobre a propagação automática, consulte [propagação automática - Layout de disco](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout). 

   Antes de executar o script, atualize os valores de seus grupos de disponibilidade.

      * Substitua `<WinSQLInstance>` com o nome do servidor da instância do SQL Server de réplica primária.

      * Substitua `<LinuxSQLInstance>` com o nome do servidor da instância do SQL Server de réplica secundária. 

   Para criar o grupo de disponibilidade, atualize os valores e executar o script na réplica primária.  

   ```sql
   CREATE AVAILABILITY GROUP [ag1]
       WITH (CLUSTER_TYPE = NONE)
       FOR REPLICA ON
           N'<WinSQLInstance>' 
        WITH (
           ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            SEEDING_MODE = AUTOMATIC,
            FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
           N'<LinuxSQLInstance>' 
       WITH (
            ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
           SEEDING_MODE = AUTOMATIC,
           FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
           )
   GO
   ```
   
   Para obter mais informações, consulte [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md).

1. Na réplica secundária, una o grupo de disponibilidade.

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. Crie um banco de dados para o grupo de disponibilidade. As etapas de exemplo usam um banco de dados denominado `<TestDB>`. Se você estiver usando a propagação automática, defina o mesmo caminho para os dados e os arquivos de log. 

   Antes de executar o script, atualize os valores do banco de dados.

      * Substitua `<TestDB>` com o nome do banco de dados.

      * Substitua `<F:\Path>` com o caminho para seu banco de dados e arquivos de log. Use o mesmo caminho para os banco de dados e arquivos de log. 

      Você também pode usar os caminhos padrão. 

    Para criar seu banco de dados, execute o script. 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. Faça um backup completo do banco de dados. 

1. Se você não estiver usando a propagação automática, restaure o banco de dados no servidor de réplica secundária (Linux). [Migrar um banco de dados do SQL Server do Windows para Linux usando o backup e restauração](sql-server-linux-migrate-restore-database.md). Restaurar o banco de dados `WITH NORECOVERY` na réplica secundária. 

1. Adicione o banco de dados para o grupo de disponibilidade. Atualize o script de exemplo. Substitua `<TestDB>` com o nome do banco de dados. Na réplica primária, execute a consulta SQL para adicionar o banco de dados para o grupo de disponibilidade.

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. Verifique se que o banco de dados está sendo preenchido na réplica secundária. 

## <a name="fail-over-the-primary-replica"></a>Fazer failover da réplica primária

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

Este artigo revisado as etapas para criar um grupo de disponibilidade de plataforma cruzada para dar suporte a cargas de trabalho de migração ou escala de leitura. Ele pode ser usado para recuperação de desastres manual. Ele também explicou como fazer failover do AG. Um grupo de disponibilidade de plataforma cruzada usa o tipo de cluster `NONE` e não oferece suporte a alta disponibilidade porque não há nenhum cluster ferramenta entre plataformas-. 

## <a name="next-steps"></a>Próximas etapas

[Visão geral dos grupos de disponibilidade AlwaysOn](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[Noções básicas de disponibilidade do SQL Server para implantações do Linux](sql-server-linux-ha-basics.md)
