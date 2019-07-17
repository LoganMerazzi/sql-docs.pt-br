---
title: sys.dm_column_store_object_pool (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a8a58ca7-0a7d-4786-bfd9-e8894bd345dd
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83369736ee18c36b3967bbbd129e0fd64574a2ed
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265994"
---
# <a name="sysdmcolumnstoreobjectpool-transact-sql"></a>sys.dm_column_store_object_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Retorna contagens de diferentes tipos de uso de pool de memória de objeto para objetos de índice columnstore.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|`database_id`|`int`|ID do banco de dados. Isso é exclusivo dentro de uma instância de um banco de dados do SQL Server ou um servidor de banco de dados SQL do Azure. |  
|`object_id`|`int`|A ID do objeto. O objeto é uma da object_types. | 
|`index_id`|`int`|ID do índice columnstore.|  
|`partition_number`|`bigint`|Número de partição com base 1 no índice ou heap. Cada tabela ou exibição tem pelo menos uma partição.| 
|`column_id`|`int`|ID da coluna columnstore. Isso é NULL para DELETE_BITMAP.| 
|`row_group_id`|`int`|ID do rowgroup.|
|`object_type`|`smallint`|1 = COLUMN_SEGMENT<br /><br /> 2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY<br /><br /> 3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY<br /><br /> 4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY<br /><br /> 5 = COLUMN_SEGMENT_DELETE_BITMAP|  
|`object_type_desc`|`nvarchar(60)`|COLUMN_SEGMENT - um segmento de coluna. `object_id` é a ID do segmento. Um segmento armazena todos os valores para uma coluna dentro de um grupo de linhas. Por exemplo, se uma tabela tiver 10 colunas, há 10 segmentos de coluna por rowgroup. <br /><br /> COLUMN_SEGMENT_PRIMARY_DICTIONARY - um dicionário global que contém informações de pesquisa para todos os segmentos de coluna na tabela.<br /><br /> COLUMN_SEGMENT_SECONDARY_DICTIONARY - um dicionário local associado a uma coluna.<br /><br /> COLUMN_SEGMENT_BULKINSERT_DICTIONARY - outra representação de dicionário global. Isso fornece uma pesquisa inversa de valor para dictionary_id. Usado para criar segmentos compactados como parte do motor de tupla ou de carregamento em massa.<br /><br /> Exclui do COLUMN_SEGMENT_DELETE_BITMAP - um bitmap que controla o segmento. Há um bitmap de exclusão por partição.|  
|`access_count`|`int`|Número de leitura ou gravação acessos a este objeto.|  
|`memory_used_in_bytes`|`bigint`|Memória usada por este objeto no pool de objeto.|  
|`object_load_time`|`datetime`|Tempo de relógio para quando o object_id foi trazida para o pool de objetos.|  
  
## <a name="permissions"></a>Permissões  

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` permissão no banco de dados. Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e básica, requer a **administrador de servidor** ou uma **administrador do Active Directory do Azure** conta.   
 
## <a name="see-also"></a>Consulte também  
  
 [Exibições e funções de gerenciamento dinâmico relacionadas ao índice &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  
