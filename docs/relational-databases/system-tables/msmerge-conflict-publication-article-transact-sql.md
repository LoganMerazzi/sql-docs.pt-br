---
title: Msmerge_conflict _&lt;publicação&gt;_&lt;artigo&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: stevestein
ms.author: sstein
ms.openlocfilehash: dfae18a55ddb8b1c95aad25e27f006b28fde79af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895109"
---
# <a name="msmergeconflictltpublicationgtltarticlegt-transact-sql"></a>Msmerge_conflict _&lt;publicação&gt;_&lt;artigo&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **msmerge_conflict _*publicação*_ * artigo*** tabela contém informações sobre linhas conflitantes ou alterações de linhas que foram desfeitas para alcançar convergência de dados. Existe uma tabela de conflitos para cada tabela replicada na publicação, onde o nome da tabela de conflitos é anexada com o nome da publicação e do artigo. Essas tabelas de conflitos específicas do artigo existem no banco de dados usado para registro de conflito, geralmente o banco de dados de publicação, mas pode ser o banco de dados de assinatura se houver log de conflitos descentralizado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|***article_column_name***|**variable**|Representa uma coluna em uma tabela replicada. Essa tabela do sistema contém uma coluna para cada coluna no artigo de tabela.|  
|**rowguid**|**uniqueidentifier**|O identificador de linha para o conflito de exclusão.|  
|**ModifiedDate**|**datetime**|A hora quando o conflito ocorreu.|  
|**origin_datasource_id**|**uniqueidentifier**|A assinatura para a qual a alteração de linha foi desfeita ou perdeu o conflito.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
