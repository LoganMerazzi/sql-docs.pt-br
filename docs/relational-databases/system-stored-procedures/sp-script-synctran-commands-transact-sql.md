---
title: sp_script_synctran_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
author: stevestein
ms.author: sstein
ms.openlocfilehash: d7caca72f684dfb6428361a4550860b3bea3f273
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126406"
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera um script que contém o **sp_addsynctrigger** chamadas para serem aplicadas nos assinantes para assinaturas atualizáveis. Há um **sp_addsynctrigger** chamar para cada artigo na publicação. O script gerado também contém o **sp_addqueued_artinfo** chamadas que cria a **MSsubsciption_articles** tabela que é necessário para processar publicações enfileiradas. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação a ser inserido no script. *publicação* está **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo a ser inserido no script. *artigo* está **sysname**, com um padrão de **todos os**, que especifica todos os artigos são incluídos no script.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="results-set"></a>Conjunto de resultados  
 **sp_script_synctran_commands** retorna um conjunto de resultados que consiste em uma única **nvarchar (4000)** coluna. O conjunto de resultados forma os scripts completos necessários para criar as a **sp_addsynctrigger** e **sp_addqueued_artinfo** chamadas para serem aplicadas nos assinantes.  
  
## <a name="remarks"></a>Comentários  
 **sp_script_synctran_commands** é usado em replicação de instantâneo e transacional.  
  
 **sp_addqueued_artinfo** é usado para assinaturas atualizáveis enfileiradas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_script_synctran_commands**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addsynctriggers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
