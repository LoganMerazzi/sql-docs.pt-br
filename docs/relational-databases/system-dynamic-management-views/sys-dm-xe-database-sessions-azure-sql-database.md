---
title: sys.dm_xe_database_sessions (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 33ea5179-16bb-4abd-96cc-9bc696e80987
author: MightyPen
ms.author: genemi
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ab0d59026bd172cb1e3fd51a92c3e5bb8b83b2e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090368"
---
# <a name="sysdmxedatabasesessions-azure-sql-database"></a>sys.dm_xe_database_sessions (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre os eventos da sessão. Eventos são pontos de execução discretos. Predicados poderão ser se aplicados a eventos para fazer com que parem de acionar caso o evento não contiver a informação exigida.  
  
||  
|-|  
|**Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e versões posteriores.|  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|O endereço da memória da sessão de evento. Não permite valor nulo.|  
|event_name|**nvarchar(60)**|O nome do evento ao qual uma ação está associada. Não permite valor nulo.|  
|event_package_guid|**uniqueidentifier**|A GUID para o pacote que contém o evento. Não permite valor nulo.|  
|event_predicate|**nvarchar(2048)**|Uma representação XML da árvore de predicado que é aplicada ao evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
A partir de 2015-07-13, 'sys.dm_xe_objects' é um desses DMVs de XEvents que não contêm Database"no nome. Não é um erro de digitação ou erro na coluna do lado direito da tabela a seguir. O nome é o mesmo no Microsoft SQL Server e banco de dados SQL.  
  
|De|Para|Relação|  
|--------|------|----------------|  
|sys.dm_xe_database_session_events.event_session_address|sys.dm_xe_database_sessions.address|Muitos para um|  
|sys.dm_xe_database_session_events.event_package_guid, sys.dm_xe_database_session_events.event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|Muitos para um|  
  
## <a name="see-also"></a>Consulte também  
[Eventos estendidos no Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
[Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
 
