---
title: sp_fulltext_pendingchanges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_pendingchanges_TSQL
- sp_fulltext_pendingchanges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_pendingchanges
ms.assetid: fee042fe-4781-4a33-a01b-d98fb5629f1b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d4d8cbd7082a3ec8d19ccc6df7212a70b101e6b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124223"
---
# <a name="spfulltextpendingchanges-transact-sql"></a>sp_fulltext_pendingchanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna alterações não processadas, como inserções, atualizações e exclusões pendentes, feitas na tabela especificada com controle de alterações habilitado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_fulltext_pendingchanges table_id  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_id*  
 Identificação da tabela. Se a tabela não for indexada com texto completo ou se o controle de alterações não for habilitado, será retornado um erro.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**Chave**|*|É o valor da chave de texto completo da tabela especificada.|  
|**DocId**|**bigint**|É a coluna do identificador de documento (DocId) interno que corresponde ao valor da chave.|  
|**Status**|**int**|0 = a linha será removida do índice de texto completo.<br /><br /> 1 = a linha será indexada com texto completo.<br /><br /> 2 = a linha está atualizada.<br /><br /> -1 = a linha está em um estado de transição (em lotes, mas não confirmada) ou de erro.|  
|**DocState**|**tinyint**|É um despejo bruto da coluna de status do mapa do identificador de documento (DocId) interno.|  
  
 <sup>* O tipo de dados para a chave é o mesmo como o tipo de dados da coluna de chave de texto completo na tabela base.</sup>  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="remarks"></a>Comentários  
 Se não houver nenhuma alteração para processar, um conjunto de linhas vazio será retornado.  
  
 Consultas de pesquisa de texto completo não retornam linhas com um **Status** valor de 0. Isso ocorre porque a linha foi excluída da tabela base e está aguardando para ser excluída do índice de texto completo.  
  
 Para saber quantas alterações pendentes uma determinada tabela possui, use a propriedade **TableFullTextPendingChanges** da função OBJECTPROPERTYEX.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de pesquisa de texto completo e pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  
