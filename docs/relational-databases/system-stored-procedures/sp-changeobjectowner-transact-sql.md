---
title: sp_changeobjectowner (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8980ab1f968bcc842fdd17a6095a9945fcc26b42
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62997077"
---
# <a name="spchangeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o proprietário de um objeto no banco de dados atual.  
  
> [!IMPORTANT]
>  Esse procedimento armazenado só funciona com os objetos disponíveis no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md) ou [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) em vez disso. **sp_changeobjectowner** altera o esquema e o proprietário. Para preservar a compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esse procedimento armazenado irá alterar proprietários de objetos somente quando o proprietário atual e o novo possuírem esquemas que tenham o mesmo nome que seus nomes de usuário do banco de dados.  
> 
> [!IMPORTANT]
>  Um novo requisito de permissão foi adicionado a esse procedimento armazenado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'object'` É o nome de uma tabela existente, exibição, função definida pelo usuário ou procedimento armazenado no banco de dados atual. *objeto* é um **nvarchar(776)**, sem padrão. *objeto* pode ser qualificado com o proprietário do objeto existente, na forma _existing_owner_**.** _objeto_ se o esquema e seu proprietário tiverem o mesmo nome.  
  
`[ @newowner = ] 'owner_ '` É o nome da conta de segurança que será o novo proprietário do objeto. *proprietário* está **sysname**, sem padrão. *proprietário* deve ser um usuário de banco de dados válido, a função de servidor [!INCLUDE[msCoName](../../includes/msconame-md.md)] logon do Windows ou grupo do Windows com acesso ao banco de dados atual. Se o novo proprietário for um usuário ou grupo do Windows para o qual não há uma entidade correspondente no nível de banco de dados, será criado um usuário de banco de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changeobjectowner** remove todas as permissões existentes do objeto. Será necessário reaplicar as permissões que você deseja manter depois de executar **sp_changeobjectowner**. Portanto, é recomendável que você gerar o script de permissões existentes antes da execução **sp_changeobjectowner**. Depois que propriedade do objeto foi alterada, você poderá usar o script para reaplicar permissões. É necessário modificar o proprietário do objeto no script de permissões antes de executar.  
  
 Para alterar o proprietário de um protegível, use ALTER AUTHORIZATION. Para alterar um esquema, use ALTER SCHEMA.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **db_owner** fixo de função de banco de dados ou a associação em ambos o **db_ddladmin** função fixa de banco de dados e o **db_securityadmin** função de banco de dados fixa e também a permissão CONTROL no objeto.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o proprietário da tabela `authors` para `Corporate\GeorgeW`.  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
