---
title: Propriedades (OLE DB) da fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 923215eb107ab72011dc4697b3beaee157b6ed4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128666"
---
# <a name="data-source-properties-ole-db"></a>Propriedades da fonte de dados (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client implementa propriedades da fonte de dados da seguinte maneira.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W: Leitura/gravação padrão: Nenhum<br /><br /> Descrição: O valor de DBPROP_CURRENTCATALOG informa o banco de dados atual para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessão do provedor OLE DB do Native Client. A definição do valor da propriedade tem o mesmo efeito de definir o banco de dados atual usando a instrução USE *database* do [!INCLUDE[tsql](../../includes/tsql-md.md)].<br /><br /> Do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] em diante, se você chamar [sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) e especificar o nome do banco de dados em minúsculas, mesmo que o banco de dados tenha sido criado originalmente com um nome com maiúsculas e minúsculas, DBPROP_CURRENTCATALOG retornará o nome em minúsculas. Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], DBPROP_CURRENTCATALOG retornará as maiúsculas e minúsculas esperadas.|  
|DBPROP_MULTIPLECONNECTIONS|R/W: Leitura/gravação padrão: VARIANT_FALSE<br /><br /> Descrição: Se a conexão estiver executando um comando que não produz um conjunto de linhas ou produz um conjunto de linhas que não é um cursor de servidor e executar outro comando, uma nova conexão será criada para executar o novo comando se DBPROP_MULTIPLECONNECTIONS for VARIANT_TRUE.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client não criará outra conexão se DBPROP_MULTIPLECONNECTION for VARIANT_FALSE ou se uma transação está ativa na conexão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retornará DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS for VARIANT_FALSE e retornará E_FAIL se houver uma transação ativa. As transações e o bloqueio são gerenciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por conexão. Se uma segunda conexão for gerada, os comandos nas conexões separadas não compartilharão bloqueios. Para assegurar um comando não bloqueie o outro, mantenha os bloqueios em linhas solicitadas pelo outro comando. Isto também se aplica à criação de várias sessões.<br /><br /> Cada sessão tem uma conexão separada.|  
  
 Na propriedade específica do provedor definida DBPROPSET_SQLSERVERDATASOURCE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client define as seguintes propriedades de fonte de dados adicionais.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W: Leitura/gravação padrão: VARIANT_FALSE<br /><br /> Descrição: Para habilitar a cópia em massa da memória, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, a sessão recém-criada permite que o consumidor acesse a interface [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md).<br /><br /> Se a propriedade for definida como VARIANT_TRUE, a interface **IRowsetFastLoad** ficará disponível por meio de **IOpenRowset::OpenRowset**, solicitando a interface **IID_IRowsetFastLoad** ou definindo **SSPROP_IRowsetFastLoad** como VARIANT_TRUE.|  
|SSPROP_ENABLEBULKCOPY|R/W: Leitura/gravação padrão: VARIANT_FALSE<br /><br /> Descrição: Para habilitar a cópia em massa de arquivos, a propriedade SSPROP_ENABLEBULKCOPY deve ser definida como VARIANT_TRUE. Com essa propriedade definida na fonte de dados, o acesso do consumidor à interface IBCPSession está disponível no nível de Sessions.<br /><br /> SSPROP_IRowsetFastLoad também deve ser definido como VARIANT_TRUE.|  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
