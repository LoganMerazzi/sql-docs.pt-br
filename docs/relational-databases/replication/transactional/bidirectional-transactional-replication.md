---
title: Replicação transacional bidirecional | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3eefd48c594c0a13388bb932faf1c5cf9fd9adea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041534"
---
# <a name="bidirectional-transactional-replication"></a>replicação transacional bidirecional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Replicação transacional bidirecional é uma topologia de replicação transacional específica que permite a dois servidores trocarem alterações entre si: cada servidor publica dados e, então, assina uma publicação com os mesmos dados do outro servidor. O parâmetro **@loopback_detection** de [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) é definido para TRUE a fim de garantir que as alterações sejam enviadas somente ao Assinante e não resultem na alteração sendo enviada de volta ao Publicador.  
  
 Em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores, essa topologia também tem suporte para replicação transacional ponto a ponto, mas replicação bidirecional pode fornecer desempenho aprimorado.  
  
## <a name="see-also"></a>Consulte Também  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
