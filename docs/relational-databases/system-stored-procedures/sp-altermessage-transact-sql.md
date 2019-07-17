---
title: sp_altermessage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_altermessage_TSQL
- sp_altermessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_altermessage
ms.assetid: 1b28f280-8ef9-48e9-bd99-ec14d79abaca
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0722bbc713804af6b2b97b5651df5b564d17a136
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117799"
---
# <a name="spaltermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o estado de mensagens definidas pelo usuário ou do sistema em uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Mensagens definidas pelo usuário podem ser exibidas usando o **sys. messages** exibição do catálogo.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@message_id =** ] *message_number*  
 É o número de erro da mensagem a ser alterada de **sys. messages**. *message_number* está **int** sem nenhum valor padrão.  
  
`[ @parameter = ] 'write\_to\_log_'` É usado com **@parameter_value** para indicar que a mensagem deve ser escrito para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] log de aplicativo do Windows. *write_to_log* está **sysname** sem nenhum valor padrão. *write_to_log* deve ser definido como WITH_LOG ou NULL. Se *write_to_log* é definido como WITH_LOG ou NULL e o valor de **@parameter_value** é **true**, a mensagem é gravada no log de aplicativo do Windows. Se *write_to_log* é definido como WITH_LOG ou NULL e o valor de **@parameter_value** é **false**, a mensagem não é sempre gravada no log de aplicativo do Windows, mas pode ser gravada dependendo de como o erro foi gerado. Se *write_to_log* for especificado, o valor para **@parameter_value** também deve ser especificado.  
  
> [!NOTE]  
>  Se uma mensagem for gravada no log do aplicativo do Windows, ela também será gravada no arquivo de log de erros do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
`[ @parameter_value = ]'value_'` É usado com **@parameter** para indicar que o erro deve ser escrito para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] log de aplicativo do Windows. *valor* está **varchar(5)** , sem nenhum valor padrão. Se **verdadeira**, o erro sempre será gravado no log de aplicativo do Windows. Se **falsos**, o erro não são sempre gravado no log de aplicativo do Windows, mas pode ser gravado dependendo de como o erro foi gerado. Se *valor* for especificado, *write_to_log* para **@parameter** também deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 O efeito **sp_altermessage** com o WITH_LOG opção é semelhante do parâmetro RAISERROR WITH LOG, exceto que **sp_altermessage** altera o comportamento do log de uma mensagem existente. Se uma mensagem foi alterada para ser WITH_LOG, ela sempre será gravada no log de aplicativos do Windows, independentemente de como um usuário invocar o erro. Até mesmo se RAISERROR for executado sem a opção WITH_LOG, o erro será gravado no log de aplicativos do Windows.  
  
 As mensagens do sistema podem ser modificadas por meio **sp_altermessage**.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **serveradmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir faz com que a mensagem `55001` existente seja registrada no log de aplicativos do Windows.  
  
```  
EXECUTE sp_altermessage 55001, 'WITH_LOG', 'true';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
