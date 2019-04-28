---
title: sp_cursorclose (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56ff3e67c51be8618f0254298a7d8707e18884ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724222"
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fecha e desaloca o cursor, como também libera todos os recursos associados; ou seja, descarta a tabela temporária usada para dar suporte a KEYSET ou STATIC **cursor**. sp_cursorclose é invocado pela especificação de ID = 9 em um pacote do protocolo TDS.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 É um cursor *manipular* valor gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e retornados pelo procedimento sp_cursoropen. *cursor* é um parâmetro obrigatório que chama uma **int** valor de entrada.  
  
> [!NOTE]  
>  Um valor de entrada -1 será aplicado a todos os cursores na conexão atual.  
  
## <a name="remarks"></a>Comentários  
 *cursor* retornará mensagens de erro se o procedimento foi executado após o cursor for fechado ou se um identificador inválido for especificado.  
  
 O status RPC indica êxito ou falha geral.  
  
 A contagem de linhas DONE é sempre 0.  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
