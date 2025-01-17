---
title: Replicação de mesclagem avançada – detecção e resolução de conflito | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- column-level conflict tracking
- row-level conflict tracking
- viewing merge replication conflicts
- resolving merge replication conflicts
- logical record-level conflict tracking [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ae61bdd59202db73b404bf2c639c2f1cee98e81f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058110"
---
# <a name="advanced-merge-replication---conflict-detection-and-resolution"></a>Replicação de mesclagem avançada – detecção e resolução de conflito
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando o Publicador e o Assinante estão conectados e ocorre a sincronização, o Agente de Mesclagem detecta se há algum conflito. Se forem detectados conflitos, o Agente de Mesclagem usará o resolvedor de conflitos (especificado quando um artigo é adicionado à publicação) para determinar quais dados serão aceitos e propagados para outros sites.  

 A replicação de mesclagem oferece uma variedade de métodos para detectar e resolver conflitos. Com relação à maioria dos aplicativos, o método padrão é apropriado.  
  
-   Se um conflito ocorrer entre um Publicador e um Assinante, a alteração do Publicador é mantida e a alteração do Assinante é descartada.   
-   Se ocorrer um conflito entre dois Assinantes que usam assinaturas de cliente (tipo padrão para assinaturas pull), a alteração do primeiro Assinante para sincronizar com o Publicador é mantida, e a alteração do segundo Assinante é descartada. Para obter informações sobre como especificar assinatura de cliente e servidor, consulte [Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md).   
-   Em caso de conflito entre dois Assinantes que usam assinaturas de servidor (tipo padrão para assinaturas push), a alteração do Assinante com o maior valor da prioridade será mantida, e a alteração do segundo Assinante será descartada. Se os valores de prioridade forem iguais, a alteração do primeiro Assinante a sincronizar com o Publicador será mantida.  
  
> [!NOTE]  
>  Embora o Assinante esteja sincronizado com o Publicador, os conflitos ocorrem normalmente entre as atualizações que são feitas em diferentes Assinantes, em vez de atualizações sendo feitas no Assinante e no Publicador.  
  
 O comportamento da detecção e resolução de conflitos depende das seguintes opções, descritas neste tópico:    
-   Especificação de controle em nível de coluna; controle em nível de linha ou controle em nível de registro lógico.    
-   Especificação do mecanismo padrão de resolução, com base na prioridade, ou especificação de um resolvedor de artigo. Um resolvedor de artigo pode ser:  
  
    -   Um *manipulador de lógica de negócios* escrito em código gerenciado.   
    -   Um *resolvedor personalizado*com base em COM.    
    -   Um resolvedor com base em COM fornecido pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
     Se o mecanismo de resolução padrão for usado, o comportamento será determinado posteriormente pelo tipo de assinatura usada: de cliente ou servidor.  
  
## <a name="conflict-detection"></a>Detecção de conflito  
 Se uma alteração de dados se qualifica ou não como conflito vai depender do tipo de controle de conflitos definido para o artigo:  
  
-   Quando o controle em nível de coluna for selecionado, ele será considerado conflito se as alterações forem feitas na mesma coluna, na mesma linha, em mais de um nó de replicação.    
-   Caso o controle em nível de linha seja selecionado, será considerado conflito se as alterações forem feitas em todas as colunas, na  mesma linha e em mais de um nó de replicação (não é necessário que as colunas afetadas nas linhas correspondentes sejam as mesmas).    
-   Caso o controle em nível de registro lógico seja selecionado, será considerado conflito se as alterações forem feitas em todas as linhas, no mesmo registro lógico e em mais de um nó de replicação (as colunas afetadas nas linhas correspondentes não precisam ser as mesmas).  
  
 Para obter mais informações, consulte [Detectando e resolvendo conflitos em registros lógicos](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
 Para especificar o acompanhamento de conflito e o nível de resolução para um artigo, confira [Especificar as propriedades de replicação de mesclagem](../../../relational-databases/replication/merge/specify-merge-replication-properties.md).  
  
## <a name="conflict-resolution"></a>Resolução de conflitos  
 Após a detecção de um conflito, o Agente de Mesclagem inicia o resolvedor do conflito selecionado e usa o resolvedor para determinar o vencedor do conflito. A linha vencedora é aplicada ao Publicador e ao Assinante, e os dados da linha perdedora são gravados em uma tabela de conflitos. Os conflitos estão resolvidos imediatamente após a execução do resolvedor, a menor que se opte por resolver conflitos de forma interativa.  

Resolver conflitos de replicação de mesclagem [!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando o Publicador e o Assinante estão conectados e ocorre a sincronização, o Agente de Mesclagem detecta se há algum conflito. Se houver conflitos detectados, o Agente de Mesclagem utiliza um resolvedor de conflitos para determinar quais dados serão aceitos e propagados para outros sites.  
  
> [!NOTE]  
>  Embora o Assinante esteja sincronizado com o Publicador, os conflitos ocorrem normalmente entre as atualizações feitas em diferentes Assinantes, em lugar de atualizações feitas no Assinante e no Publicador.  
  
 A replicação de mesclagem oferece uma variedade de métodos para detectar e resolver conflitos. Com relação à maioria dos aplicativos, o método padrão é apropriado.  
  
-   Se um conflito ocorrer entre um Publicador e um Assinante, a alteração do Publicador é mantida e a alteração do Assinante é descartada.  
  
-   Se ocorrer um conflito entre dois Assinantes que usam assinaturas de cliente (tipo padrão para assinaturas pull), a alteração do primeiro Assinante para sincronizar com o Publicador é mantida, e a alteração do segundo Assinante é descartada. Para obter informações sobre como especificar assinatura de cliente e servidor, consulte [Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
-   Em caso de conflito entre dois Assinantes que usam assinaturas de servidor (tipo padrão para assinaturas push), a alteração do Assinante com o maior valor da prioridade será mantida, e a alteração do segundo Assinante será descartada. Se os valores de prioridade forem iguais, a alteração do primeiro Assinante a sincronizar com o Publicador será mantida.  
  
 Para obter mais informações sobre a detecção de conflito e resolução para replicação de mesclagem, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### <a name="resolver-types"></a>Tipos de resolvedores  
 Na replicação de mesclagem, a resolução de conflitos ocorre no âmbito do artigo. Com relação às publicações compostas de vários artigos, pode haver diferentes resolvedores de conflitos servindo diferentes artigos ou um único resolvedor de conflitos servindo um artigo, vários artigos ou todos os artigos contidos em uma publicação.  
  
 Se o plano é usar o resolvedor padrão de conflitos com base na prioridade, não é necessário definir a propriedade de resolvedor de um artigo. Para usar um resolvedor de artigos em vez do resolvedor padrão, é preciso definir a propriedade do resolvedor do artigo a ser usado, selecionando um resolvedor disponível no Publicador. Quaisquer informações específicas que precisem ser passadas ao resolvedor podem igualmente ser especificadas na propriedade de informações do resolvedor.  
  
 A replicação de mesclagem oferece quatro tipos de resolvedores de conflito:  
  
-   O resolvedor de conflito padrão com base em prioridade  
  
     O mecanismo de resolução padrão comporta-se de forma diferente, dependendo se a assinatura for uma assinatura de cliente ou uma assinatura de servidor. Valores de prioridade são atribuídos a Assinantes individuais que usam as assinaturas de servidor; as alterações feitas no nó com a mais alta prioridade vencem todos os conflitos. Para assinaturas de cliente, a primeira alteração gravada no Publicador vence o conflito.  
  
     Após a criação de uma assinatura, ela não pode ser alterada de um tipo para outro.  
  
-   Manipulador de lógica de negócios  
  
     A estrutura do manipulador de lógica comercial permite que você grave um assembly de código gerenciado que é chamado durante o processo de sincronização de mesclagem. O assembly inclui a lógica comercial que pode corresponder a conflitos e a uma série de outras condições durante a sincronização. Para obter mais informações, consulte [Executar lógica de negócios durante a sincronizações de mesclagem](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
-   Resolvedor personalizado baseado em COM  
  
     A replicação de mesclagem founece uma API para escrever resolvedoues como objetos COM em linguagens, como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. Para obter mais informações, consulte [COM-Based Custom Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
-   Resolvedor baseado em COM fornecido pela [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
     O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inclui vários resolvedores baseados em COM. Para obter mais informações, consulte [Resolvedores Microsoft baseados em COM](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 Para mais informações sobre como selecionar um tipo adequado de resolvedor, consulte [Escolher um resolvedor](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-choose-a-resolver.md).  
  
> [!NOTE]  
>  Alguns resolvedores de artigo são escritos para controlar conflitos apenas em determinadas operações. Por exemplo, um resolvedor poderia controlar atualizações, mas não inserções ou exclusões. O solucionador de conflito padrão baseado em prioridade controla todos os conflitos não controlados pelo resolvedor de artigo.  
  
 Para especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflito, consulte  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Especificar um tipo de assinatura de mesclagem e a prioridade da resolução de conflitos &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)  
  
-   Programação de replicação do [!INCLUDE[tsql](../../../includes/tsql-md.md)] e programação do RMO (Replication Management Objects): [Criar uma assinatura pull](../../../relational-databases/replication/create-a-pull-subscription.md) e [Criar uma assinatura push](../../../relational-databases/replication/create-a-push-subscription.md)  
  
### <a name="interactive-resolver"></a>Resolvedor Interativo  
 A replicação fornece uma interface de usuário de Resolvedor Interativo que pode ser usada tanto em conjunto com o resolvedor padrão de conflitos, baseado em prioridade, como com o resolvedor de artigo. Ao realizar a sincronização sob demanda por meio do Gerenciador de Sincronização do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, o Resolvedor Interativo exibe os dados do conflito em tempo real e permite que se opte pela forma de resolução dos conflitos. Para obter mais informações sobre como ativar resolução interativa e iniciar o Resolvedor Interativo, consulte [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
## <a name="viewing-conflicts"></a>Exibindo conflitos  
 A forma mais objetiva de exibir conflitos é usar o Visualizador de Conflitos de Replicação, disponível no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também fornece procedimentos armazenados que permitem a consulta de tabelas em conflito). O Visualizador de Conflitos e o Resolvedor Interativo são ferramentas semelhantes, mas o Resolvedor Interativo permite resolver conflitos à medida que a sincronização ocorre, enquanto o Visualizador de Conflitos foi projetado para exibir os conflitos após eles terem sido resolvidos. Se os metadados de conflito ainda estiverem disponíveis nas tabelas do sistema (metadados de conflito são retidos por 14 dias, por padrão), será possível substituir os resultados da resolução de conflitos no Visualizador de Conflitos; contudo, se a intervenção direta for necessária de maneira regular, o melhor será usar o Resolvedor Interativo.  
  
> [!NOTE]  
>  Não são exibidos conflitos que envolvem registros lógicos no Visualizador de Conflitos. Para exibir informações sobre esses conflitos, use procedimentos armazenados de replicação. Para obter mais informações, consulte [Exibir informações sobre conflitos em publicações de mesclagem &#40;Programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
 O Visualizador de Conflitos exibe informações de três tabelas do sistema:  
  
-   A replicação cria uma tabela de conflitos para cada tabela em um artigo de mesclagem, com um nome na forma **MSmerge_conflict_\<PublicationName>_\<ArticleName>** .  
  
     As tabelas de conflitos têm a mesma estrutura das tabelas em que foram baseadas. Uma linha em uma dessas tabelas consiste na versão perdedora de uma linha de conflito (a versão vencedora da linha fica na tabela real do usuário).  
  
-   A tabela **MSmerge_conflicts_info** fornece informações sobre cada conflito, inclusive o tipo de conflito.  
  
-   A tabela **sysmergearticles** identifica quais tabelas de usuário têm tabelas de conflitos e fornecem informações sobre as tabelas de conflitos.  
  
 Por padrão, as informações sobre conflitos são armazenadas:  
  
-   No Publicador e no Assinante, caso o nível de compatibilidade da publicação for 90RTM ou superior.  
  
-   No Publicador, caso o nível de compatibilidade da publicação seja inferior a 80RTM.  
  
-   No Publicador, caso os Assinantes estejam executando [!INCLUDE[ssEW](../../../includes/ssew-md.md)]. Os dados de conflito não podem ser armazenados nos Assinantes do [!INCLUDE[ssEW](../../../includes/ssew-md.md)] .  
  
 **Para exibir conflitos**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Exibir e resolver conflitos de dados em publicações de mesclagem &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   Programação de replicação do [!INCLUDE[tsql](../../../includes/tsql-md.md)]: [Exibir informações sobre conflitos para publicações de mesclagem &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Sincronizar dados](../../../relational-databases/replication/synchronize-data.md)  
  
  
