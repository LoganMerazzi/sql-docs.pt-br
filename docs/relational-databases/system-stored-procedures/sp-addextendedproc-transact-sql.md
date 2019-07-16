---
title: sp_addextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0bc8ea22699762927a026ae4cc811500c193555c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072749"
---
# <a name="spaddextendedproc-transact-sql"></a>sp_addextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra o nome de um novo procedimento armazenado estendido à [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use a [Integração CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @functname = ] 'procedure'` É o nome da função a ser chamada dentro da biblioteca de vínculo dinâmico (DLL). *procedimento* está **nvarchar(517)** , sem padrão. *procedimento* , opcionalmente, pode incluir o nome do proprietário na forma *owner.function*.  
  
`[ @dllname = ] 'dll'` É o nome da DLL que contém a função. *dll* está **varchar(255)** , sem padrão. É recomendável especificar o caminho completo da DLL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Depois que um procedimento armazenado estendido é criado, ele deve ser adicionado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio **sp_addextendedproc**. Para obter mais informações, consulte [adicionando um procedimento armazenado estendido ao SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md).  
  
 Esse procedimento pode ser executado somente na **mestre** banco de dados. Para executar um procedimento armazenado estendido de um banco de dados diferente de **mestre**, qualifique o nome do procedimento armazenado estendido com **mestre**.  
  
 **sp_addextendedproc** adiciona entradas para o [sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) exibição de catálogo, registrar o nome do novo procedimento armazenado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele também adiciona uma entrada na [extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) exibição do catálogo.  
  
> [!IMPORTANT]  
>  DLLs existentes que não são registradas com um caminho completo não funcionarão depois da atualização do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para corrigir o problema, use **sp_dropextendedproc** para cancelar o registro de DLL e, em seguida, registrá-la novamente com **sp_addextendedproc**, especificando o caminho completo.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_addextendedproc**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona o **xp_hello** o procedimento armazenado estendido.  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>Consulte também  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
