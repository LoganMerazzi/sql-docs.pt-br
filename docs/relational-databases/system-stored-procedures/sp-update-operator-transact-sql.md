---
title: sp_update_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2a766ad74f42336612859c63cf42df654846ff96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084838"
---
# <a name="spupdateoperator-transact-sql"></a>sp_update_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza informações sobre um operador (recipiente de notificação) para ser usado com alertas e trabalhos.  
  
   ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_operator   
     [ @name =] 'name'   
     [ , [ @new_name = ] 'new_name' ]   
     [ , [ @enabled = ] enabled]   
     [ , [ @email_address = ] 'email_address' ]  
     [ , [ @pager_address = ] 'pager_number']   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]  
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]  
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]  
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @name=] '*nome*'  
 O nome do operador a ser modificado. *nome da* está **sysname**, sem padrão.  
  
 [ @new_name=] '*new_name*'  
 O novo nome do operador. Esse nome deve ser exclusivo. *new_name* está **sysname**, com um padrão NULL.  
  
 [ @enabled=] *habilitado*  
 Um número que indica o status atual do operador (**1** se está habilitado no momento, **0** se não). *habilitada* está **tinyint**, com um padrão NULL. Se não estiver habilitado, um operador não receberá notificações de alerta.  
  
 [ @email_address=] '*email_address*'  
 O endereço de email do operador. Essa cadeia de caracteres é passada diretamente para o sistema de email. *email_address* está **nvarchar(100)** , com um padrão NULL.  
  
 [ @pager_address=] '*pager_number*'  
 O endereço de pager do operador. Essa cadeia de caracteres é passada diretamente para o sistema de email. *pager_number* está **nvarchar(100)** , com um padrão NULL.  
  
 [ @weekday_pager_start_time=] *weekday_pager_start_time*  
 Especifica a hora depois da qual uma notificação de pager pode ser enviada a esse operador, de segunda-feira a sexta-feira. *weekday_pager_start_time*está **int**, com um padrão de NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @weekday_pager_end_time=] *weekday_pager_end_time*  
 Especifica a hora depois da qual uma notificação de pager não pode ser enviada ao operador especificado, de segunda-feira a sexta-feira. *weekday_pager_end_time*está **int**, com um padrão de NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @saturday_pager_start_time=] *saturday_pager_start_time*  
 Especifica a hora depois da qual uma notificação de pager pode ser enviada ao operador aos sábados. *saturday_pager_start_time*está **int**, com um padrão de NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @saturday_pager_end_time=] *saturday_pager_end_time*  
 Especifica a hora depois da qual uma notificação de pager não pode ser enviada ao operador aos sábados. *saturday_pager_end_time*está **int**, com um padrão de NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @sunday_pager_start_time=] *sunday_pager_start_time*  
 Especifica a hora depois da qual uma notificação de pager pode ser enviada ao operador aos domingos. *sunday_pager_start_time*está **int**, com um padrão de NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @sunday_pager_end_time=] *sunday_pager_end_time*  
 Especifica a hora depois da qual uma notificação de pager não pode ser enviada ao operador aos domingos. *sunday_pager_end_time*está **int**, com um padrão de NULL e deve ser inserida no formato HHMMSS para uso com um relógio de 24 horas.  
  
 [ @pager_days=] *pager_days*  
 Especifica os dias em que o operador está disponível para receber páginas (sujeitos aos horários de início/término especificados). *pager_days*está **tinyint**, com um padrão de NULL, e deve ser um valor de **0** por meio de **127**. *pager_days* é calculado somando os valores individuais para os dias necessários. Por exemplo, de segunda-feira a sexta-feira é **2**+**4**+**8**+**16** + **32** = **64**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Segunda-feira|  
|**4**|Terça-feira|  
|**8**|Quarta-feira|  
|**16**|Quinta-feira|  
|**32**|Sexta-feira|  
|**64**|Sábado|  
  
 [ @netsend_address=] '*netsend_address*'  
 O endereço de rede do operador para o qual a mensagem de rede é enviada. *netsend_address*está **nvarchar(100)** , com um padrão NULL.  
  
 [ @category_name=] '*categoria*'  
 O nome da categoria para este alerta. *categoria* está **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_update_operator deve ser executado a partir do banco de dados msdb.  
  
## <a name="permissions"></a>Permissões  
 As permissões para executar este procedimento usam como padrão membros da função de servidor fixa sysadmin.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir atualiza o status do operador como habilitado e define os dias (de segunda-feira a sexta-feira, das 8h às 17h) quando o operador pode ser notificado por pager.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_operator   
    @name = N'François Ajenstat',  
    @enabled = 1,  
    @email_address = N'françoisa',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 64 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
