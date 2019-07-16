---
title: sp_server_diagnostics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_server_diagnostics
- sp_server_diagnostics_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_server_diagnostics
ms.assetid: 62658017-d089-459c-9492-c51e28f60efe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 30ea7fba212cc99b8d6d7e58397d29731048c6f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056303"
---
# <a name="spserverdiagnostics-transact-sql"></a>sp_server_diagnostics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Captura dados de diagnóstico e informações de integridade sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para detectar falhas potenciais. O procedimento é executado no modo de repetição e envia resultados periodicamente. Pode ser invocado a partir de uma conexão comum ou DAC.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_server_diagnostics [@repeat_interval =] 'repeat_interval_in_seconds'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @repeat_interval = ] 'repeat_interval_in_seconds'` Indica o intervalo de tempo em que o procedimento armazenado será executado repetidamente para enviar informações de integridade.  
  
 *repeat_interval_in_seconds* está **int** com o padrão de 0. Os valores de parâmetros válidos são 0 ou qualquer valor igual ou superior a 5. O procedimento armazenado deve ser executado por pelo menos 5 segundos para retornar dados completos. O valor mínimo de execução do procedimento armazenado no modo de repetição é de 5 segundos.  
  
 Se esse parâmetro não for especificado ou se o valor especificado for 0, o procedimento armazenado retornará dados uma vez e depois será encerrado.  
  
 Se o valor especificado for menor do que o valor mínimo, isso gerará um erro e não retornará nada.  
  
 Se o valor especificado for igual ou maior que 5, o procedimento armazenado será executado repetidamente para retornar o estado de integridade até que seja manualmente cancelado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
**sp_server_diagnostics** retorna as informações a seguir  
  
|coluna|Data type|Descrição|  
|------------|---------------|-----------------|  
|**creation_time**|**datetime**|Indica o carimbo de data/hora de criação de linha. Cada linha em um único conjunto de linhas tem o mesmo carimbo de data/hora.|  
|**component_type**|**sysname**|Indica se a linha contém informações para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nível de componente ou para um grupo de disponibilidade Always On da instância:<br /><br /> instância<br /><br /> AlwaysOn: AvailabilityGroup|  
|**component_name**|**sysname**|Indica o nome de componente ou o nome do grupo de disponibilidade:<br /><br /> sistema<br /><br /> resource<br /><br /> query_processing<br /><br /> io_subsystem<br /><br /> eventos<br /><br /> *\<nome do grupo de disponibilidade >*|  
|**state**|**int**|Indica o status de integridade do componente:<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> 3|  
|**state_desc**|**sysname**|Descreve a coluna de estado. Descrições que correspondem aos valores na coluna de estado são:<br /><br /> 0: Unknown<br /><br /> 1: limpar<br /><br /> 2: aviso<br /><br /> 3: erro|  
|**data**|**varchar (max)**|Especifica dados que são específicos do componente.|  
  
 Aqui estão as descrições dos cinco componentes:  
  
-   **sistema**: Coleta dados de uma perspectiva do sistema em spinlocks, condições de processamento severas, tarefas não produzidas, falhas de página e uso da CPU. Essas informações produzem uma recomendação de estado de integridade geral.  
  
-   **recurso**:  Coleta dados de uma perspectiva de recurso na memória física e virtual, pools de buffers, páginas, cache e outros objetos de memória. Essas informações produz uma recomendação de estado de integridade geral.  
  
-   **query_processing**: Coleta dados de uma perspectiva de processamento de consulta em threads de trabalho, tarefas, tipos de espera, sessões intensivas de CPU e tarefas de bloqueio. Essas informações produz uma recomendação de estado de integridade geral.  
  
-   **io_subsystem**: Coleta dados sobre e/s. Além dos dados de diagnóstico, esse componente produz um estado de integridade limpo ou de integridade de aviso somente para um subsistema de IO.  
  
-   **Eventos**: Coleta de dados e superfícies por meio do procedimento armazenado nos erros e eventos interessantes registrados pelo servidor, incluindo detalhes sobre exceções de buffer de anel, eventos de buffer de anel sobre agente de memória, fora de memória, monitor do Agendador, pool de buffer, spinlocks, segurança e conectividade. Eventos sempre mostrarão 0 como o estado.  
  
-   **\<nome do grupo de disponibilidade >** : Coleta dados para o grupo de disponibilidade especificado (se component_type = "sempre em: AvailabilityGroup").  
  
## <a name="remarks"></a>Comentários  
De uma perspectiva de falha, os componentes system, resource e query_processing serão aproveitados para detecção de falha, enquanto os componentes io_subsystem e eventos serão aproveitados apenas para fins de diagnóstico.  
  
A tabela a seguir mapeia os componentes para seus estados de integridade associados.  
  
|Componentes|Clean (1)|Warning (2)|Erro (3)|Unknowns (0)|  
|----------------|-----------------|-------------------|-----------------|--------------------|  
|sistema|x|x|x||  
|resource|x|x|x||  
|query_processing|x|x|x||  
|io_subsystem|x|x|||  
|eventos||||x|  
  
O (x) em cada linha representa estados de integridade válida para o componente. Por exemplo, io_subsystem mostrará como clean ou warning. Não mostrará os estados de erro.  
 
> [!NOTE]
> Execução do procedimento de sp_server_diagnostics interno é implementada em um thread preemptive com prioridade alta.
  
## <a name="permissions"></a>Permissões  
, é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
É prática recomendada usar sessões estendidas para capturar as informações de integridade e salvá-las em um arquivo localizado fora do SQL Server. Portanto, ainda será possível acessar isso em caso de falha. O exemplo a seguir salva a saída de uma sessão de evento em um arquivo:  
```sql  
CREATE EVENT SESSION [diag]  
ON SERVER  
           ADD EVENT [sp_server_diagnostics_component_result] (set collect_data=1)  
           ADD TARGET [asynchronous_file_target] (set filename='c:\temp\diag.xel');  
GO  
ALTER EVENT SESSION [diag]  
      ON SERVER STATE = start;  
GO  
```  
  
A consulta de exemplo abaixo lê o arquivo de log de sessão estendida:  
```sql  
SELECT  
    xml_data.value('(/event/@name)[1]','varchar(max)') AS Name  
  , xml_data.value('(/event/@package)[1]', 'varchar(max)') AS Package  
  , xml_data.value('(/event/@timestamp)[1]', 'datetime') AS 'Time'  
  , xml_data.value('(/event/data[@name=''component_type'']/value)[1]','sysname') AS Sysname  
  , xml_data.value('(/event/data[@name=''component_name'']/value)[1]','sysname') AS Component  
  , xml_data.value('(/event/data[@name=''state'']/value)[1]','int') AS State  
  , xml_data.value('(/event/data[@name=''state_desc'']/value)[1]','sysname') AS State_desc  
  , xml_data.query('(/event/data[@name="data"]/value/*)') AS Data  
FROM   
(  
      SELECT  
                        object_name as event  
                        ,CONVERT(xml, event_data) as xml_data  
       FROM    
      sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\*.xel', NULL, NULL, NULL)  
)   
AS XEventData  
ORDER BY time;  
```  
  
O exemplo a seguir captura a saída de sp_server_diagnostics para uma tabela em um modo de não repetição:  
```sql  
CREATE TABLE SpServerDiagnosticsResult  
(  
      create_time DateTime,  
      component_type sysname,  
      component_name sysname,  
      state int,  
      state_desc sysname,  
      data xml  
);  
INSERT INTO SpServerDiagnosticsResult  
EXEC sp_server_diagnostics; 
```  

A consulta de exemplo abaixo lê a saída de resumo da tabela:  
```sql  
SELECT create_time,
       component_name,
       state_desc 
FROM SpServerDiagnosticsResult;  
``` 

A consulta de exemplo abaixo lê algumas das saídas detalhadas de cada componente na tabela:  
```sql  
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult 
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult 
where component_name like 'resource'
go

-- Nonpreemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/nonPreemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- Preemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/preemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- CPU intensive requests
select cpureq.evt.value('(@sessionId)','bigint') as 'SessionID',
   cpureq.evt.value('(@command)','varchar(100)') as 'Command',
   cpureq.evt.value('(@cpuUtilization)','bigint') as 'CPU_Utilization',
   cpureq.evt.value('(@cpuTimeMs)','bigint') as 'CPU_Time_ms'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/cpuIntensiveRequests/request') AS cpureq(evt)
where component_name like 'query_processing'
go

-- Blocked Process Report
select blk.evt.query('.') as 'Blocked_Process_Report_XML'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/blockingTasks/blocked-process-report') AS blk(evt)
where component_name like 'query_processing'
go

-- IO
select data.value('(/ioSubsystem/@ioLatchTimeouts)[1]','bigint') as 'Latch_Timeouts',
   data.value('(/ioSubsystem/@totalLongIos)[1]','bigint') as 'Total_Long_IOs'
from SpServerDiagnosticsResult 
where component_name like 'io_subsystem'
go

-- Event information
select xevts.evt.value('(@name)','varchar(100)') as 'xEvent_Name',
   xevts.evt.value('(@package)','varchar(100)') as 'Package',
   xevts.evt.value('(@timestamp)','datetime') as 'xEvent_Time',
   xevts.evt.query('.') as 'Event Data'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/events/session/RingBufferTarget/event') AS xevts(evt)
where component_name like 'events'
go  
``` 
  
## <a name="see-also"></a>Consulte também  
 [Política de failover para instâncias de cluster de failover](../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
