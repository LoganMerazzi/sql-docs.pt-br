---
title: sp_syscollector_run_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_run_collection_set_TSQL
- sp_syscollector_run_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_run_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 7bbaee48-dfc7-45c0-b11f-c636b6a7e720
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2ad81b1d92bb45d9ab15ca11897804cc0d333a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63001754"
---
# <a name="spsyscollectorruncollectionset-transact-sql"></a>sp_syscollector_run_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia um conjunto de coleta se o coletor já estiver habilitado e o conjunto de coleta estiver configurado para o modo de coleta sem armazenamento em cache.  
  
> [!NOTE]  
>  Este procedimento falhará se for executado em um conjunto de coleta configurado para o modo de coleta em cache.  
  
 sp_syscollector_run_collection_set permite que um usuário tire instantâneos de dados sob demanda.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_run_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @collection_set_id = ] collection_set_id` É o identificador local exclusivo para o conjunto de coleta. *collection_set_id* está **int** e deve ter um valor se *nome* é NULL.  
  
`[ @name = ] 'name'` É o nome do conjunto de coleta. *nome da* está **sysname** e deve ter um valor se *collection_set_id* é NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Qualquer um dos *collection_set_id* ou *nome* deve ter um valor, ambos não podem ser NULL.  
  
 Esse procedimento iniciará a coleta e carregará os trabalhos para a coleção especificada definida e iniciará imediatamente o trabalho de agente de coleta se o conjunto de coleta tem seu **@collection_mode** definido como não armazenado em cache (1). Para obter mais informações, consulte [sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
 sp_sycollector_run_collection_set também pode ser usado para executar um conjunto de coleta que não tenha uma agenda.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **dc_operator** (com permissão EXECUTE) a função de banco de dados fixa para executar esse procedimento.  
  
## <a name="example"></a>Exemplo  
 Inicia um conjunto de coleta usando seu identificador.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_run_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
