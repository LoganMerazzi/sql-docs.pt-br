---
title: sys.registered_search_property_lists (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- registered_search_property_lists_TSQL
- sys.registered_search_property_lists
- registered_search_property_lists
- sys.registered_search_property_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- sys.registered_search_property_lists catalog view
- search property lists [SQL Server], viewing
ms.assetid: 630d4caa-9bea-4cd3-a5b1-01098b0855fc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 89636150a5925d3f1d2c77d0462666d369492010
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/30/2019
ms.locfileid: "64946500"
---
# <a name="sysregisteredsearchpropertylists-transact-sql"></a>sys.registered_search_property_lists (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada lista de propriedades de pesquisa no banco de dados atual.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|ID da lista de propriedades.|  
|**name**|**sysname**|O nome da lista de propriedades.|  
|**create_date**|**datetime**|A data em que a lista de propriedades foi criada.|  
|**modify_date**|**datetime**|A data da última modificação da lista de propriedades por uma instrução ALTER.|  
|**principal_id**|**int**|O proprietário da lista de propriedades.|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="permissions"></a>Permissões  
 A visibilidade dos metadados nas listas de propriedades de pesquisa é limitada aos metadados que estão em listas de propriedades de pesquisa de sua propriedade ou nas quais você recebeu a permissão REFERENCE.  
  
> [!NOTE]  
>  O proprietário da lista de propriedades de pesquisa pode conceder as permissões REFERENCE ou CONTROL na lista. Usuários com permissão CONTROL também podem conceder a permissão REFERENCE a outros usuários.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe a ID e o nome das listas de propriedades de pesquisa no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT property_list_id, name FROM sys.registered_search_property_lists;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
  
