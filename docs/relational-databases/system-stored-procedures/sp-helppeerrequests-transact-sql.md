---
title: sp_helppeerrequests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5b9e2a370c9acc9c22dac7e5e60ceb10e08e46ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137624"
---
# <a name="sphelppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre todas as solicitações de status recebidas por participantes em uma topologia de replicação ponto a ponto, onde essas solicitações foram inicializadas executando [sp_requestpeerresponse &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) qualquer o banco de dados publicado na topologia. Esse procedimento armazenado é executado no banco de dados de publicação em um Publicador que participa de uma topologia de replicação ponto a ponto. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação em uma topologia ponto a ponto para o qual as solicitações de status foram enviadas. *publicação* está **sysname**, sem padrão.  
  
`[ @description = ] 'description'` Valor que pode ser usado para identificar solicitações de status individuais, que permite que você filtrar respostas retornadas com base em usuário definiu informações fornecidas ao chamar [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). *Descrição* está **nvarchar (4000)** , com um padrão de **%** . Por padrão, todas as solicitações de status para a publicação são retornadas. Esse parâmetro é usado para retornar somente as solicitações de status com uma descrição correspondente ao valor fornecido no *descrição*, em que as cadeias de caracteres são correspondidas usando uma [como &#40;Transact-SQL&#41; ](../../t-sql/language-elements/like-transact-sql.md)cláusula.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica uma solicitação.|  
|**publicação**|**sysname**|Nome da publicação para a qual a solicitação de status foi enviada.|  
|**sent_date**|**datetime**|Data e hora de envio da solicitação de status.|  
|**description**|**nvarchar(4000)**|Informações que podem ser usadas para identificar solicitações de status individuais definidas pelo usuário.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helppeerrequests** é usado em replicação transacional ponto a ponto.  
  
 **sp_helppeerrequests** é usado ao restaurar um banco de dados publicado em uma topologia ponto a ponto.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_helppeerrequests**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
