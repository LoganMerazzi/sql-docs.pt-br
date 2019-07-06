---
title: Fontes de dados com suporte em modelos de tabela 1400 do Analysis Services do SQL Server | Microsoft Docs
ms.date: 07/02/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 246375015786cf67685c89f368f83662539da36b
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597347"
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>Fontes de dados com suporte no SQL Server Analysis Services, modelos de tabela 1400

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

Este artigo descreve os tipos de fontes de dados que podem ser usados com modelos de tabela do SQL Server Analysis Services (SSAS) no nível de compatibilidade 1400. 

Para modelos de tabela do SSAS nos níveis de compatibilidade 1200 e inferior, consulte [fontes de dados com suporte em modelos do SQL Server Analysis Services tabulares 1200](data-sources-supported-ssas-tabular.md).

Para o Azure Analysis Services, consulte [fontes de dados com suporte no Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource).


## <a name="cloud-data-sources"></a>Fontes de dados de nuvem

|Fonte de dados  |Na memória  |DirectQuery  |
|---------|---------|---------|
|Banco de dados SQL do Azure <sup> [1](#ae)</sup>    |   Sim      |    Sim      |
|Azure SQL Data Warehouse     |   Sim      |   Sim       |
|Armazenamento de blobs do Azure     |   Sim       |    Não      |
|Armazenamento de tabelas do Azure    |   Sim       |    Não      |
|Azure Cosmos DB     |  Sim        |  Não        |
|Azure Data Lake Store (Gen1)<sup>[2](#gen2)</sup>      |   Sim       |    Não      |
|HDFS do HDInsight do Azure    |     Sim     |   Não       |
|Azure HDInsight Spark <sup> [3](#databricks)</sup>     |   Sim       |   Não       |
||||

<a name="ae">1</a> -não há suporte para o azure SQL banco de dados Always Encrypted.   
<a name="gen2">2</a> -Gen2 do ADLS não é suportado atualmente.   
<a name="databricks">3</a> – azure Databricks usando o Spark connector não é suportado atualmente.   




**Provedor**   
Na memória e os modelos DirectQuery se conectar a fontes de dados do Azure usam o .NET Framework Data Provider para SQL Server.

## <a name="on-premises-data-sources"></a>Fontes de dados locais

### <a name="supported-by-in-memory-and-directquery-models"></a>Compatível com modelos na memória e DirectQuery

|Fonte de dados | Provedor na memória | Provedor do DirectQuery |
|  --- | --- | --- |
| SQL Server <sup>[4](#aeop)</sup> |SQL Server Native Client 11.0, provedor Microsoft OLE DB para SQL Server, o .NET Framework Data Provider para SQL Server | Provedor de dados do .NET Framework para SQL Server |
| SQL Server Data Warehouse |SQL Server Native Client 11.0, provedor Microsoft OLE DB para SQL Server, o .NET Framework Data Provider para SQL Server | Provedor de dados do .NET Framework para SQL Server |
| Oracle |Provedor Microsoft OLE DB para Oracle, o provedor de dados Oracle para .NET |Provedor de dados Oracle para .NET | |
| Teradata |Provedor OLE DB para Teradata, provedor de dados Teradata para .NET |Provedor de dados Teradata para .NET | |
| | | |

<a name="aeop">4</a> -banco de dados do banco de dados SQL e SQL Server Always Encrypted tem suporte como um DirectQuery [fonte de dados do cliente](data-sources-supported-ssas-tabular.md#bkmk_supported_ds_dq) em modelos de tabela do SQL Server Analysis Services no nível de compatibilidade 1200 apenas. Não há suporte para o banco de dados do banco de dados SQL do Azure e SQL Server Always Encrypted no Azure Analysis Services.       

> [!NOTE]
> Para modelos na memória, provedores OLE DB podem fornecer um melhor desempenho para dados em larga escala. Ao escolher entre diferentes provedores para a mesma fonte de dados, tente primeiro o provedor OLE DB.  

### <a name="supported-by-in-memory-models-only"></a>Com suporte apenas a modelos na memória

|banco de dados  |
|---------|---------|---------|
|Banco de dados do Access     | 
|SQL Server Analysis Services     | 
|IBM Informix (beta) | 
|Documento JSON     | 
|Linhas de binário     | 
|Banco de dados MySQL     | 
|Banco de dados PostgreSQL    | Sim | Não
|SAP HANA   | Sim | Não
|SAP Business Warehouse    | Sim | Não
|Banco de dados Sybase     | Sim | Não
|||

|Arquivo  |  
|---------|---------|
|Pasta de trabalho do Excel     |
|Pasta     | 
|JSON | 
|Texto/CSV    | 
|Tabela XML    | 
|||

|Serviços online  |  
|---------|---------|
|Dynamics 365      |
|Exhange Online     |
|Objetos de Saleforce    | 
|Relatórios do Salesforce     |
|Lista do SharePoint Online     |
|||

|Outro  |  
|---------|---------|
|Active Directory      | 
|Exhange     |  
|Feed OData     | 
|Consulta ODBC     | 
|OLE DB  | 
|Lista do SharePoint | 
|||

## <a name="see-also"></a>Confira também

[Fontes de dados com suporte no SQL Server Analysis Services, modelos de tabela 1200](data-sources-supported-ssas-tabular.md)

[Fontes de dados com suporte no Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
