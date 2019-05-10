---
title: Mover membros dentro de uma hierarquia (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 160c3ab39c09d6c0ecd9517a270e770bde118751
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65478955"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>Mover membros dentro de uma hierarquia (Master Data Services)
  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], mova os membros dentro de uma hierarquia para alterar seu local ou atribuição pai.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Para hierarquias explícitas, você deve ter um mínimo de **atualização** permissão à entidade.  
  
-   Para hierarquias derivadas, você deve ter um mínimo de **atualização** para o modelo e para quaisquer atributos baseados em domínio usados na hierarquia.  
  
### <a name="to-move-members-within-a-hierarchy"></a>Para mover membros dentro de uma hierarquia  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista **Modelo** , selecione um modelo.  
  
2.  Na lista **Versão** , selecione uma versão.  
  
3.  Clique em **Gerenciador**.  
  
4.  Na barra de menus, aponte para **hierarquias** e clique em *hierarchy_name*.  
  
5.  No **hierarquia** painel, em que a hierarquia é exibida em uma estrutura de árvore, clique na caixa de seleção para cada membro que você deseja mover.  
  
6.  Na parte superior do **hierarquia** painel, clique em **Recortar**.  
  
7.  No **hierarquia** painel, clique na caixa de seleção para o membro que você deseja mover os membros.  
  
8.  Clique em **colar**.  
  
    > [!NOTE]  
    >  Em hierarquias derivadas, você somente pode mover os membros para o mesmo nível. Além disso, não pode alterar a ordem de classificação dos membros.  
  
## <a name="see-also"></a>Consulte também  
 [Mover membros de hierarquia explícita por meio do processo de preparo &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Hierarquias derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [Hierarquias explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
