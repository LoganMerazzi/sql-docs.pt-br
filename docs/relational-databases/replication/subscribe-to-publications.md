---
title: Assinar publicações | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.conc.subtopubs.f1
helpviewer_keywords:
- subscriptions [SQL Server replication], about subscriptions
- pull subscriptions [SQL Server replication]
- subscriptions [SQL Server replication]
- push subscriptions [SQL Server replication], about push subscriptions
- merge replication subscribing [SQL Server replication]
- merge replication subscribing [SQL Server replication], about subscribing
- publications [SQL Server replication], subscribing
- push subscriptions [SQL Server replication]
- pull subscriptions [SQL Server replication], about pull subscriptions
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 088ee30a-05ab-47c4-92ed-316b93e12445
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3a15256be44ace579c6dcc9aa74bf55fdc319e7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129928"
---
# <a name="subscribe-to-publications"></a>Assinar publicações
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Uma assinatura é uma solicitação para se obter uma cópia dos dados e objetos do banco de dados em uma publicação. Uma assinatura define qual publicação será recebida, e onde e quando será recebida. Ao planejar assinaturas, considere onde o processamento de agente deverá acontecer. O tipo de assinatura selecionado controla onde o agente é executado. Com uma assinatura push, o Agente de Mesclagem ou o Agente de Distribuição são executados no Distribuidor, enquanto que, com uma assinatura pull, os agentes são executados nos Assinantes. Após a criação de uma assinatura, ela não pode ser alterada de um tipo para outro.  
  
|Assinatura|Características|Use quando|  
|------------------|---------------------|--------------|  
|Assinatura push|Em uma assinatura push, o Publicador propaga alterações para o Assinante sem solicitação do Assinante. As alterações podem ser empurradas para os Assinantes sob demanda continuamente ou com base em agendamento. O Agente de Distribuição ou o Agente de Mesclagem são executados no Distribuidor.|Os dados são sincronizados de forma contínua ou com base em uma agenda que recorre com frequência.<br /><br /> As publicações requerem movimentação de dados tempo quase real.<br /><br /> A sobrecarga do processador superior no Distribuidor não afeta o desempenho.<br /><br /> É usado com mais frequência com replicação transacional e de instantâneo.|  
|Assinatura pull|Em uma assinatura pull, o Assinante solicita que alterações sejam feitas no Publicador. As assinaturas pull permitem que o usuário, no Assinante, determine quando as alterações de dados serão sincronizadas. O Agente de Distribuição ou o Agente de Mesclagem são executados no Assinante.|Em geral, os dados são sincronizados sob demanda ou com base em uma agenda, em vez de continuamente.<br /><br /> A publicação tem um grande número de Assinantes, e/ou demandaria muitos recursos para executar todos os agentes no Distribuidor.<br /><br /> Os assinantes são autônomos, desconectados, e/ou móveis. Os assinantes determinam quando as alterações são conectadas e sincronizadas.<br /><br /> Usado com mais frequência com replicação de mesclagem.|  
  
## <a name="merge-replication-subscription-types"></a>Tipos de assinatura de replication de mesclagem  
 Todos os tipos de replicação permitem assinaturas push e pull. A replicação de mesclagem usa duas condições a mais para distinguir assinaturas: assinatura de cliente e assinatura de servidor. Os tipos de assinatura de cliente e de servidor podem ser usados com assinaturas push e pull. As assinaturas de cliente são apropriadas para a maioria dos Assinantes, enquanto que as assinaturas de servidor são usadas, em geral, para Assinantes que republicam dados em outros Assinantes. A opção de assinatura também afeta a resolução de conflitos.  
  
## <a name="non-sql-server-subscribers"></a>Non-SQL Server Subscribers  
 O Oracle e o IBM DB2 podem assinar as publicações de instantâneo e transacionais usando assinaturas push. Para obter mais informações, consulte [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
## <a name="creating-subscriptions"></a>Criando assinaturas  
 Para criar uma assinatura, forneça as seguintes informações:  
  
-   O nome da publicação.  
  
-   Nome do Assinante e o banco de dados de assinatura.  
  
-   Se o Agente de Distribuição ou o Agente de Mesclagem forem executados no Distribuidor ou no Assinante.  
  
-   Se o Agente de Distribuição ou Agente de Mesclagem forem executados de forma contínua, com base em uma agenda ou somente sob demanda.  
  
-   Se o Agente de Instantâneo precisar criar um instantâneo inicial para a assinatura e se o Agente de Distribuição ou Agente de Mesclagem devem aplicar esse instantâneo no Assinante.  
  
-   As contas nas quais o Agente de Distribuição ou Agente de Mesclagem serão executados.  
  
-   Com relação à replicação de mesclagem, o tipo de assinatura: de servidor ou cliente.  
  
 **Para criar uma assinatura push**  
  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
  
 **Para exibir ou modificar propriedades de assinatura push**  
  
 [Exibir e modificar propriedades de assinatura push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
 **Para excluir uma assinatura push**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Excluir uma assinatura push](../../relational-databases/replication/delete-a-push-subscription.md)  
  
> [!NOTE]  
>  Excluir uma assinatura não remove objetos publicados no Assinante.  
  
 **Para criar uma assinatura pull**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)  
  
 **Para exibir ou modificar propriedades de assinatura pull**  
  
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
 **Para excluir uma assinatura pull**  
  
 [Excluir uma assinatura pull](../../relational-databases/replication/delete-a-pull-subscription.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Proteger o Assinante](../../relational-databases/replication/security/secure-the-subscriber.md)   
 [Desativação e expiração de assinatura](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
