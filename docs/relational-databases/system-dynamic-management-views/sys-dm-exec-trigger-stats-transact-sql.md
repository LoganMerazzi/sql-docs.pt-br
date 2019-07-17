---
title: sys.dm_exec_trigger_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 65e54b90fa036e738f2e1e6a28498559051011a5
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262210"
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna estatísticas de desempenho de agregação dos gatilhos em cache. A exibição contém uma linha por gatilho e o tempo de vida da linha equivale ao tempo de permanência do gatilho em cache. Quando um gatilho é removido do cache, a linha correspondente é eliminada desta exibição. Nesse momento, um evento de rastreamento do SQL de estatísticas de desempenho é gerado semelhante à **DM exec_query_stats**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados no qual o gatilho reside.|  
|**object_id**|**int**|Número de identificação de objeto do gatilho.|  
|**type**|**char(2)**|Tipo do objeto:<br /><br /> TA = Gatilho (CLR) de assembly<br /><br /> TR = Gatilho SQL|  
|**Type_desc**|**nvarchar(60)**|Descrição do tipo de objeto:<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|Isso pode ser usado para correlacionar com consultas no **DM exec_query_stats** que foram executadas a partir deste gatilho.|  
|**plan_handle**|**varbinary(64)**|Identificador do plano na memória. Esse identificador é transitório e permanece constante somente enquanto o plano permanece no cache. Esse valor pode ser usado com o **DM exec_cached_plans** exibição de gerenciamento dinâmico.|  
|**cached_time**|**datetime**|Hora em que o gatilho foi adicionado ao cache.|  
|**last_execution_time**|**datetime**|Hora da última execução do gatilho.|  
|**execution_count**|**bigint**|O número de vezes que o gatilho foi executado desde sua última compilação.|  
|**total_worker_time**|**bigint**|A quantidade total de tempo de CPU, em microssegundos, consumido por execuções deste gatilho desde sua compilação.|  
|**last_worker_time**|**bigint**|Tempo de CPU, em microssegundos, consumido na última vez em que o gatilho foi executado.|  
|**min_worker_time**|**bigint**|O máximo tempo de CPU, em microssegundos, que este gatilho consumiu durante uma única execução.|  
|**max_worker_time**|**bigint**|O máximo tempo de CPU, em microssegundos, que este gatilho consumiu durante uma única execução.|  
|**total_physical_reads**|**bigint**|O número total de leituras físicas efetuadas por execuções deste gatilho desde sua compilação.|  
|**last_physical_reads**|**bigint**|O número de leituras físicas efetuadas na última vez em que o gatilho foi executado.|  
|**min_physical_reads**|**bigint**|O número mínimo de leituras físicas que este gatilho efetuou durante uma única execução.|  
|**max_physical_reads**|**bigint**|O número máximo de leituras físicas que este gatilho efetuou durante uma única execução.|  
|**total_logical_writes**|**bigint**|O número total de gravações lógicas efetuadas por execuções deste gatilho desde sua compilação.|  
|**last_logical_writes**|**bigint**|O número de gravações lógicas efetuadas na última vez em que o gatilho foi executado.|  
|**min_logical_writes**|**bigint**|O número mínimo de gravações lógicas que este gatilho efetuou durante uma única execução.|  
|**max_logical_writes**|**bigint**|O número máximo de gravações lógicas que este gatilho efetuou durante uma única execução.|  
|**total_logical_reads**|**bigint**|O número total de leituras lógicas efetuadas por execuções deste gatilho desde sua compilação.|  
|**last_logical_reads**|**bigint**|O número de leituras lógicas efetuadas na última vez em que o gatilho foi executado.|  
|**min_logical_reads**|**bigint**|O número mínimo de leituras lógicas que este gatilho efetuou durante uma única execução.|  
|**max_logical_reads**|**bigint**|O número máximo de leituras lógicas que este gatilho efetuou durante uma única execução.|  
|**total_elapsed_time**|**bigint**|O tempo total decorrido, em microssegundos, de execuções concluídas deste gatilho.|  
|**last_elapsed_time**|**bigint**|Tempo decorrido, em microssegundos, da execução concluída mais recente deste gatilho.|  
|**min_elapsed_time**|**bigint**|O tempo mínimo decorrido, em microssegundos, de qualquer execução concluída deste gatilho.|  
|**max_elapsed_time**|**bigint**|O tempo máximo decorrido, em microssegundos, de qualquer execução concluída deste gatilho.| 
|**total_spills**|**bigint**|O número total de páginas despejadas pela execução deste gatilho desde sua compilação.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**last_spills**|**bigint**|O número de páginas despejadas a última vez em que o gatilho foi executado.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**min_spills**|**bigint**|O número mínimo de páginas que esse gatilho já foram liberados durante uma única execução.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**max_spills**|**bigint**|O número máximo de páginas que esse gatilho já foram liberados durante uma única execução.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**total_page_server_reads**|**bigint**|O número total de leituras de página de servidor efetuadas por execuções deste gatilho desde sua compilação.<br /><br /> **Aplica-se ao**: Em hiperescala do banco de dados SQL do Azure|  
|**last_page_server_reads**|**bigint**|O número de leituras de página de servidor efetuadas na última vez em que o gatilho foi executado.<br /><br /> **Aplica-se ao**: Em hiperescala do banco de dados SQL do Azure|  
|**min_page_server_reads**|**bigint**|O número mínimo de servidor de páginas lê que este gatilho efetuou durante uma única execução.<br /><br /> **Aplica-se ao**: Em hiperescala do banco de dados SQL do Azure|  
|**max_page_server_reads**|**bigint**|O número máximo de servidor de páginas lê que este gatilho efetuou durante uma única execução.<br /><br /> **Aplica-se ao**: Em hiperescala do banco de dados SQL do Azure|  

  
## <a name="remarks"></a>Comentários  
 No [!INCLUDE[ssSDS](../../includes/sssds-md.md)], as exibições de gerenciamento dinâmico não podem expor informações que afetarão a contenção do banco de dados ou informações sobre outros bancos de dados aos quais o usuário tem acesso. Para evitar a exposição dessas informações, cada linha que contém dados que não pertencem ao locatário conectado será filtrada.  

As estatísticas na exibição são atualizadas quando uma consulta é concluída.  
  
## <a name="permissions"></a>Permissões  

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` permissão no banco de dados. Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e básica, requer a **administrador de servidor** ou uma **administrador do Active Directory do Azure** conta.   
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre os cinco principais gatilhos identificados por tempo médio decorrido.  
  
```sql  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>Consulte também  
[Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
