---
title: sys.dm_os_memory_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_nodes_TSQL
- sys.dm_os_memory_nodes
- sys.dm_os_memory_nodes_TSQL
- dm_os_memory_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_nodes dynamic management view
ms.assetid: bf4032fe-7db1-40e9-a62e-d69cebff4b44
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7d1be540f73a5a5e625a1f33f1c3f24e409fd307
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265761"
---
# <a name="sysdmosmemorynodes-transact-sql"></a>sys.dm_os_memory_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  As alocações internas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam o gerenciador de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Controle da diferença entre contadores de memória do processo do **sys.dm_os_process_memory** e contadores internos pode indicar uso de memória de componentes externos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espaço de memória.  
  
 Os nós são criados por nós físicos de memória NUMA. Eles podem ser diferentes de nós de CPU no **DM os_nodes**.  
  
 Nenhuma alocação feita diretamente por meio de rotinas de alocações de memória do Windows é rastreada. A tabela a seguir fornece informações sobre alocações de memória feitas usando somente interfaces do gerenciador de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_memory_nodes**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**memory_node_id**|**smallint**|Especifica a ID do nó de memória. Relacionado ao **memory_node_id** dos **DM os_memory_clerks**. Não permite valor nulo.|  
|**virtual_address_space_reserved_kb**|**bigint**|Indica o número de reservas de endereço virtual, em quilobytes (KB), que não são nem confirmadas nem mapeadas em páginas físicas. Não permite valor nulo.|  
|**virtual_address_space_committed_kb**|**bigint**|Especifica a quantidade de endereço virtual, em KB, que foi comprometida ou mapeada em páginas físicas. Não permite valor nulo.|  
|**locked_page_allocations_kb**|**bigint**|Especifica a quantidade de memória física, em KB, que foi bloqueada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**single_pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Parcela da memória confirmada, em KB, que está alocada pelo uso do alocador de página única pelos threads em execução nesse nó. Essa memória é alocada do pool de buffers. Esse valor indica o nó em que ocorreu a solicitação de alocações; não o local físico em que a solicitação de alocação foi atendida.|  
|**pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica a quantidade de memória confirmada, em KB, alocada por esse nó NUMA pelo Alocador de Página do Gerenciador de Memória. Não permite valor nulo.|  
|**multi_pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Parcela da memória confirmada, em KB, que está alocada pelo uso do alocador de várias páginas pelos threads em execução nesse nó. Essa memória é externa ao pool de buffers. Esse valor indica o nó em que ocorreram as solicitações de alocação; não o local físico em que a solicitação de alocação foi atendida.|  
|**shared_memory_reserved_kb**|**bigint**|Especifica a quantidade de memória compartilhada, em KB, que foi reservada nesse nó. Não permite valor nulo.|  
|**shared_memory_committed_kb**|**bigint**|Especifica a quantidade de memória compartilhada, em KB, que foi confirmada nesse nó. Não permite valor nulo.|  
|**cpu_affinity_mask**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Somente para uso interno. Não permite valor nulo.|  
|**online_scheduler_mask**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Somente para uso interno. Não permite valor nulo.|  
|**processor_group**|**smallint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Somente para uso interno. Não permite valor nulo.|  
|**foreign_committed_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica a quantidade de memória confirmada, em KB, de outros nós de memória. Não permite valor nulo.|  
|**target_kb** |**bigint** |**Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Especifica a meta de memória para o nó de memória, em KB. |   
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` permissão no banco de dados. Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e básica, requer a **administrador de servidor** ou uma **administrador do Active Directory do Azure** conta.   

## <a name="see-also"></a>Consulte também  
  [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


