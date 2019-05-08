---
title: Conectar o Spark para o SQL Server
titleSuffix: SQL Server big data clusters
description: Saiba como usar o conector do Spark MSSQL no Spark para leitura e gravação para o SQL Server.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 54361f9a061169d51f11ccb130e78ba67c0a9a67
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759213"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>Como ler e gravar para o SQL Server no Spark usando o conector do Spark MSSQL

Um padrão de uso de chave de dados grandes é alto volume de processamento de dados no Spark, seguido de gravar os dados no SQL Server para acesso a aplicativos de linha de negócios. Esses padrões de uso se beneficiar de um conector que utiliza otimizações importantes de SQL e fornece um mecanismo de gravação eficiente.

Com Clusters de dados grande CTP2.5 fornece um novo conector de MSSQL Spark que usa o SQL Server em massa gravar APIs para um Spark com bom desempenho para gravação SQL. Este artigo fornece um exemplo de como ler e gravar para o SQL Server do Spark usando o conector do Spark MSSQL. Neste exemplo, os dados são lidos do HDFS em um cluster de big data, processados pelo Spark e, em seguida, são gravados para a instância mestre do SQL Server no cluster usando o novo conector do Spark MSSQL.

## <a name="mssql-spark-connector-interface"></a>Interface de conector do Spark MSSQL

Conector do Spark MSSQL é baseado na fonte de dados do Spark APIs e fornece uma interface familiar do conector Spark JDBC. Para parâmetros de interface, consulte [documentação do Apache Spark](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html). O conector do Spark MSSQL é referenciado pelo nome da **com.microsoft.sqlserver.jdbc.spark**.

A tabela a seguir descreve os parâmetros de interface que foram alterados ou novos:

| Nome da propriedade | Opcional | Descrição |
|---|---|---|
| **isolationLevel** | Sim | Descreve o nível de isolamento da conexão. É o padrão para o conector MSSQLSpark **READ_COMMITTED** |

O conector usa em massa do SQL Server gravar APIs. Qualquer gravação em massa parâmetros podem ser passados como parâmetros opcionais pelo usuário e são passados como-está pelo conector para a API subjacente. Para obter mais informações sobre em massa operações de gravação, consulte [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions).

## <a name="prerequisites"></a>Prerequisites

- Um [cluster de big data do SQL Server](deploy-get-started.md).

- [Azure Data Studio](../azure-data-studio/download.md).

## <a name="create-the-target-database"></a>Criar o banco de dados de destino

1. Abra o Studio de dados do Azure, e [conectar-se à instância mestre do SQL Server do seu cluster de big data](connect-to-big-data-cluster.md).

1. Criar uma nova consulta e execute o seguinte comando para criar um banco de dados de exemplo denominado **MinhaBaseDadosTeste**.

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>Carregar dados de exemplo no HDFS

1. Baixe [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) em seu computador local.

1. No estúdio de dados do Azure, clique com botão direito na pasta do HDFS do seu cluster de big data e selecione **novo diretório**. Nomeie o diretório **spark_data**.

1. Clique com botão direito do **spark_data** diretório e selecione **carregar arquivos**. Carregar o **AdultCensusIncome.csv** arquivo.

   ![Arquivo CSV AdultCensusIncome](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>Executar o notebook de exemplo

Para demonstrar o uso do conector do Spark MSSQL com esses dados, baixar um exemplo de notebook, abri-lo no estúdio de dados do Azure e executar cada bloco de código. Para obter mais informações sobre como trabalhar com blocos de anotações, consulte [como usar blocos de anotações na visualização do SQL Server 2019](notebooks-guidance.md).

1. Em uma linha de comando do PowerShell ou bash, execute o comando a seguir para baixar o **mssql_spark_connector.ipynb** notebook de exemplo:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/spark_to_sql/mssql_spark_connector.ipynb"
   ```

1. No estúdio de dados do Azure, abra o arquivo do bloco de anotações de exemplo. Verifique se que ele está conectado ao seu Gateway HDFS/Spark para seu cluster de big data.

1. Execute cada célula de código no exemplo para ver o uso do conector do Spark MSSQL.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data, consulte [como implantar grandes de dados do SQL Server clusters no Kubernetes](deployment-guidance.md)