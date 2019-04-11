---
title: sys.query_store_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.query_store_wait_stats
- query_store_wait_stats
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_wait_stats catalog view
- sys.query_store_wait_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e91217f725251b17dadbcdddeb04b4d06d82642
ms.sourcegitcommit: 57f7e5f25161dbb4cc446e751ea74b1ac5f86165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2019
ms.locfileid: "59476662"
---
# <a name="sysquerystorewaitstats-transact-sql"></a>sys.query_store_wait_stats (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Contém informações sobre as informações de espera da consulta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**BIGINT**|Identificador da linha que representa as estatísticas de espera para plan_id, runtime_stats_interval_id, execution_type e wait_category. Ele é exclusivo somente para os intervalos de estatísticas de tempo de execução anterior. Para o intervalo ativo no momento, pode haver várias linhas que representa as estatísticas de espera para o plano referenciado pelo plan_id, com o tipo de execução representado pelo execution_type e categoria de espera representado por wait_category. Normalmente, uma linha representa as estatísticas de espera são liberadas para disco, enquanto outras (s) representam o estado na memória. Portanto, para obter o estado real para cada intervalo você precisa agregar as métricas, agrupando por plan_id, runtime_stats_interval_id, execution_type e wait_category. |  
|**plan_id**|**BIGINT**|Chave estrangeira. Ingressa [query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**BIGINT**|Chave estrangeira. Ingressa [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**wait_category**|**TINYINT**|Tipos de espera são categorizados usando a tabela a seguir e, em seguida, o tempo de espera é agregado entre essas categorias de espera. Categorias de espera diferentes exigem uma análise de acompanhamento diferente para resolver o problema, mas aguardar tipos de cliente potencial mesma categoria para uma experiência semelhante a solução de problemas e fornecer a consulta afetada Além disso, para as esperas é a que faltava para concluir o maioria dessas investigações com êxito.|
|**wait_category_desc**|**nvarchar(128)**|Para obter uma descrição textual do campo de categoria de espera, examine a tabela a seguir.|
|**execution_type**|**TINYINT**|Determina o tipo de execução da consulta:<br /><br /> 0 - execução regular (concluída com êxito)<br /><br /> 3 - cliente iniciado anulou a execução<br /><br /> 4 - exceção anulou a execução|  
|**execution_type_desc**|**nvarchar(128)**|Descrição textual do campo de tipo de execução:<br /><br /> 0 - regular<br /><br /> 3 - anulada<br /><br /> 4 - exceção|  
|**total_query_wait_time_ms**|**BIGINT**|Total `CPU wait` tempo para o plano de consulta dentro do intervalo de agregação e categoria (relatada em milissegundos) de espera.|
|**avg_query_wait_time_ms**|**FLOAT**|Média de duração da espera para o plano de consulta por execução dentro da categoria de espera e de intervalo de agregação (relatada em milissegundos).|
|**last_query_wait_time_ms**|**BIGINT**|Última duração da espera para o plano de consulta dentro do intervalo de agregação e categoria (relatada em milissegundos) de espera.|
|**min_query_wait_time_ms**|**BIGINT**|Mínimo `CPU wait` tempo para o plano de consulta dentro do intervalo de agregação e categoria (relatada em milissegundos) de espera.|
|**max_query_wait_time_ms**|**BIGINT**|Máximo `CPU wait` tempo para o plano de consulta dentro do intervalo de agregação e categoria (relatada em milissegundos) de espera.|
|**stdev_query_wait_time_ms**|**FLOAT**|`Query wait` desvio padrão de duração para a consulta planejar dentro do intervalo de agregação e categoria (relatada em milissegundos) de espera.|

## <a name="wait-categories-mapping-table"></a>Tabela de mapeamento de categorias de espera

"%" é usado como um caractere curinga
  
|Valor inteiro|Categoria de espera|Tipos de espera incluem na categoria|  
|-----------------|---------------|-----------------|  
|**0**|**Unknown (desconhecido)**|Unknown (desconhecido) |  
|**1**|**CPU**|SOS_SCHEDULER_YIELD|
|**2**|**Thread de trabalho**|THREADPOOL|
|**3**|**Bloqueio**|LCK_M_%|
|**4**|**Trava**|LATCH_%|
|**5**|**Trava de buffer**|% PAGELATCH_|
|**6**|**Buffer de e/s**|PAGEIOLATCH_%|
|**7**|**Compilação***|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|**8**|**SQL CLR**|CLR%, SQLCLR%|
|**9**|**Espelhamento**|DBMIRROR%|
|**10**|**Transaction**|XACT%, DTC%, TRAN_MARKLATCH_%, MSQL_XACT_%, TRANSACTION_MUTEX|
|**11**|**Idle**|SLEEP_%, LAZYWRITER_SLEEP, SQLTRACE_BUFFER_FLUSH, SQLTRACE_INCREMENTAL_FLUSH_SLEEP, SQLTRACE_WAIT_ENTRIES, FT_IFTS_SCHEDULER_IDLE_WAIT, XE_DISPATCHER_WAIT, REQUEST_FOR_DEADLOCK_SEARCH, LOGMGR_QUEUE, ONDEMAND_TASK_QUEUE, CHECKPOINT_QUEUE, XE_TIMER_EVENT|
|**12**|**PreEmptive**|PREEMPTIVE_%|
|**13**|**Service Broker**|% BROKER_ **(mas não BROKER_RECEIVE_WAITFOR)**|
|**14**|**Log tran e/s**|LOGMGR, LOGBUFFER, LOGMGR_RESERVE_APPEND, LOGMGR_FLUSH, LOGMGR_PMM_LOG, CHKPT, WRITELOG|
|**15**|**E/s de rede**|ASYNC_NETWORK_IO, NET_WAITFOR_PACKET, PROXY_NETWORK_IO, EXTERNAL_SCRIPT_NETWORK_IOF|
|**16**|**Parallelism**|CXPACKET, EXCHANGE|
|**17**|**Memória**|RESOURCE_SEMAPHORE, CMEMTHREAD, CMEMPARTITIONED, EE_PMOLOCK, MEMORY_ALLOCATION_EXT, RESERVED_MEMORY_ALLOCATION_EXT, MEMORY_GRANT_UPDATE|
|**18**|**Espera de usuário**|WAITFOR, WAIT_FOR_RESULTS, BROKER_RECEIVE_WAITFOR|
|**19**|**Rastreamento**|TRACEWRITE, SQLTRACE_LOCK, SQLTRACE_FILE_BUFFER, SQLTRACE_FILE_WRITE_IO_COMPLETION, SQLTRACE_FILE_READ_IO_COMPLETION, SQLTRACE_PENDING_BUFFER_WRITERS, SQLTRACE_SHUTDOWN, QUERY_TRACEOUT, TRACE_EVTNOTIFF|
|**20**|**Pesquisa de Texto Completo**|FT_RESTART_CRAWL, FULLTEXT GATHERER, MSSEARCH, FT_METADATA_MUTEX, FT_IFTSHC_MUTEX, FT_IFTSISM_MUTEX, FT_IFTS_RWLOCK, FT_COMPROWSET_RWLOCK, FT_MASTER_MERGE, FT_PROPERTYLIST_CACHE, FT_MASTER_MERGE_COORDINATOR, PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC|
|**21**|**Outras e/s de disco**|ASYNC_IO_COMPLETION, IO_COMPLETION, BACKUPIO, WRITE_COMPLETION, IO_QUEUE_LIMIT, IO_RETRY|
|**22**|**Replicação**|SE_REPL_%, REPL_%, HADR_% **(but not HADR_THROTTLE_LOG_RATE_GOVERNOR)**, PWAIT_HADR_%, REPLICA_WRITES, FCB_REPLICA_WRITE, FCB_REPLICA_READ, PWAIT_HADRSIM|
|**23**|**Administrador de taxa de log**|LOG_RATE_GOVERNOR, POOL_LOG_RATE_GOVERNOR, HADR_THROTTLE_LOG_RATE_GOVERNOR, INSTANCE_LOG_RATE_GOVERNOR|

**Compilação** categoria de espera não é suportada atualmente.

## <a name="permissions"></a>Permissões

 Requer a permissão `VIEW DATABASE STATE`.  
  
## <a name="see-also"></a>Consulte também

- [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)
- [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)
- [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)
- [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)
- [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)
- [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)
- [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)
- [Procedimentos armazenados do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
