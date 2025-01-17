---
title: sp_helpmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergefilter
- sp_helpmergefilter_TSQL
helpviewer_keywords:
- sp_helpmergefilter
ms.assetid: f133a094-0009-4771-b93b-e86a5c01e40b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5a743b03d379276e6842b72e44d346cc1356cf7a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137694"
---
# <a name="sphelpmergefilter-transact-sql"></a>sp_helpmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre filtros de mesclagem. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergefilter [ @publication= ] 'publication'   
    [ , [ @article= ] 'article']  
    [ , [ @filtername= ] 'filtername']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo. *artigo* está **sysname**, com um padrão de **%** , que retorna os nomes de todos os artigos.  
  
`[ @filtername = ] 'filtername'` É o nome do filtro sobre o qual retornar informações. *FilterName* está **sysname**, com um padrão de **%** , que retorna informações sobre todos os filtros definidos em um artigo ou publicação.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**join_filterid**|**int**|ID do filtro de junção.|  
|**FilterName**|**sysname**|Nome do filtro.|  
|**nome do artigo**|**sysname**|Nome do artigo de junção.|  
|**join_filterclause**|**nvarchar(2000)**|Cláusula de filtro que qualifica a junção.|  
|**join_unique_key**|**int**|Se a junção está em uma chave exclusiva.|  
|**proprietário da tabela base**|**sysname**|Nome do proprietário da tabela base.|  
|**nome da tabela base**|**sysname**|Nome da tabela base.|  
|**proprietário da tabela de junção**|**sysname**|Nome do proprietário da tabela que é adicionada à tabela base.|  
|**nome da tabela de junção**|**sysname**|Nome da tabela que é adicionada à tabela base.|  
|**nome do artigo**|**sysname**|Nome do artigo de tabela que é adicionado à tabela base.|  
|**filter_type**|**tinyint**|Tipo de filtro de mesclagem, que pode ser um dos seguintes:<br /><br /> **1** = somente filtro de junção<br /><br /> **2** = relação de registro lógico<br /><br /> **3** = ambos|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergefilter** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa e a **db_owner** banco de dados fixa podem executar **sp_helpmergefilter**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
