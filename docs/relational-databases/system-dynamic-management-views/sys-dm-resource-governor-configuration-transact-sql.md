---
title: DM resource_governor_configuration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_resource_governor_configuration_TSQL
- dm_resource_governor_configuration
- sys.dm_resource_governor_configuration
- sys.dm_resource_governor_configuration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_configuration dynamic management view
ms.assetid: c89aab6a-0434-4ce6-af8c-f8a1a3284e38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 00b425e5efd441868bfa763fe544827bd7279dc2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067796"
---
# <a name="sysdmresourcegovernorconfiguration-transact-sql"></a>sys.dm_resource_governor_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha que contém o estado de configuração na memória atual do Administrador de recursos.  
  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|ID da função de classificador atualmente usado pelo Administrador de recursos. Retornará um valor de 0 se nenhuma função estiver sendo usada. Não permite valor nulo.<br /><br /> **Observação:** Essa função é usada para classificar novas solicitações e usa regras para encaminhar essas solicitações para o grupo de carga de trabalho adequado. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).|  
|is_reconfiguration_pending|**bit**|Indica se foram ou não feitas alterações em um pool ou em um grupo com a instrução ALTER RESOURCE GOVERNOR RECONFIGURE e se elas não foram aplicadas à configuração na memória. O valor retornado pode ser um dos seguintes:<br /><br /> 0 - Uma instrução de reconfiguração não é necessária.<br /><br /> 1 - Uma instrução de reconfiguração ou reinicialização de servidor é necessária para que as alterações de configuração pendentes sejam aplicadas.<br /><br /> **Observação:** O valor retornado é sempre 0 quando o administrador de recursos está desabilitado.<br /><br /> Não permite valor nulo.|  
|max_outstanding_io_per_volume|**int**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> O número máximo de E/S pendente por volume.|  
  
## <a name="remarks"></a>Comentários  
 Essa exibição de gerenciamento dinâmico mostra a configuração na memória. Para verificar os metadados de configuração armazenados, use a exibição do catálogo correspondente.  
  
 O exemplo a seguir mostra como obter e comparar os valores de metadados armazenados e os valores na memória da configuração do Administrador de recursos.  
  
```  
USE master;  
go  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
go  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
go  
```  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-configuration-transact-sql.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  

