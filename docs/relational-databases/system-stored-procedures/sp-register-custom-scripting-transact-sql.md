---
title: sp_register_custom_scripting (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: c10451148c6f9b2fda231691b770bca3928517f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075754"
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A replicação permite procedimentos armazenados personalizados definidos pelo usuário, para substituir um ou mais dos procedimentos padrão usados em replicação transacional. Quando uma alteração de esquema é feita em uma tabela replicada, esses procedimentos armazenados são recriados. **sp_register_custom_scripting** registra um procedimento armazenado ou [!INCLUDE[tsql](../../includes/tsql-md.md)] arquivo de script que é executado quando ocorre uma alteração de esquema para o script de definição para um novo definido pelo usuário procedimento armazenado personalizado. Esse novo procedimento armazenado personalizado deve refletir o novo esquema da tabela. **sp_register_custom_scripting** é executado no publicador do banco de dados de publicação, e o arquivo de script registrado ou o procedimento armazenado é executado no assinante quando ocorre uma alteração de esquema.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @type = ] 'type'` O tipo de procedimento armazenado personalizado ou script está sendo registrado. *tipo de* está **varchar(16)** , sem padrão e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**insert**|Procedimento armazenado personalizado registrado é executado quando uma instrução INSERT é replicada.|  
|**update**|Procedimento armazenado personalizado registrado é executado quando uma instrução UPDATE é replicada.|  
|**delete**|Procedimento armazenado personalizado registrado é executado quando uma instrução DELETE é replicada.|  
|**custom_script**|O script é executado ao término do gatilho DDL (Data Definition Language).|  
  
`[ @value = ] 'value'` Nome de um procedimento armazenado ou o nome e o caminho totalmente qualificado para o [!INCLUDE[tsql](../../includes/tsql-md.md)] arquivo de script que está sendo registrado. *valor* está **nvarchar(1024)** , sem padrão.  
  
> [!NOTE]  
>  Especificação de NULL para *valor*parâmetro irá cancelar o registro de um script registrado anteriormente, o que é o mesmo que executar [sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md).  
  
 Quando o valor de *tipo* é **custom_script**, o nome e caminho completo de um [!INCLUDE[tsql](../../includes/tsql-md.md)] arquivo de script é esperado. Caso contrário, *valor* deve ser o nome de um procedimento armazenado registrado.  
  
`[ @publication = ] 'publication'` Nome da publicação para o qual o procedimento armazenado personalizado ou script está sendo registrado. *publicação* está **sysname**, com um padrão de **nulo**.  
  
`[ @article = ] 'article'` Nome do artigo para o qual o procedimento armazenado personalizado ou script está sendo registrado. *artigo* está **sysname**, com um padrão de **nulo**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_register_custom_scripting** é usado em replicação de instantâneo e transacional.  
  
 Esse procedimento armazenado deve ser executado antes de efetuar uma alteração de esquema em uma  tabela replicada. Para obter mais informações sobre como usar esse procedimento armazenado, consulte [regenerar os procedimentos transacionais personalizados para refletir alterações de esquema](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa, o **db_owner** função de banco de dados fixa ou o **db_ddladmin** pode executar a função de banco de dados fixa **SP _ register_custom_scripting**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_unregister_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
