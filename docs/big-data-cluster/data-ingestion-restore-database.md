---
title: Restaurar um banco de dados
titleSuffix: SQL Server big data clusters
description: Este artigo mostra como restaurar um banco de dados para a instância mestre de um cluster de big data do SQL Server 2019 (visualização).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1ad5ca749f3862f0d7df3411efd78104052dba91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958620"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>Restaurar um banco de dados para a instância de mestre de cluster de big data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como restaurar um banco de dados existente para a instância mestre de um cluster de big data do SQL Server 2019 (visualização). O método recomendado é usar uma cópia de backup, e restaurar a abordagem.

## <a name="backup-your-existing-database"></a>Fazer backup de seu banco de dados existente

Primeiro, fazer backup de seu banco de dados do SQL Server existente do SQL Server no Windows ou Linux. Use técnicas padrão de backup com o Transact-SQL ou com uma ferramenta como o SQL Server Management Studio (SSMS).

Este artigo mostra como restaurar o banco de dados AdventureWorks, mas você pode usar qualquer backup de banco de dados. 

> [!TIP]
> Você pode baixar o backup do AdventureWorks [aqui](https://www.microsoft.com/download/details.aspx?id=49502).

## <a name="copy-the-backup-file"></a>Copie o arquivo de backup

Copie o arquivo de backup para o contêiner do SQL Server no pod instância mestre do cluster Kubernetes.

```bash
kubectl cp <path to .bak file> mssql-master-pool-0:/tmp -c mssql-server -n <name of your big data cluster>
```

Exemplo:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-master-pool-0:/tmp -c mssql-server -n clustertest
```

Em seguida, verifique se o arquivo de backup foram copiado para o contêiner de pod.

```bash
kubectl exec -it mssql-master-pool-0 -n <name of your big data cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

Exemplo:

```bash
kubectl exec -it mssql-master-pool-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>Restaurar o arquivo de backup

Em seguida, restaure o backup de banco de dados para a instância mestre do SQL Server.  Se você estiver restaurando um backup de banco de dados que foi criado no Windows, você precisará obter os nomes dos arquivos.  No estúdio de dados do Azure, conectar-se à instância do mestre e execute este script SQL:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

Exemplo:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![Lista de arquivos de backup](media/restore-database/database-restore-file-list.png)

Agora, restaure o banco de dados. O script a seguir é um exemplo. Substitua os nomes ou caminhos, conforme necessário, dependendo de seu backup de banco de dados.

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>Configurar o pool de dados e acesso do HDFS

Agora, para a instância mestre do SQL Server para pools de dados do access e o HDFS, execute os procedimentos de pool armazenado de pool e o armazenamento de dados. Execute os seguintes scripts de Transact-SQL no banco de dados recém-restaurado:

```sql
USE AdventureWorks2016CTP3
GO
-- Create the SqlDataPool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
  CREATE EXTERNAL DATA SOURCE SqlDataPool
  WITH (LOCATION = 'sqldatapool://controller-svc/default');

-- Create the SqlStoragePool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   CREATE EXTERNAL DATA SOURCE SqlStoragePool
   WITH (LOCATION = 'sqlhdfs://controller-svc/default');
GO
```

> [!NOTE]
> Você precisará executar esses scripts de instalação somente para bancos de dados restaurados a partir de versões anteriores do SQL Server. Se você criar um novo banco de dados na instância mestre do SQL Server, os procedimentos de armazenamento de pool de armazenamento e o pool de dados já estão configurados para você.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte a visão geral a seguir:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
