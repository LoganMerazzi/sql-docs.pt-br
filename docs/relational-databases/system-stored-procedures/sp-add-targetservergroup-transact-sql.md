---
title: sp_add_targetservergroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_targetservergroup
- sp_add_targetservergroup_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_targetservergroup
ms.assetid: acb69343-d766-46ff-b771-0c7655c5231a
author: stevestein
ms.author: sstein
ms.openlocfilehash: c268c356e41c957349f452d2f83fc4b807042d9e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990503"
---
# <a name="spaddtargetservergroup-transact-sql"></a>sp_add_targetservergroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona o grupo de servidor especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_targetservergroup [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` O nome do grupo de servidores para criar. *nome da* está **sysname**, sem padrão. *nome* não pode conter vírgulas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Os grupos de servidores de destino fornecem uma maneira fácil de direcionar um trabalho a uma coleção de servidores de destino. Para obter mais informações, consulte [sp_apply_job_to_targets](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função fixa de servidor pode executar este procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria o grupo de servidor de destino chamado `Servers Processing Customer Orders`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_targetservergroup  
    'Servers Processing Customer Orders' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_apply_job_to_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_help_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
