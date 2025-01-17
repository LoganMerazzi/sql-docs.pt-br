---
title: Configurar uma política de failover automático flexível para um grupo de disponibilidade
description: Descreve como configurar uma política de failover flexível para um Grupo de Disponibilidade AlwaysOn usando o T-SQL (Transact-SQL), o PowerShell ou o SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 1ed564b4-9835-4245-ae35-9ba67419a4ce
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 31968f84f6cfaad42d2f3c049a2213a60a66ffbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988496"
---
# <a name="configure-a-flexible-automatic-failover-policy-for-an-always-on-availability-group"></a>Configurar uma política de failover automático flexível para um Grupo de Disponibilidade AlwaysOn

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como configurar a política de failover flexível para um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Uma política de failover flexível fornece o controle granular das condições que causam um failover automático para um grupo de disponibilidade. Ao alterar as condições de falha que disparam um failover automático e a frequência de verificações de integridade, você pode aumentar ou diminuir a probabilidade de um failover automático para oferecer suporte ao seu SLA para alta disponibilidade.  
 
    > [!NOTE]  
    >  The flexible failover policy of an availability group cannot be configured by using [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 
## <a name="Limitations"></a> Limitações sobre failovers automáticos  
  
-   Para que um failover automático ocorra, a réplica primária e uma réplica secundária deverão ser configuradas para o modo de disponibilidade de confirmação síncrona com failover automático e a réplica secundária deverá ser sincronizada com a réplica primária.  
  
-   Apenas três réplicas têm suporte para o failover automático.  
  
-   Se um grupo de disponibilidade exceder seu limite de falha do WSFC, o cluster do WSFC não tentará um failover automático para o grupo de disponibilidade. Além disso, o grupo de recursos do WSFC do grupo de disponibilidade permanece em um estado com falha até o administrador de cluster manualmente colocar online o grupo de recursos com falha ou o administrador de banco de dados executar um failover manual do grupo de disponibilidade. O *limite de falha do WSFC* é definido como o número máximo de falhas com suporte para o grupo de disponibilidade durante um determinado período de tempo. O período padrão é de seis horas e o valor padrão para o número máximo de falhas durante este período é *n*-1, em que *n* é o número de nós do WSFC. Para alterar os valores do limite de failover para um determinado grupo de disponibilidade, use o Console de Gerenciador de Failover WSFC.  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
   
##  <a name="Permissions"></a> Permissões  
  
|Tarefa|Permissões|  
|----------|-----------------|  
|Para configurar a política de failover flexível para um novo grupo de disponibilidade|Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
|Para modificar a política de um grupo de disponibilidade existente|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para configurar a política de failover flexível**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Para um novo grupo de disponibilidade, use a instrução [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Se você estiver modificando um grupo de disponibilidade existente, use a instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Para definir o nível de condição de failover, use a opção FAILURE_CONDITION_LEVEL = *n* , em que *n* é um número inteiro de 1 a 5.  
  
         Por exemplo, a instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir altera o nível da condição de falha de um grupo de disponibilidade existente, `AG1`, para o nível um:  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1);  
        ```  
  
         A relação destes valores inteiros para os níveis de condição de falha é a seguinte:  
  
        |[!INCLUDE[tsql](../../../includes/tsql-md.md)] Valor|Nível|Automático é o failover iniciado em caso de...|  
        |------------------------------|-----------|-------------------------------------------|  
        |1|Um|Em servidor inativo. O serviço SQL Server é interrompido devido a um failover ou a uma reinicialização.|  
        |2|Dois|Em servidor sem resposta. Qualquer condição de valor inferior é atendida, o serviço SQL Server está conectado ao cluster e o tempo limite de verificação de integridade é excedido, ou a réplica primária atual está em um estado de falha.|  
        |3|Três|Em erros críticos do servidor. Qualquer condição de valor inferior é atendida ou há um erro crítico de servidor interno.<br /><br /> Este é o nível padrão.|  
        |4|Quatro|Em erros moderados do servidor. Qualquer condição de valor inferior é atendida ou há um erro moderado de servidor.|  
        |5|Cinco|Em qualquer condição de falha qualificada. Qualquer condição de valor inferior é atendida ou há uma condição de falha qualificada.|  
  
         Para obter mais informações sobre os níveis de condição de failover, consulte [Política de failover flexível para failover automático de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
    -   Para configurar o tempo limite de verificação de integridade, use a opção HEALTH_CHECK_TIMEOUT = *n*, em que *n* é um número inteiro de 15000 milissegundos (15 segundos) a 4294967295 milissegundos. O valor padrão é 30000 milissegundos (30 segundos).  
  
         Por exemplo, a instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir altera o limite de tempo limite de verificação de integridade de um grupo de disponibilidade existente, `AG1`, para 60.000 milissegundos (um minuto).  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT = 60000);  
        ```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para configurar a política de failover flexível**  
  
1.  Defina o padrão (**cd**) como a instância de servidor que hospeda a réplica primária.  
  
2.  Ao adicionar uma réplica de disponibilidade a um grupo de disponibilidade, use o cmdlet **New-SqlAvailabilityGroup** . Ao modificar uma réplica de disponibilidade existente, use o cmdlet **Set-SqlAvailabilityGroup** .  
  
    -   Para definir o nível de condição de failover, use o parâmetro **FailureConditionLevel**_level_ , onde *level* é um dos seguintes valores:  
  
        |Valor|Nível|Automático é o failover iniciado em caso de...|  
        |-----------|-----------|-------------------------------------------|  
        |**OnServerDown**|Um|Em servidor inativo. O serviço SQL Server é interrompido devido a um failover ou a uma reinicialização.|  
        |**OnServerUnresponsive**|Dois|Em servidor sem resposta. Qualquer condição de valor inferior é atendida, o serviço SQL Server está conectado ao cluster e o tempo limite de verificação de integridade é excedido, ou a réplica primária atual está em um estado de falha.|  
        |**OnCriticalServerError**|Três|Em erros críticos do servidor. Qualquer condição de valor inferior é atendida ou há um erro crítico de servidor interno.<br /><br /> Este é o nível padrão.|  
        |**OnModerateServerError**|Quatro|Em erros moderados do servidor. Qualquer condição de valor inferior é atendida ou há um erro moderado de servidor.|  
        |**OnAnyQualifiedFailureConditions**|Cinco|Em qualquer condição de falha qualificada. Qualquer condição de valor inferior é atendida ou há uma condição de falha qualificada.|  
  
         Para obter mais informações sobre os níveis de condição de failover, consulte [Política de failover flexível para failover automático de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
         Por exemplo, o comando a seguir altera o nível da condição de falha de um grupo de disponibilidade existente, `AG1`, para o nível um.  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `   
        -FailureConditionLevel OnServerDown  
        ```  
  
    -   Para definir o tempo limite de verificação de integridade, use o parâmetro **HealthCheckTimeout**_n_ , em que *n* é um número inteiro de 15000 milissegundos (15 segundos) a 4294967295 milissegundos. O valor padrão é 30000 milissegundos (30 segundos).  
  
         Por exemplo, o comando a seguir altera o tempo limite de verificação de integridade de um grupo de disponibilidade existente, `AG1`, para 120.000 milissegundos (dois minutos).  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
        -HealthCheckTimeout 120000  
        ```  
  
> [!NOTE]  
>  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Failover e modos de failover &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Política de failover para instâncias de cluster de failover](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)  
  
  
