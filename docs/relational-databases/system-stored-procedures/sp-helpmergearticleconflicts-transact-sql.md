---
title: sp_helpmergearticleconflicts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 85e75e1ce52866eb04b3c410f021db8de392239a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122332"
---
# <a name="sphelpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os artigos na publicação que tem conflitos. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação ou no Assinante, no banco de dados de assinatura de mesclagem.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação de mesclagem. *publicação* é **sysname**, com um padrão de **%** , que retorna todos os artigos no banco de dados que tem conflitos.  
  
`[ @publisher = ] 'publisher'` É o nome do publicador. *publisher* é **sysname**, com um padrão NULL.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados publicador. *publisher_db* é **sysname**, com um padrão NULL.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**article**|**sysname**|Nome do artigo.|  
|**source_owner**|**sysname**|Proprietário do objeto de origem.|  
|**source_object**|**nvarchar(386)**|Nome do objeto de origem.|  
|**conflict_table**|**nvarchar(258)**|Nome da tabela que armazena os conflitos de entrada ou atualização.|  
|**guidcolname**|**sysname**|Nome do RowGuidCol para o objeto de origem.|  
|**centralized_conflicts**|**int**|Se os registros de conflito são armazenados no Publicador determinado.|  
  
 Se o artigo tiver somente conflitos excluídos e nenhuma **conflict_table** linhas, o nome da **conflict_table** no resultado do conjunto é NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergearticleconflicts** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa e a **db_owner** banco de dados fixa podem executar **sp_helpmergearticleconflicts**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
