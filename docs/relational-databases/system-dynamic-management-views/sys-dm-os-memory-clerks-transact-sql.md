---
title: DM os_memory_clerks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_clerks
- sys.dm_os_memory_clerks
- dm_os_memory_clerks_TSQL
- sys.dm_os_memory_clerks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_clerks dynamic management view
ms.assetid: 1d556c67-5c12-46d5-aa8c-7ec1bb858df7
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 89493294fe08f82b3a61bb8eab7a99e7a941ed28
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265776"
---
# <a name="sysdmosmemoryclerks-transact-sql"></a>sys.dm_os_memory_clerks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o conjunto de todos os administradores de memória que estão ativos no momento na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_memory_clerks**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**memory_clerk_address**|**varbinary(8)**|Especifica o endereço de memória exclusivo do administrador de memória. Esta é a coluna de chave primária. Não permite valor nulo.|  
|**type**|**nvarchar(60)**|Especifica o tipo do administrador de memória. Todo administrador de memória tem um tipo específico, como os Administradores MEMORYCLERK_SQLCLR do CLR. Não permite valor nulo.|  
|**name**|**nvarchar(256)**|Especifica o nome atribuído internamente deste administrador de memória. Um componente pode ter vários administradores de memória de um tipo específico. Um componente pode optar por usar nomes específicos para identificar administradores de memória do mesmo tipo. Não permite valor nulo.|  
|**memory_node_id**|**smallint**|Especifica a ID do nó de memória. Não permite valor nulo.|  
|**single_pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].|  
|**pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica a quantidade de memória de páginas alocada em KB (quilobytes) para este administrador de memória. Não permite valor nulo.|  
|**multi_pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade de memória de várias páginas alocada em KB. Esta é a quantidade de memória alocada usando o alocador de várias páginas dos nós de memória. Esta memória é alocada fora do pool de buffers e se beneficia do alocador virtual dos nós de memória. Não permite valor nulo.|  
|**virtual_memory_reserved_kb**|**bigint**|Especifica a quantidade de memória virtual reservada por um administrador de memória. Não permite valor nulo.|  
|**virtual_memory_committed_kb**|**bigint**|Especifica a quantidade de memória virtual confirmada por um administrador de memória. A quantidade de memória confirmada sempre deve ser menor que a quantidade de memória reservada. Não permite valor nulo.|  
|**awe_allocated_kb**|**bigint**|Especifica a quantidade de memória em KB (quilobytes) bloqueada na memória física e não paginada para fora pelo sistema operacional. Não permite valor nulo.|  
|**shared_memory_reserved_kb**|**bigint**|Especifica a quantidade de memória compartilhada reservada por um administrador de memória. A quantidade de memória reservada para uso por mapeamento de arquivo e memória compartilhada. Não permite valor nulo.|  
|**shared_memory_committed_kb**|**bigint**|Especifica a quantidade de memória compartilhada confirmada pelo administrador de memória. Não permite valor nulo.|  
|**page_size_in_bytes**|**bigint**|Especifica a granularidade da alocação de páginas para este administrador de memória. Não permite valor nulo.|  
|**page_allocator_address**|**varbinary(8)**|Especifica o endereço do alocador de páginas. Esse endereço é exclusivo para um administrador de memória e podem ser usado em **DM os_memory_objects** para localizar objetos de memória que são associados a esse administrador. Não permite valor nulo.|  
|**host_address**|**varbinary(8)**|Especifica o endereço de memória do host desse administrador de memória. Para obter mais informações, consulte [sys.dm_os_hosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md). Componentes, tais como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, acessam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos de memória por meio da interface de host.<br /><br /> 0x00000000 = O administrador de memória pertence ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Não permite valor nulo.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões 

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` permissão no banco de dados. Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e básica, requer a **administrador de servidor** ou uma **administrador do Active Directory do Azure** conta.   
  
## <a name="remarks"></a>Comentários  
 O gerenciador de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste em uma hierarquia de três camadas. Na parte inferior da hierarquia estão os nós de memória. O próximo nível médio consiste em administradores de memória, caches de memória e pools de memória. A camada superior consiste em objetos de memória. Esses objetos geralmente são usados para alocar memória em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os nós de memória fornecem a interface e a implementação para alocadores de baixo nível. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], apenas os administradores de memória têm acesso a nós de memória. Os administradores de memória acessam interfaces de nó de memória para alocar memória. Os nós de memória também controlam a memória alocada, usando o administrador para diagnósticos. Todo componente que aloca uma quantidade significativa de memória deve criar seu próprio administrador de memória e alocar toda a sua memória usando as interfaces do administrador. Frequentemente, os componentes criam seus administradores correspondentes no momento em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado.  
  
## <a name="see-also"></a>Consulte também  

 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
  
  


