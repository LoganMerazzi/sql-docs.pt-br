---
title: Queue Reader Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.queuereaderagent.f1
helpviewer_keywords:
- Queue Reader Agent dialog box
ms.assetid: f02d24b6-dcb5-4126-b56e-fab41cfe4337
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f07c9be82be63d01d563499a80e049e572a4150
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63262055"
---
# <a name="queue-reader-agent"></a>Queue Reader Agent
  A caixa de diálogo **Queue Reader Agent** exibe informações detalhadas sobre o Queue Reader Agent, incluindo status, histórico, mensagens informativas e qualquer mensagem de erro.  
  
## <a name="options"></a>Opções  
 Selecione as sessões do Queue Reader Agent a serem exibidas no menu **Exibir** e depois selecione uma sessão específica na grade rotulada **Sessões do Queue Reader Agent**. Informações detalhadas sobre essa sessão são exibidas na grade rotulada **Ações na sessão selecionada**. Se a sessão selecionada terminou em erro, a área de texto rotulada **Detalhes ou mensagem de erro da sessão selecionada** também será exibida.  
  
 **Exibir**  
 Selecione as sessões do Queue Reader Agent a serem exibidas. O Queue Reader Agent normalmente é executado continuamente, portanto pode haver somente uma sessão para exibir.  
  
 **Status**  
 O status do Queue Reader Agent. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Tentando novamente comandos com falha  
  
-   Não está sendo executado  
  
-   Executando  
  
 **Start Time**  
 A hora de início da sessão.  
  
 **Hora de término**  
 A hora de término da sessão. Se o agente não parou, esse campo estará vazio.  
  
 **Duration**  
 A quantidade de tempo que o Queue Reader Agent está em execução nessa sessão. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total da sessão, se a sessão do agente tiver terminado.  
  
 **Mensagem de erro**  
 Se uma sessão terminou em um erro, esse campo exibirá a última mensagem de erro registrada pelo Queue Reader Agent. Se uma sessão não terminou em erro, esse campo ficará em branco.  
  
 **Mensagem de Ação**  
 Todas as mensagens informativas e de erro que o Queue Reader Agent registrou durante a sessão selecionada.  
  
 **Tempo da Ação**  
 O tempo no qual a ação descrita na coluna **Mensagem de Ação** foi executada.  
  
 **Detalhes ou mensagem de erro da sessão selecionada**  
 Exibido somente se a sessão selecionada exibir um valor de **Erro** na coluna **Status** . Essa área de texto exibe informações de erro detalhadas e o comando tentado no momento do erro. Também inclui links para conteúdo adicional relacionado ao erro.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas usando o Replication Monitor](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitorando a Replicação](monitoring-replication.md)   
 [Visão geral dos agentes de replicação](agents/replication-agents-overview.md)  
  
  
