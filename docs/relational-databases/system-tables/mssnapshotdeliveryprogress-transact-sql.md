---
title: MSsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
author: stevestein
ms.author: sstein
ms.openlocfilehash: 638bea3db68712300ad2284e50676bf1df67c9ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139808"
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSsnapshotdeliveryprogress** tabela é usada para controlar arquivos que tenham sido entregues com êxito ao assinante quando um instantâneo está sendo aplicado. Esses dados são usados para retomar a entrega de arquivos quando o Merge Agent não consegue entregar todos os arquivos durante a sessão, para que os mesmos arquivos não sejam entregues novamente na próxima execução do Merge Agent. Essa tabela é armazenada no Assinante, no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|Identifica o caminho para a pasta de instantâneo na qual o arquivo foi entregue com êxito. Para publicações que usam filtros com parâmetros, a cadeia de caracteres **dynsnap** será acrescentado ao valor.|  
|**progress_token_hash**|**int**|Um valor de hash gerado com base no valor de *progress_token* que é usado melhorar a eficiência da pesquisa de um determinado *progress_token* valor.|  
|**progress_token**|**nvarchar(500)**|Identifica um valor entregue com êxito, onde o valor é uma combinação do nome de arquivo e caminho.|  
|**progress_timestamp**|**datetime**|O **datetime** valor que indica quando um arquivo de instantâneo foi entregue com êxito.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
