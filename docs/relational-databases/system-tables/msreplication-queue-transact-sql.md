---
title: MSreplication_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
author: stevestein
ms.author: sstein
ms.openlocfilehash: 914cf3ad65c881383a6d625c07d4fb5ed028b36a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080013"
---
# <a name="msreplicationqueue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplication_queue** tabela é usada pelo processo de replicação para armazenar comandos enfileirados emitidos por todas as assinaturas de atualização em fila que estão usando o SQL-base em fila. Essa tabela é armazenada no banco de dados de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|O nome do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados de publicação.|  
|**publicação**|**sysname**|O nome da publicação.|  
|**tranid**|**sysname**|A ID da transação na qual o comando enfileirado foi executado.|  
|**data**|**varbinary(8000)**|O pacote de fluxo de bytes que armazenou informações sobre os comandos na fila.|  
|**datalen**|**int**|O comprimento dos dados, em bytes.|  
|**CommandType**|**int**|O tipo de comando que está sendo enfileirado:<br /><br /> 1 = Comando de usuário na transação.<br /><br /> 2 = Comando de sincronização de assinatura.|  
|**insertdate**|**datetime**|A data da inserção.|  
|**orderkey**|**bigint**|A coluna de identidade que aumenta de forma monotônica.|  
|**cmdstate**|**bit**|O estado do comando:<br /><br /> 0 = Completo.<br /><br /> 1 = Parcial.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
