---
title: sys.system_views (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.system_views_TSQL
- system_views
- system_views_TSQL
- sys.system_views
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_views catalog view
ms.assetid: a526c410-e7b5-4075-8103-e1f3c6837c3c
author: stevestein
ms.author: sstein
ms.openlocfilehash: fce2816d8cb169c5761f47dd0f9dd0a6ed1959f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078611"
---
# <a name="syssystemviews-transact-sql"></a>sys.system_views (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada exibição de sistema que é incluída no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Todas as exibições do sistema estão contidas nos esquemas chamados **sys** ou **INFORMATION_SCHEMA**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|\<herdado colunas >||Para obter uma lista de colunas que essa exibição herda valores, consulte [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_replicated**|**bit**|1 = A exibição é replicada.|  
|**has_replication_filter**|**bit**|1 = A exibição tem um filtro de replicação.|  
|**has_opaque_metadata**|**bit**|1 = A opção VIEW_METADATA especificada para exibição. Para obter mais informações, veja [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).|  
|**has_unchecked_assembly_data**|**bit**|1 = A tabela contém dados persistentes que dependem de um assembly cuja definição foi alterada durante o último ALTER ASSEMBLY. Será redefinida como 0 depois do próximo DBCC CHECKDB ou DBCC CHECKTABLE bem-sucedido.|  
|**with_check_option**|**bit**|1 = WITH CHECK OPTION foi especificado na definição de exibição.|  
|**is_date_correlation_view**|**bit**|1 = exibição foi criada automaticamente pelo sistema para armazenar informações de correlação entre **datetime** colunas. A criação dessa exibição foi habilitada ao definir DATE_CORRELATION_OPTIMIZATION como ON.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
