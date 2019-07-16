---
title: sp_helpextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3dcbe6d187b56b0b15ae829eeecf1811b02dfee7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943502"
---
# <a name="sphelpextendedproc-transact-sql"></a>sp_helpextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata os procedimentos armazenados estendidos atualmente definidos e o nome da biblioteca de vínculo dinâmico (DLL) à qual o procedimento (função) pertence.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use a [Integração CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @funcname = ] 'procedure'` É o nome do procedimento armazenado estendido para o qual as informações são relatadas. *procedimento* está **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do procedimento armazenado estendido.|  
|**dll**|**nvarchar(255)**|O nome da DLL.|  
  
## <a name="remarks"></a>Comentários  
 Quando *procedimento* for especificado, **sp_helpextendedproc** procedimento armazenado estendido de relatórios no especificado. Quando esse parâmetro não for fornecido, **sp_helpextendedproc** retorna todas as estendido nomes de procedimento armazenado e os nomes DLL para o qual cada procedimento armazenado estendido pertence.  
  
## <a name="permissions"></a>Permissões  
 Permissão para executar **sp_helpextendedproc** é concedida a **público**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-reporting-help-on-all-extended-stored-procedures"></a>A. Relatando ajuda em todos os procedimentos armazenados estendidos  
 O exemplo a seguir relata todos os procedimentos armazenados estendidos.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc;  
GO  
```  
  
### <a name="b-reporting-help-on-a-single-extended-stored-procedure"></a>B. Relatando ajuda em um único procedimento armazenado estendido  
 O exemplo a seguir relata a `xp_cmdshell` o procedimento armazenado estendido.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
