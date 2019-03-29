---
title: Restaurar um banco de dados do SQL Server no Docker | Microsoft Docs
description: Este tutorial mostra como restaura um backup de banco de dados do SQL Server em um novo contêiner do Docker do Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 31cf9104ea47bdf8086e8676312d9ac8d8085184
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2019
ms.locfileid: "58566545"
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Restaurar um banco de dados do SQL Server em um contêiner do Docker do Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Este tutorial demonstra como mover e restaurar um arquivo de backup do SQL Server em uma imagem de contêiner do SQL Server 2017 Linux em execução no Docker.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Este tutorial demonstra como mover e restaurar um arquivo de backup do SQL Server em uma imagem de contêiner do SQL Server versão prévia de 2019 Linux em execução no Docker.

::: moniker-end

> [!div class="checklist"]
> * Efetuar pull e executar a imagem de contêiner do SQL Server Linux mais recente.
> * Copie o arquivo de banco de dados da Wide World Importers no contêiner.
> * Restaure o banco de dados no contêiner.
> * Execute instruções Transact-SQL para exibir e modificar o banco de dados.
> * Fazer backup de banco de dados modificado.

## <a name="prerequisites"></a>Prerequisites

* O Docker Engine 1.8 ou superior em qualquer distribuição do Linux ou do Docker para Mac/Windows com suporte. Para obter mais informações, veja [Install Docker](https://docs.docker.com/engine/installation/) (Instalar o Docker).
* Mínimo de 2 GB de espaço em disco
* Mínimo de 2 GB de RAM
* [Requisitos do sistema do SQL Server no Linux](sql-server-linux-setup.md#system).

## <a name="pull-and-run-the-container-image"></a>Efetuar pull e executar a imagem de contêiner

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Abra um terminal bash no Linux/Mac ou uma sessão do PowerShell com privilégios elevados no Windows.

1. Efetue pull da imagem de contêiner do SQL Server 2017 do Linux por meio do Hub do Docker.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > Ao longo deste tutorial, os exemplos de comando do docker são fornecidos para o shell bash (Linux/Mac) e o PowerShell (Windows).

1. Para executar a imagem de contêiner com Docker, você pode usar o comando a seguir:

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   Este comando cria um contêiner do SQL Server 2017 com a edição de desenvolvedor (padrão). Porta do SQL Server **1433** é exposta no host de porta **1401**. Opcional `-v sql1data:/var/opt/mssql` parâmetro cria um contêiner de volume de dados denominado **sql1ddata**. Isso é usado para manter os dados criados pelo SQL Server.

   > [!NOTE]
   > O processo para executar edições do SQL Server de produção em contêineres é ligeiramente diferente. Para obter mais informações, veja [Executar imagens de contêiner de produção](sql-server-linux-configure-docker.md#production). Se você usar o mesmo nomes de contêiner e portas, o restante deste passo a passo ainda funciona com contêineres de produção.

1. Para exibir seus contêineres do Docker, use o comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e será escutado na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

  ```bash
  $ sudo docker ps -a

  CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
  941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
  ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Abra um terminal bash no Linux/Mac ou uma sessão do PowerShell com privilégios elevados no Windows.

1. Extrair a visualização do SQL Server 2019 imagem de contêiner do Linux de Hub do Docker.

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   > [!TIP]
   > Ao longo deste tutorial, os exemplos de comando do docker são fornecidos para o shell bash (Linux/Mac) e o PowerShell (Windows).

1. Para executar a imagem de contêiner com Docker, você pode usar o comando a seguir:

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   Este comando cria um contêiner de visualização de 2019 do SQL Server com a edição de desenvolvedor (padrão). Porta do SQL Server **1433** é exposta no host de porta **1401**. Opcional `-v sql1data:/var/opt/mssql` parâmetro cria um contêiner de volume de dados denominado **sql1ddata**. Isso é usado para manter os dados criados pelo SQL Server.

1. Para exibir seus contêineres do Docker, use o comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. Se a coluna **STATUS** mostrar o status **Up**, o SQL Server estará em execução no contêiner e será escutado na porta especificada na coluna **PORTS**. Se a coluna **STATUS** do contêiner do SQL Server mostrar **Exited**, confira a [seção Solução de problemas do guia de configuração](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

::: moniker-end

## <a name="change-the-sa-password"></a>Alterar a senha SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>Copiar um arquivo de backup no contêiner

Este tutorial usa o [banco de dados de exemplo Wide World Importers](../sample/world-wide-importers/wide-world-importers-documentation.md). Use as etapas a seguir para baixar e copiar o arquivo de backup do banco de dados Wide World Importers para seu contêiner do SQL Server.

1. Primeiro, use **o docker exec** para criar uma pasta de backup. O comando a seguir cria uma **/var/opt/mssql/backup** diretório dentro do contêiner do SQL Server.

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. Em seguida, baixe o [WideWorldImporters-Full](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) arquivo para o computador host. Os seguintes comandos, navegue até o diretório de usuário/home e baixa o arquivo de backup como **wwi.bak**.

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. Use **docker cp** para copiar o arquivo de backup no contêiner na **/var/opt/mssql/backup** directory.

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>Restaurar o banco de dados

Agora, o arquivo de backup está localizado dentro do contêiner. Antes de restaurar o backup, é importante conhecer os nomes de arquivo lógico e os tipos de arquivos dentro do backup. Os seguintes comandos Transact-SQL inspecionar o backup e realizar a restauração usando **sqlcmd** no contêiner.

> [!TIP]
> Este tutorial usa **sqlcmd** dentro do contêiner, como o contêiner é fornecido com essa ferramenta pré-instalada. No entanto, você também pode executar instruções Transact-SQL com outro cliente ferramentas fora do contêiner, como [Visual Studio Code](sql-server-linux-develop-use-vscode.md) ou [SQL Server Management Studio](sql-server-linux-manage-ssms.md). Para se conectar, use a porta de host foi mapeada para a porta 1433 no contêiner. Neste exemplo, que é **localhost, 1401** no computador host e **Host_IP_Address, 1401** remotamente.

1. Execute **sqlcmd** dentro do contêiner para listar os nomes de arquivo lógico e caminhos dentro do backup. Isso é feito com o **RESTORE FILELISTONLY** instrução Transact-SQL.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost \
      -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE FILELISTONLY FROM DISK = "/var/opt/mssql/backup/wwi.bak"' \
      | tr -s ' ' | cut -d ' ' -f 1-2
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost `
      -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/wwi.bak'"
   ```

   Você deve ver saídas semelhantes ao seguinte:

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. Chame o **RESTAURAR banco de dados** comando para restaurar o banco de dados dentro do contêiner. Especifica um caminho novo para cada um dos arquivos na etapa anterior.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE DATABASE WideWorldImporters FROM DISK = "/var/opt/mssql/backup/wwi.bak" WITH MOVE "WWI_Primary" TO "/var/opt/mssql/data/WideWorldImporters.mdf", MOVE "WWI_UserData" TO "/var/opt/mssql/data/WideWorldImporters_userdata.ndf", MOVE "WWI_Log" TO "/var/opt/mssql/data/WideWorldImporters.ldf", MOVE "WWI_InMemory_Data_1" TO "/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE DATABASE WideWorldImporters FROM DISK = '/var/opt/mssql/backup/wwi.bak' WITH MOVE 'WWI_Primary' TO '/var/opt/mssql/data/WideWorldImporters.mdf', MOVE 'WWI_UserData' TO '/var/opt/mssql/data/WideWorldImporters_userdata.ndf', MOVE 'WWI_Log' TO '/var/opt/mssql/data/WideWorldImporters.ldf', MOVE 'WWI_InMemory_Data_1' TO '/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1'"
   ```

   Você deve ver saídas semelhantes ao seguinte:

   ```
   Processed 1464 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   Processed 33 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   Processed 3862 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Converting database 'WideWorldImporters' from version 852 to the current version 869.
   Database 'WideWorldImporters' running the upgrade step from version 852 to version 853.
   Database 'WideWorldImporters' running the upgrade step from version 853 to version 854.
   Database 'WideWorldImporters' running the upgrade step from version 854 to version 855.
   Database 'WideWorldImporters' running the upgrade step from version 855 to version 856.
   Database 'WideWorldImporters' running the upgrade step from version 856 to version 857.
   Database 'WideWorldImporters' running the upgrade step from version 857 to version 858.
   Database 'WideWorldImporters' running the upgrade step from version 858 to version 859.
   Database 'WideWorldImporters' running the upgrade step from version 859 to version 860.
   Database 'WideWorldImporters' running the upgrade step from version 860 to version 861.
   Database 'WideWorldImporters' running the upgrade step from version 861 to version 862.
   Database 'WideWorldImporters' running the upgrade step from version 862 to version 863.
   Database 'WideWorldImporters' running the upgrade step from version 863 to version 864.
   Database 'WideWorldImporters' running the upgrade step from version 864 to version 865.
   Database 'WideWorldImporters' running the upgrade step from version 865 to version 866.
   Database 'WideWorldImporters' running the upgrade step from version 866 to version 867.
   Database 'WideWorldImporters' running the upgrade step from version 867 to version 868.
   Database 'WideWorldImporters' running the upgrade step from version 868 to version 869.
   RESTORE DATABASE successfully processed 58455 pages in 18.069 seconds (25.273 MB/sec).
   ```

## <a name="verify-the-restored-database"></a>Verifique se o banco de dados restaurado

Execute a consulta a seguir para exibir uma lista de nomes de banco de dados em seu contêiner:

```bash
sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
   -Q 'SELECT Name FROM sys.Databases'
```

```PowerShell
docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
   -Q "SELECT Name FROM sys.Databases"
```

Você deve ver **WideWorldImporters** na lista de bancos de dados.

## <a name="make-a-change"></a>Faça uma alteração

As etapas a seguir faz uma alteração no banco de dados.

1. Executar uma consulta para exibir os 10 principais itens a **Warehouse.StockItems** tabela.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID"
   ```

   Você deve ver uma lista de nomes e identificadores de item:

   ```
   StockItemID StockItemName
   ----------- -----------------
             1 USB missile launcher (Green)
             2 USB rocket launcher (Gray)
             3 Office cube periscope (Black)
             4 USB food flash drive - sushi roll
             5 USB food flash drive - hamburger
             6 USB food flash drive - hot dog
             7 USB food flash drive - pizza slice
             8 USB food flash drive - dim sum 10 drive variety pack
             9 USB food flash drive - banana
            10 USB food flash drive - chocolate bar
   ```

1. Atualizar a descrição do primeiro item com o seguinte **atualização** instrução:

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName="USB missile launcher (Dark Green)" WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName='USB missile launcher (Dark Green)' WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   Você deve ver saídas semelhantes ao seguinte texto:

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>Crie um novo backup

Depois de ter restaurado o banco de dados em um contêiner, você também poderá criar regularmente os backups de banco de dados dentro do contêiner em execução. As etapas seguem um padrão semelhante para as etapas anteriores, mas na ordem inversa.

1. Use o **BACKUP do banco de dados** comando Transact-SQL para criar um backup de banco de dados no contêiner. Este tutorial cria um novo arquivo de backup **wwi_2.bak**, em criado anteriormente **/var/opt/mssql/backup** directory.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   Você deve ver saídas semelhantes ao seguinte:

   ```
   10 percent processed.
   20 percent processed.
   30 percent processed.
   40 percent processed.
   50 percent processed.
   60 percent processed.
   70 percent processed.
   Processed 1200 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   80 percent processed.
   Processed 3865 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Processed 938 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   100 percent processed.
   BACKUP DATABASE successfully processed 59099 pages in 25.056 seconds (18.427 MB/sec).
   ```

1. Em seguida, copie o arquivo de backup para fora do contêiner e a máquina host.

   ```bash
   cd ~
   sudo docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

   ```PowerShell
   cd ~
   docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

## <a name="use-the-persisted-data"></a>Use os dados persistentes

Além de fazer backups de banco de dados para proteger seus dados, você também pode usar contêineres de volume de dados. O início deste tutorial criada o **sql1** contêiner com o `-v sql1data:/var/opt/mssql` parâmetro. O **sql1data** persiste do contêiner de volume de dados de **/var/opt/mssql** dados mesmo depois que o contêiner é removido. As etapas a seguir removem completamente o **sql1** contêiner e, em seguida, crie um novo contêiner **sql2**, com os dados persistentes.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Parar o **sql1** contêiner.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. Remova o contêiner. Isso não exclui criado anteriormente **sql1data** contêiner de volume de dados e os dados persistentes nela.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. Criar um novo contêiner **sql2**e reutilizar as **sql1data** contêiner de volume de dados.

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

1. O banco de dados da Wide World Importers está agora no novo contêiner. Execute uma consulta para verificar a alteração anterior feita.

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > A senha de SA não é a senha especificada para o **sql2** contêiner, `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`. Todos os dados do SQL Server foi restaurado a partir **sql1**, incluindo a senha alterada de anteriormente no tutorial. Na verdade, algumas opções como esta são ignoradas devido a restauração dos dados no /var/opt/mssql. Por esse motivo, a senha é `<YourNewStrong!Passw0rd>` conforme mostrado aqui.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Parar o **sql1** contêiner.

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. Remova o contêiner. Isso não exclui criado anteriormente **sql1data** contêiner de volume de dados e os dados persistentes nela.

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. Criar um novo contêiner **sql2**e reutilizar as **sql1data** contêiner de volume de dados.

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
    ```

1. O banco de dados da Wide World Importers está agora no novo contêiner. Execute uma consulta para verificar a alteração anterior feita.

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > A senha de SA não é a senha especificada para o **sql2** contêiner, `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`. Todos os dados do SQL Server foi restaurado a partir **sql1**, incluindo a senha alterada de anteriormente no tutorial. Na verdade, algumas opções como esta são ignoradas devido a restauração dos dados no /var/opt/mssql. Por esse motivo, a senha é `<YourNewStrong!Passw0rd>` conforme mostrado aqui.

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Neste tutorial, você aprendeu a fazer backup de um banco de dados no Windows e movê-lo para um servidor Linux executando o SQL Server 2017. Você aprendeu como para:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Neste tutorial, você aprendeu a fazer backup de um banco de dados no Windows e movê-lo para um servidor Linux executando o SQL Server 2019 preview. Você aprendeu como para:

::: moniker-end

> [!div class="checklist"]
> * Crie imagens de contêiner do Linux do SQL Server.
> * Copie os backups de banco de dados do SQL Server em um contêiner.
> * Executar instruções Transact-SQL dentro do contêiner com **sqlcmd**.
> * Criar e extrair arquivos de backup de um contêiner.
> * Use contêineres de volume de dados no Docker para persistir dados do SQL Server.

Em seguida, examine outras configurações do Docker e cenários de solução de problemas:

> [!div class="nextstepaction"]
>[Guia de configuração para o SQL Server 2017 no Docker](sql-server-linux-configure-docker.md)
