---
title: MSSQL_ENG014157 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014157 error
ms.assetid: 1a0890cf-d977-43e0-a2ba-9c5ff1a8f856
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5ac7abab429d56aa835c46479140f0a29013db6a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100040"
---
# <a name="mssqleng014157"></a>MSSQL_ENG014157
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14157|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|A assinatura criada pelo Assinante '%s' para a publicação '%s' expirou e foi descartada.|  
  
## <a name="explanation"></a>Explicação  
 Um Assinante deve fazer a sincronização com o Publicador no momento especificado no período de retenção de publicação. Se um Assinante não fizer a sincronização nesse período, a assinatura será expirada. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="user-action"></a>Ação do usuário  
 É necessário recriar e inicializar a assinatura para que o Assinante comece a receber novamente as alterações de dados:  
  
-   Para obter mais informações sobre como criar assinaturas, consulte [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Para obter informações sobre como inicializar assinaturas, consulte [Inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md).  
  
 Se o banco de dados de assinatura contiver alterações que não foram sincronizadas com o Publicador, será possível usar o [tablediff Utility](../../tools/tablediff-utility.md) para determinar quais linhas são diferentes nos bancos de dados de publicação e de assinatura.  
  
 É possível aumentar o período de retenção de publicação para que a assinatura não expire. Tome cuidado ao definir um valor alto, já que isso pode resultar no armazenamento de mais dados e metadados, o que afeta o desempenho. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
