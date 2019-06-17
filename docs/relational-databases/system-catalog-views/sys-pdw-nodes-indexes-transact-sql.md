---
title: sys.pdw_nodes_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 261bcb7f-a906-4979-b274-bc5f1aa66426
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c13e41abea44bdbe0f954518f42aab118360a155
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62715833"
---
# <a name="syspdwnodesindexes-transact-sql"></a>sys.pdw_nodes_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Retorna os índices para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|ID do objeto ao qual este índice pertence.||  
|nome|**sysname**|Nome do índice. Nome é exclusivo somente dentro do objeto. NULL = Heap||  
|index_id|**int**|ID do índice. index_id só é exclusivo dentro do objeto.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> > 1 = índice não clusterizado||  
|type|**tinyint**|Tipo de índice:<br /><br /> 0 = Heap<br /><br /> 1 = Clusterizado<br /><br /> 2 = não clusterizados<br /><br /> 5 = índice de columnstore otimizado em memória clusterizado xVelocity|  
|type_desc|**nvarchar(60)**|Descrição de tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> COLUMNSTORE CLUSTERIZADO||  
|is_unique|**bit**|0 = O índice não é exclusivo.|Sempre 0.|  
|data_space_id|**int**|ID do espaço de dados para esse índice. O espaço de dados é um grupo de arquivos ou um esquema de partição.<br /><br /> 0 = object_id é uma função com valor de tabela.||  
|ignore_dup_key|**bit**|0 = IGNORE_DUP_KEY está OFF.|Sempre 0.|  
|is_primary_key|**bit**|1 = O índice faz parte de uma restrição PRIMARY KEY.|Sempre 0.|  
|is_unique_constraint|**bit**|1 = O índice faz parte de uma restrição UNIQUE.|Sempre 0.|  
|fill_factor|**tinyint**|> 0 = porcentagem de FILLFACTOR usada quando o índice foi criado ou reconstruído.<br /><br /> 0 = Valor padrão|Sempre 0.|  
|is_padded|**bit**|0 = PADINDEX está OFF.|Sempre 0.|  
|is_disabled|**bit**|1 = O índice está desabilitado.<br /><br /> 0 = O índice não está desabilitado.||  
|is_hypothetical|**bit**|0 = O índice não é hipotético.|Sempre 0.|  
|allow_row_locks|**bit**|1 = O índice permite bloqueios de linha.|Sempre 1.|  
|allow_page_locks|**bit**|1 = O índice permite bloqueios de página.|Sempre 1.|  
|has_filter|**bit**|0 = O índice não tem um filtro.|Sempre 0.|  
|filter_definition|**nvarchar(max)**|Expressão do subconjunto de linhas incluído no índice filtrado.|Sempre NULL.|  
|pdw_node_id|**int**|Identificador exclusivo de um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nó.|NOT NULL|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse e Parallel Data Warehouse exibições do catálogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
