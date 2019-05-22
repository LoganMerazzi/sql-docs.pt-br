---
title: sys.query_store_runtime_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9df0a31b6a15bfedd02e281b6e9bc5367144e9a9
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65980053"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contém informações sobre as informações de estatísticas de execução de tempo de execução da consulta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|Identificador da linha que representa as estatísticas de execução de tempo de execução para o **plan_id**, **execution_type** e **runtime_stats_interval_id**. Ele é exclusivo somente para os intervalos de estatísticas de tempo de execução anterior. Para o intervalo ativo no momento pode haver várias linhas que representa as estatísticas de tempo de execução para o plano referenciado pelo **plan_id**, com o tipo de execução representado pelo **execution_type**. Normalmente, uma linha representa as estatísticas de tempo de execução que são liberadas no disco, enquanto outras (s) representam o estado na memória. Portanto, para obter o estado real para cada intervalo é necessário agregar as métricas, agrupando **plan_id**, **execution_type** e **runtime_stats_interval_id**.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**plan_id**|**bigint**|Chave estrangeira. Ingressa [query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Chave estrangeira. Ingressa [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**execution_type**|**tinyint**|Determina o tipo de execução da consulta:<br /><br /> 0 - execução regular (concluída com êxito)<br /><br /> 3 - cliente iniciado anulou a execução<br /><br /> 4 - exceção anulou a execução|  
|**execution_type_desc**|**nvarchar(128)**|Descrição textual do campo de tipo de execução:<br /><br /> 0 - regular<br /><br /> 3 - anulada<br /><br /> 4 - exceção|  
|**first_execution_time**|**datetimeoffset**|Primeiro tempo de execução para o plano de consulta dentro do intervalo de agregação. Isso se refere à hora de término da execução da consulta.|  
|**last_execution_time**|**datetimeoffset**|Último tempo de execução para a consulta planejar dentro do intervalo de agregação. Isso se refere à hora de término da execução da consulta.|  
|**count_executions**|**bigint**|Contagem total de execuções do plano de consulta dentro do intervalo de agregação.|  
|**avg_duration**|**float**|Média de duração para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**last_duration**|**bigint**|Duração da consulta do último plano dentro do intervalo de agregação (relatado em microssegundos).|  
|**min_duration**|**bigint**|Duração mínima para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**max_duration**|**bigint**|Duração máxima para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**stdev_duration**|**float**|Desvio padrão de duração para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).|  
|**avg_cpu_time**|**float**|Tempo médio de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_cpu_time**|**bigint**|Último tempo de CPU para a consulta planejar dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_cpu_time**|**bigint**|Tempo mínimo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_cpu_time**|**bigint**|Tempo máximo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_cpu_time**|**float**|Desvio de padrão de tempo de CPU para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_logical_io_reads**|**float**|Lê o número médio de e/s lógica para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_logical_io_reads**|**bigint**|Último número de e/s lógicas lê para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_logical_io_reads**|**bigint**|Lê o número mínimo de e/s lógica para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_logical_io_reads**|**bigint**|Lê o número máximo de e/s lógica para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_logical_io_reads**|**float**|Número de e/s lógicas lê o desvio padrão para o plano de consulta dentro do intervalo de agregação. (expresso como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_logical_io_writes**|**float**|Número médio de e/s lógicas grava para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_logical_io_writes**|**bigint**|Último número de e/s lógicas grava para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_logical_io_writes**|**bigint**|Número mínimo de e/s lógicas grava para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_logical_io_writes**|**bigint**|Número máximo de e/s lógicas grava para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_logical_io_writes**|**float**|Número de e/s lógicas grava o desvio padrão para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_physical_io_reads**|**float**|Lê o número médio de e/s física para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_physical_io_reads**|**bigint**|Último número de e/s física lê para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_physical_io_reads**|**bigint**|Lê o número mínimo de e/s física para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_physical_io_reads**|**bigint**|Lê o número máximo de e/s física para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_physical_io_reads**|**float**|Número de e/s física lê o desvio padrão para o plano de consulta dentro do intervalo de agregação (expressado como um número de páginas de 8KB de leitura).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_clr_time**|**float**|Tempo médio de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_clr_time**|**bigint**|Última hora CLR para a consulta planejar dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_clr_time**|**bigint**|Tempo mínimo de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_clr_time**|**bigint**|Tempo máximo de CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_clr_time**|**float**|Desvio do padrão de tempo do CLR para o plano de consulta dentro do intervalo de agregação (relatado em microssegundos).<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_dop**|**float**|Média DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_dop**|**bigint**|Último DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_dop**|**bigint**|Mínimo DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_dop**|**bigint**|Máximo DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_dop**|**float**|Desvio padrão DOP (grau de paralelismo) para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_query_max_used_memory**|**float**|Concessão de memória média (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_query_max_used_memory**|**bigint**|Última concessão de memória (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_query_max_used_memory**|**bigint**|Concessão de memória mínima (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_query_max_used_memory**|**bigint**|Concessão máxima de memória (relatado como o número de páginas de 8 KB) para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_query_max_used_memory**|**float**|Desvio padrão (relatado como o número de páginas de 8 KB) de concessão de memória para o plano de consulta dentro do intervalo de agregação. Sempre 0 para consultas que usam nativamente compilado procedimentos com otimização de memória.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**avg_rowcount**|**float**|Número médio de linhas retornadas para o plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_rowcount**|**bigint**|Número de linhas retornadas pela última execução do plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_rowcount**|**bigint**|Número mínimo de linhas retornadas para a consulta planejar dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_rowcount**|**bigint**|Número máximo de linhas retornadas para a consulta planejar dentro do intervalo de agregação.|  
|**stdev_rowcount**|**float**|Número de desvio padrão de linhas retornadas para o plano de consulta dentro do intervalo de agregação.|
|**avg_log_bytes_used**|**float**|Número médio de bytes no log do banco de dados usadas pelo plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**last_log_bytes_used**|**bigint**|Número de bytes no log do banco de dados usado pela última execução do plano de consulta, dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**min_log_bytes_used**|**bigint**|Número mínimo de bytes no log do banco de dados usadas pelo plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**max_log_bytes_used**|**bigint**|Número máximo de bytes no log do banco de dados usadas pelo plano de consulta dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
|**stdev_log_bytes_used**|**float**|Desvio padrão do número de bytes no log do banco de dados usado por um plano de consulta, dentro do intervalo de agregação.<br/>**Observação:** SQL Data Warehouse do Azure sempre retornará zero (0).|
  
## <a name="permissions"></a>Permissões  
 Requer o **VIEW DATABASE STATE** permissão.  
  
## <a name="see-also"></a>Consulte também  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimentos armazenados de Store de consulta &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
