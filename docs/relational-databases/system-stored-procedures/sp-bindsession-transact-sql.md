---
title: sp_bindsession (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindsession
- sp_bindsession_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindsession
ms.assetid: 1436fe21-ad00-4a98-aca1-1451a5e571d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: fac327d88aa8a6d74e153c1c7b2f3d637bf6f936
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046018"
---
# <a name="spbindsession-transact-sql"></a>sp_bindsession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Associa ou desassocia uma sessão para outras sessões na mesma instância das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. As sessões associadas permitem que duas ou mais sessões participem da mesma transação e bloqueios de compartilhamento até que uma ROLLBACK TRANSACTION ou COMMIT TRANSACTION seja emitida.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use MARS (vários conjuntos de resultados ativos) ou, então, transações distribuídas. Para obter mais informações, confira [Usando o MARS &#40;conjunto de resultados ativos múltiplos&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_bindsession { 'bind_token' | NULL }  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *bind_token* **'**  
 É o token que identifica a transação originalmente obtida usando **sp_getbindtoken** ou o Open Data Services **srv_getbindtoken** função. *bind_token*está **varchar(255)** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Duas sessões associadas compartilham somente uma transação e bloqueios. Cada sessão retém seu próprio nível de isolamento e a definição de um novo nível de isolamento em uma sessão não afeta o nível de isolamento da outra sessão. Cada sessão permanece identificada por sua conta de segurança e só pode acessar os recursos de banco de dados para o qual a conta recebeu permissão.  
  
 **sp_bindsession** usa um token de associação para associar duas ou mais sessões de cliente existentes. Essas sessões de cliente devem estar na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] do qual o token de associação foi obtido. Uma sessão é um cliente executando um comando. As sessões associadas de banco de dados compartilham uma transação e um espaço de bloqueio.  
  
 Um token de associação obtido de uma instância de [!INCLUDE[ssDE](../../includes/ssde-md.md)] não pode ser usado para uma sessão de cliente conectada a outra instância, mesmo para transações DTC. Um token de associação só é válido localmente dentro de cada instância e não pode ser compartilhado por diversas instâncias. Para associar sessões de cliente em outra instância das [!INCLUDE[ssDE](../../includes/ssde-md.md)], você deve obter um token de associação diferente executando **sp_getbindtoken**.  
  
 **sp_bindsession** falhará com um erro se ele usa um token que não está ativo.  
  
 Desassocie uma sessão usando **sp_bindsession** sem especificar *bind_token* ou passando NULL na *bind_token*.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir faz a associação do token de associação especificado à sessão atual.  
  
> [!NOTE]  
>  O token de associação mostrado no exemplo foi obtido executando **sp_getbindtoken** antes de executar **sp_bindsession**.  
  
```  
USE master;  
GO  
EXEC sp_bindsession 'BP9---5---->KB?-V'<>1E:H-7U-]ANZ';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [srv_getbindtoken &#40;API de procedimento armazenado estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
