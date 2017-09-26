---
title: Importar e exportar dados do SQL Server e do Banco de Dados SQL do Azure | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 6e754198cf82a7ba0752fe8f20c3780a8ac551d7
ms.openlocfilehash: 3c41be0642b13b63367c5601b716b506808472e7
ms.contentlocale: pt-br
ms.lasthandoff: 09/14/2017

---
# <a name="import-and-export-data-from-sql-server-and-azure-sql-database"></a>Importar e exportar dados do SQL Server e do Banco de Dados SQL do Azure
Use uma variedade de métodos para importar e exportar dados do SQL Server e do Banco de Dados SQL do Azure. Esses métodos incluem instruções Transact-SQL, ferramentas de linha de comando e assistentes.

Também importe e exporte dados em uma variedade de formatos. Esses formatos incluem arquivos simples, Excel, os principais bancos de dados relacionais e vários serviços de nuvem.

## <a name="methods-for-importing-and-exporting-data"></a>Métodos para importar e exportar dados

### <a name="use-transact-sql-statements"></a>Usar instruções Transact-SQL
Importe dados com os comandos `BULK INSERT` ou `OPENROWSET(BULK...)`. Normalmente, você executa esses comandos no SSMS (SQL Server Management Studio). Para obter mais informações, consulte [Importar dados em massa usando BULK INSERT ou OPENROWSET(BULK...)](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

### <a name="use-bcp-from-the-command-prompt"></a>Usar o BCP no prompt de comando
Importe e exporte dados com o utilitário de linha de comando BCP. Para obter mais informações, consulte [Importar e exportar dados em massa usando o utilitário BCP](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

### <a name="use-the-sql-server-import-and-export-wizard"></a>Usar o Assistente para Importação e Exportação do SQL Server
Importe ou exporte dados de uma variedade de fontes e destinos com o Assistente para Importação e Exportação do SQL Server. Para usar o assistente, você deve ter o SSIS (SQL Server Integration Services) ou o SSDT (SQL Server Data Tools) instalado. Para obter mais informações, consulte [Importar e exportar dados com o Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

### <a name="design-your-own-import-or-export"></a>Criar sua própria importação ou exportação
Se desejar criar uma importação de dados personalizada, use um dos seguintes recursos ou serviços:
-   SQL Server Integration Services. Para obter mais informações, consulte [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).
-   Azure Data Factory. Para obter mais informações, consulte [Introdução ao Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-introduction).

## <a name="data-formats-for-import-and-export"></a>Formatos de dados para importação e exportação

### <a name="supported-formats"></a>Formatos com suporte

Importe e exporte dados para arquivos simples ou uma variedade de outros formatos de arquivo, bancos de dados relacionais e serviços de nuvem. Para saber mais sobre essas opções de ferramentas específicas, consulte os seguintes tópicos
-   Para o Assistente para Importação e Exportação do SQL Server, consulte [Conectar-se a fontes de dados com o Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md).
-   Para o SQL Server Integration Services, consulte [Conexões do SSIS (Integration Services)](../../integration-services/connection-manager/integration-services-ssis-connections.md).
-   Para o Azure Data Factory, consulte [Conectores do Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-amazon-redshift-connector).

### <a name="commonly-used-data-formats"></a>Formatos de dados usados com frequência

Há considerações especiais e exemplos disponíveis para alguns formatos de dados usados com frequência. Para saber mais sobre esses formatos de dados, consulte os seguintes tópicos:
-   Para o Excel, consulte [Importar do Excel](import-data-from-excel-to-sql.md).
-   Para o JSON, consulte [Importar documentos JSON](../json/import-json-documents-into-sql-server.md).
-   Para o XML, consulte [Importar e exportar documentos XML](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md).
-   Para o Armazenamento de Blobs do Azure, consulte [Importar e exportar do Armazenamento de Blobs do Azure](examples-of-bulk-access-to-data-in-azure-blob-storage.md).

## <a name="next-steps"></a>Próximas etapas
Caso não tenha certeza de onde começar com a tarefa de importação ou exportação, considere a possibilidade de usar o Assistente para Importação e Exportação do SQL Server. Para obter uma introdução rápida, consulte [Começar com este exemplo simples do Assistente para Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).
