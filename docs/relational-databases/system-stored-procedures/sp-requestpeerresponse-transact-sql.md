---
title: sp_requestpeerresponse (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords:
- sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
author: stevestein
ms.author: sstein
ms.openlocfilehash: f8d75b208cc91d52d20fb4e94340809cd6857fa1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129726"
---
# <a name="sprequestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quando executado de um nó em uma topologia ponto a ponto, esse procedimento solicita uma resposta de todos os outros nós na topologia. Ao executar esse procedimento e analisar as respostas correspondentes, você garante que todos os comandos anteriores sejam entregues aos nós respondentes. Esse procedimento armazenado é executado no nó de solicitação, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_requestpeerresponse [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
    [ , [ @request_id = ] request_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação em uma topologia ponto a ponto para o qual o status está sendo verificado. *publicação* está **sysname**, sem padrão.  
  
`[ @description = ] 'description'` Informações definidas pelo usuário que podem ser usadas para identificar solicitações de status individuais. *Descrição* está **nvarchar (4000)** , com um padrão NULL.  
  
`[ @request_id = ] request_id` Retorna a ID da nova solicitação. *request_id* está **int** e é um parâmetro de saída. Esse valor pode ser usado ao executar [sp_helppeerresponses &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) para exibir todas as respostas a uma solicitação de status.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_requestpeerresponse** é usado em replicação transacional ponto a ponto.  
  
 **sp_requestpeerresponse** é usado para garantir que todos os comandos foram recebidos por todos os outros nós antes de restaurar um banco de dados publicado em uma topologia ponto a ponto. É também usado ao aplicar alterações de DDL (linguagem de definição de dados) feitas enquanto um nó estava offline para estimar quando essas alterações alcançarão os outros nós.  
  
 **sp_requestpeerresponse** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_requestpeerresponse**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
