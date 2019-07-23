---
title: Tipos de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5ac8f243b559efcbee8f27b201469d7bf562b076
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895315"
---
# <a name="types-of-replication"></a>Tipos de replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece os seguintes tipos de replicação para uso nos aplicativos distribuídos:  
  
-   Replicação transacional. Para obter mais informações, consulte [Replicação transacional](../../relational-databases/replication/transactional/transactional-replication.md).  
  
-   Replicação de mesclagem. Para obter mais informações, consulte [Replicação de mesclagem](../../relational-databases/replication/merge/merge-replication.md).  
  
-   Replicação de instantâneo Para obter mais informações, consulte [Replicação de instantâneo](../../relational-databases/replication/snapshot-replication.md).  
  
 O tipo de replicação que você escolhe para um aplicativo, depende de muitos fatores, incluindo o ambiente físico da replicação, o tipo e a quantidade de dados a serem replicados e se os dados serão ou não atualizados no Assinante. O ambiente físico inclui o número e local dos computadores envolvidos na replicação e se esses computadores são clientes (estações de trabalho, laptops ou dispositivos portáteis) ou servidores.  
  
 Cada tipo de replicação começa normalmente com uma sincronização inicial dos objetos publicados entre o Publicador e os Assinantes. Esta sincronização inicial pode ser executada por replicação com um *instantâneo*, que é uma cópia de todos os objetos e dados especificados por uma publicação. Depois que o instantâneo é criado, ele é distribuído aos Assinantes. Para alguns aplicativos, a replicação de instantâneo é tudo o que é necessário. Para outros tipos de aplicativos, é importante que as alterações de dados subsequentes fluam para o Assinante de forma incremental com o passar do tempo. Alguns aplicativos também exigem que as alterações fluam do Assinante de volta para o Publicador. A replicação transacional e a replicação de mesclagem fornecem opções para estes tipos de aplicativos.  
  
 As alterações de dados não são rastreadas para a replicação de instantâneo. Sempre que um instantâneo é aplicado, ele sobrescreve por completo os dados existentes. A replicação transacional rastreia as alterações pelo log de transação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a replicação de mesclagem rastreia as alterações pelos gatilhos e tabelas de metadados.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos agentes de replicação.](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
