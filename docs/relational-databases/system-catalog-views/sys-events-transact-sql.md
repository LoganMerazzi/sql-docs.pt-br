---
title: sys. Events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.events_TSQL
- sys.events
- events_TSQL
- events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.events catalog view
ms.assetid: f245a97a-80fc-43fb-a6e4-139420c9a47a
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15fac5b2449e90fe7d6500bca383a71bc73954f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025787"
---
# <a name="sysevents-transact-sql"></a>sys.events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contém uma linha para cada evento para qual um gatilho ou uma notificação de eventos são disparados. Esses eventos representam os tipos de eventos que são especificados quando a gatilho ou notificação de eventos é criada usando [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) ou [CREATE EVENT NOTIFICATION](../../t-sql/statements/create-event-notification-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do gatilho ou da notificação de eventos. Esse valor, junto com **tipo**, exclusivamente identifica a linha.|  
|**type**|**int**|Evento que faz o gatilho ser disparado.|  
|**type_desc**|**nvarchar(60)**|Descrição do evento que faz o gatilho ser disparado.|  
|**is_trigger_event**|**bit**|1 = Evento de gatilho.<br /><br /> 0 = Evento de notificação.|  
|**event_group_type**|**int**|Grupo de eventos no qual o gatilho ou a notificação de eventos são criados, ou NULL quando não é criado em um grupo de eventos.|  
|**event_group_type_desc**|**nvarchar(60)**|Descrição do grupo de eventos no qual o gatilho ou a notificação de eventos são criados, ou NULL quando não é criado em um grupo de eventos.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
