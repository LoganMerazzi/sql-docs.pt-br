---
title: MSpeer_conflictdetectionconfigrequest (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2ecd4ef541422b1241689f17ab5c4f1a53bcc0a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115040"
---
# <a name="mspeerconflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado em replicação ponto a ponto para controlar solicitações de toda a topologia para uma publicação. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**int**|Identifica uma solicitação de configuração de conflito. A coluna request_id em [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md) usa esse valor.|  
|publication|**sysname**|Nome da publicação da qual a solicitação de configuração de conflito originou.|  
|sent_date|**datetime**|Data e hora em que a solicitação de configuração de conflito foi iniciada.|  
|timeout|**int**|Quantidade de tempo que um procedimento deve esperar por todos os pontos retornarem informações sobre conflitos.|  
|modified_date|**datetime**|Data e hora em que uma fase foi concluída.|  
|progress_phase|**nvarchar(32)**|Identifica a fase atual de processamento, usando um dos seguintes valores:<br /><br /> Started (iniciado)<br /><br /> Explorando topologia<br /><br /> Coletando status<br /><br /> Status coletado|  
|phase_timed_out|**bit**|Indica se a fase atual atingiu o tempo limite.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
