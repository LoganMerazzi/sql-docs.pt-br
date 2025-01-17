---
title: Sincronizar uma assinatura push | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], push subscriptions
- subscriptions [SQL Server replication], push
- push subscriptions [SQL Server replication], synchronizing
ms.assetid: 0cfa7ae5-91d3-4a4f-9edf-a852d45783b5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 60fdfbecf617f0a4aa92b40b72b1b5e969f69388
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745876"
---
# <a name="synchronize-a-push-subscription"></a>Sincronizar uma assinatura push
  Este tópico descreve como sincronizar uma assinatura push no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [agentes de replicação](agents/replication-agents-overview.md), ou RMO (Replication Management Objects).  
  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Assinaturas são sincronizadas pelo Agente de Distribuição (para replicação transacional e de instantâneo) ou pelo Agente de Mesclagem (para replicação de mesclagem). Os agentes podem ser executados continuamente, sob demanda ou em um agendamento. Para obter mais informações sobre como especificar agendas de sincronização, consulte [Especificar agendas de sincronização](specify-synchronization-schedules.md).  
  
 Sincronize uma assinatura sob demea das pastas **Publicações Locais** e **Assinaturas Locais** no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e the **Todas as Assinaturas** no Replication Monitor. As assinaturas para as publicações Oracle não podem ser sincronizadas sob demanda no Assinante. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
#### <a name="to-synchronize-a-push-subscription-on-demand-in-management-studio-at-the-publisher"></a>Para sincronizar uma assinatura push sob demanda no Management Studio (no Publicador)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação com relação à qual as assinaturas serão sincronizadas.  
  
4.  Clique com o botão direito do mouse na assinatura a ser sincronizada e clique em **Exibir Status da Sincronização**.  
  
5.  Na caixa de diálogo **Exibir Status da Sincronização – \<Subscriber>:\<SubscriptionDatabase>** , clique em **Iniciar**. Quando a sincronização estiver concluída, a mensagem **Sincronização concluída** será exibida.  
  
6.  Clique em **Fechar**.  
  
#### <a name="to-synchronize-a-push-subscription-on-demand-in-management-studio-at-the-subscriber"></a>Para sincronizar uma assinatura push sob demanda no Management Studio (no Assinante)  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito do mouse na assinatura a ser sincronizada e clique em **Exibir Status da Sincronização**.  
  
4.  Uma mensagem é exibida sobre como estabelecer conexão com o Distribuidor. Clique em **OK**.  
  
5.  Na caixa de diálogo **Exibir Status da Sincronização – \<Subscriber>:\<SubscriptionDatabase>** , clique em **Iniciar**. Quando a sincronização estiver concluída, a mensagem **Sincronização concluída** será exibida.  
  
6.  Clique em **Fechar**.  
  
#### <a name="to-synchronize-a-push-subscription-on-demand-in-replication-monitor"></a>Para sincronizar uma assinatura push sob demanda no Replication Monitor  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e, depois, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com o botão direito do mouse na assinatura a ser sincronizada, depois clique em **Iniciar Sincronização**.  
  
4.  Para exibir o andamento da sincronização, clique com o botão direito do mouse na assinatura e, depois, clique em **Exibir Detalhes**.  
  
##  <a name="ReplProg"></a> Usando agentes de replicação  
 Assinaturas push podem ser sincronizadas por programa e sob demanda chamando o arquivo executável apropriado do agente de replicação do prompt de comando. O arquivo executável do agente de replicação chamado dependerá do tipo de publicação para a qual a assinatura push pertence.  
  
#### <a name="to-start-the-distribution-agent-to-synchronize-a-push-subscription-to-a-transactional-publication"></a>Para iniciar o Distribution Agent para sincronizar uma assinatura push a uma publicação transacional  
  
1.  Do prompt de comando ou do arquivo de lote no Distribuidor, execute **distrib.exe**. Especifique os seguintes argumentos de linha de comando:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     Se você estiver usando Autenticação do SQL Server, deve-se também especificar os seguintes argumentos:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
#### <a name="to-start-the-merge-agent-to-synchronize-a-push-subscription-to-a-merge-publication"></a>Para iniciar o Merge Agent para sincronizar uma assinatura push a uma publicação de mesclagem  
  
1.  Do prompt de comando ou do arquivo de lote no Distribuidor, execute **replmerg.exe**. Especifique os seguintes argumentos de linha de comando:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     Se você estiver usando Autenticação do SQL Server, deve-se também especificar os seguintes argumentos:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
###  <a name="TsqlExample"></a> Exemplos (agentes de replicação)  
 O exemplo seguinte inicia o Agente de Distribuição para sincronizar uma assinatura push.  
  
 
```
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksProductsTran  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4
```
  
 O exemplo a seguir inicia o Agente de Mesclagem para sincronizar uma assinatura push.  

```
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksSalesOrdersMerge  
  
REM -- Start the Merge Agent.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE"  -Publisher %Publisher%   
-Subscriber  %Subscriber%  -Distributor %Publisher% -PublisherDB  %PublicationDB%   
-SubscriberDB %SubscriptionDB% -Publication %Publication% -PublisherSecurityMode 1   
-OutputVerboseLevel 3  -Output -SubscriberSecurityMode 1  -SubscriptionType 0   
-DistributorSecurityMode 1
```
  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 É possível sincronizar as assinaturas push programaticamente usando o RMO (Replication Management Objects) e o acesso de código gerenciado para as funcionalidades do agente de replicação. As classes usadas para sincronizar uma assinatura push dependem do tipo de publicação ao qual a assinatura pertence.  
  
> [!NOTE]  
>  Se quiser iniciar uma sincronização que execute autonomamente sem afetar seu aplicativo, inicie o agente em modo assíncrono. Porém, se quiser monitorar o resultado da sincronização e receber retornos de chamada do agente durante o processo de sincronização (por exemplo, se quiser exibir a barra de andamento), inicie o agente de forma síncrona. Para os Assinantes do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] , você deve iniciar o agente de forma síncrona.  
  
#### <a name="to-synchronize-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para sincronizar uma assinatura push a um instantâneo ou publicação transacional  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransSubscription> e defina as propriedades a seguir:  
  
    -   O nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   O nome da publicação à qual a assinatura pertence para <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   O nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   O nome do Assinante para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   A conexão criada na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as demais propriedades do objeto. Se esse método retornar `false`, verifique se a assinatura existe.  
  
4.  Inicie o Distribution Agent no Distribuidor de uma das seguintes maneiras:  
  
    -   Chame o método <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizeWithJob%2A> na instância de <xref:Microsoft.SqlServer.Replication.TransSubscription> da etapa 2. Esse método inicia o Distribution Agent em modo assíncrono e o controle retorna imediatamente para o seu aplicativo enquanto o trabalho do agente está em execução. Você não poderá chamar este método se a assinatura foi criada com um valor de `false` para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>.  
  
    -   Obtenha uma instância de classe <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> da propriedade <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizationAgent%2A> , e chame o método <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> . Esse método inicia o agente de forma síncrona e o controle permanece com o trabalho do agente em execução. Durante a execução síncrona você pode manipular o evento <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> com o agente em execução.  
  
#### <a name="to-synchronize-a-push-subscription-to-a-merge-publication"></a>Para sincronizar uma assinatura push a uma publicação de mesclagem  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância de classe <xref:Microsoft.SqlServer.Replication.MergeSubscription> , e defina as propriedades a seguir:  
  
    -   O nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   O nome da publicação à qual a assinatura pertence para <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   O nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   O nome do Assinante para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   A conexão criada na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as demais propriedades do objeto. Se esse método retornar `false`, verifique se a assinatura existe.  
  
4.  Inicie o Merge Agent no Distribuidor de uma das seguintes maneiras:  
  
    -   Chame o método <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizeWithJob%2A> na instância de <xref:Microsoft.SqlServer.Replication.MergeSubscription> da etapa 2. Esse método inicia o Merge Agent em modo assíncrono e o controle retorna imediatamente para o seu aplicativo enquanto o trabalho do agente está em execução. Você não poderá chamar este método se a assinatura foi criada com um valor de `false` para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>.  
  
    -   Obtenha uma instância de classe <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> da propriedade <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizationAgent%2A> , e chame o método <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> . Esse método inicia o Merge Agent de forma síncrona e o controle permanece com o trabalho do agente em execução. Durante execução síncrona, você pode manipular o evento <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> enquanto o agente está em execução.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Este exemplo sincroniza a assinatura push a uma publicação transacional, onde o agente é iniciado de forma assíncrona usando o trabalho do agente.  
  
 [!code-csharp[HowTo#rmo_SyncTranPushSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpushsub_withjob)]  
  
 Este exemplo sincroniza a assinatura push a uma publicação transacional, onde o agente é iniciado de forma síncrona.  
  
 [!code-csharp[HowTo#rmo_SyncTranPushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpushsub)]  
  
 Este exemplo sincroniza a assinatura push a uma publicação de mesclagem, onde o agente é iniciado de forma assíncrona usando o trabalho do agente.  
  
 [!code-csharp[HowTo#rmo_SyncMergePushSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepushsub_withjob)]  
  
 Este exemplo sincroniza a assinatura push a uma publicação de mesclagem, onde o agente é iniciado de forma síncrona.  
  
 [!code-csharp[HowTo#rmo_SyncMergePushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepushsub)]  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos de objetos de gerenciamento de replicação](concepts/replication-management-objects-concepts.md)   
 [Sincronizar dados](synchronize-data.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)  
  
  
