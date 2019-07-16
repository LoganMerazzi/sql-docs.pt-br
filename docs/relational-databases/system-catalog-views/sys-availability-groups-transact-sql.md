---
title: sys. availability_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_TSQL
- availability_groups_TSQL
- sys.availability_groups
- availability_groups
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups catalog view
ms.assetid: da7fa55f-c008-45d9-bcfc-3513b02d9e71
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b6992cceb19d0fe39c1e53e36535949a94907295
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942650"
---
# <a name="sysavailabilitygroups-transact-sql"></a>sys.availability_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada grupo de disponibilidade para o qual a instância local do SQL Server hospeda uma réplica de disponibilidade. Cada linha contém uma cópia armazenada em cache dos metadados do grupo de disponibilidade.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|GUID (identificador exclusivo) do grupo de disponibilidade.|  
|**name**|**sysname**|O nome do grupo de disponibilidade. Esse é um nome especificado pelo usuário que deve ser exclusivo no WSFC (Windows Server Failover Cluster).|  
|**resource_id**|**nvarchar(40)**|ID de recurso do recurso de cluster WSFC.|  
|**resource_group_id**|**nvarchar(40)**|ID do grupo de recursos do cluster WSFC do grupo de disponibilidade.|  
|**failure_condition_level**|**int**|Falha definido pelo usuário nível de condição sob a qual um failover automático deve ser disparado, um dos valores de inteiro, mostrados na tabela imediatamente abaixo desta tabela.<br /><br /> Os níveis da condição de falha (1 a 5) variam do menos restritivo, nível 1, até o mais restritivo, nível 5. Um determinado nível de condição abrange todos os níveis menos restritivos. Assim, o nível de condição mais rígido, 5, inclui os quatro níveis de condição menos restritivos (1 a 4), o nível 4 inclui os níveis 1 a 3 e assim sucessivamente.<br /><br /> Para alterar esse valor, use a opção FAILURE_CONDITION_LEVEL dos [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.|  
|**health_check_timeout**|**int**|Tempo de espera (em milissegundos) para o [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) sistema de procedimento armazenado para retornar informações de integridade do servidor, antes da instância do servidor é considerada lenta ou travada. O valor padrão é 30000 milissegundos (30 segundos).<br /><br /> Para alterar esse valor, use a opção HEALTH_CHECK_TIMEOUT dos [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.|  
|**automated_backup_preference**|**tinyint**|Local preferido para executar backups nos bancos de dados de disponibilidade nesse grupo de disponibilidade. A seguir estão os valores possíveis e suas descrições.<br /><br /> <br /><br /> 0 : Primário. Backups sempre devem ocorrer na réplica primária.<br /><br /> 1 : Somente secundária. A execução de backups em uma réplica secundária é preferível.<br /><br /> 2 : Preferir secundária. A execução de backups em uma réplica secundária é preferível, mas a execução de backups na réplica primária será aceitável se nenhuma réplica secundária estiver disponível para operações de backup. Esse é o comportamento padrão.<br /><br /> 3 : Qualquer réplica. Nenhuma preferência sobre se os backups são executados na réplica primária ou em uma réplica secundária.<br /><br /> <br /><br /> Para obter mais informações, confira [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**automated_backup_preference_desc**|**nvarchar(60)**|Descrição da **automated_backup_preference**, um de:<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> Nenhuma|  
|**version**|**smallint**|A versão dos metadados do grupo de disponibilidade armazenado no Cluster de Failover do Windows. Esse número de versão é incrementado quando novos recursos são adicionados.|  
|**basic_features**|**bit**|Especifica se este é um grupo de disponibilidade básica. Para obter mais informações, consulte [Grupos de disponibilidade básicos &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).|  
|**dtc_support**|**bit**|Especifica se o suporte DTC foi habilitado para este grupo de disponibilidade. O **DTC_SUPPORT** opção de **CREATE AVAILABILITY GROUP** controla essa configuração.|  
|**db_failover**|**bit**|Especifica se o grupo de disponibilidade dá suporte a failover para condições de integridade do banco de dados. O **DB_FAILOVER** opção de **CREATE AVAILABILITY GROUP** controla essa configuração.|  
|**is_distributed**|**bit**|Especifica se este é um grupo de disponibilidade distribuído. Para obter mais informações, veja [Grupos de disponibilidade distribuídos e &#40;Grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md).|  
  
## <a name="failure-condition-level--values"></a>Valores de nível de condição de falha  
 A tabela a seguir descreve os níveis de condição de falha possíveis para o **failure_condition_level** coluna.  
  
|Valor|Condição de falha|  
|-----------|-----------------------|  
|1|Especifica que um failover automático deverá ser iniciado quando uma destas condições ocorrer:<br /><br /> <br /><br /> -O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço está inativo.<br /><br /> -A concessão do grupo de disponibilidade para se conectar ao cluster de failover WSFC expira porque nenhum ACK foi recebido da instância de servidor. Para obter mais informações, confira [Como funciona: Tempo limite de concessão do Always On do SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).|  
|2|Especifica que um failover automático deverá ser iniciado quando uma destas condições ocorrer:<br /><br /> <br /><br /> -A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não se conectar ao cluster e o usuário especificou **health_check_timeout** limite do grupo de disponibilidade é excedido.<br /><br /> -A réplica de disponibilidade está em estado de falha.|  
|3|Especifica que um failover automático deve ser iniciado em erros internos críticos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como spinlocks órfãos, violações do acesso de gravação graves ou muito descarte.<br /><br /> Este é o valor padrão.|  
|4|Especifica que um failover automático deve ser iniciado em caso de erros internos moderados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como uma condição de memória insuficiente persistente no pool de recursos interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|5|Especifica que um failover automático deve ser iniciado em qualquer condição de falha qualificada, incluindo:<br /><br /> <br /><br /> -Esgotamento dos threads de trabalho do SQL Engine.<br /><br /> -Detecção de um deadlock insolúvel.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION na instância de servidor.  
  
## <a name="see-also"></a>Consulte também  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
