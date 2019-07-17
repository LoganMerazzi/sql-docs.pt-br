---
title: Criar e gerenciar hierarquias em modelos tabulares do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e785fe0e4a5f0030beceff7b9393932a29eaa52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163021"
---
# <a name="create-and-manage-hierarchies"></a>Criar e gerenciar hierarquias 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  As hierarquias podem ser criadas e gerenciadas no designer modelo em Exibição de Diagrama. Par exibir o designer de modelos na Exibição de Diagrama no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Model** , aponte para **Exibição de Modelo**e clique em **Exibição de Diagrama**.  
  
 Este artigo inclui as seguintes tarefas:  
  
-   [Criar uma hierarquia](#bkmk_create)  
  
-   [Editar uma hierarquia](#bkmk_edit)  
  
-   [Excluir uma hierarquia](#bkmk_delete)  
  
##  <a name="bkmk_create"></a> Criar uma hierarquia  
 Você pode criar uma hierarquia usando as colunas e o menu de contexto de tabela. Quando você criar uma hierarquia, um novo nível pai é exibido com as colunas selecionadas como níveis filho.  
  
#### <a name="to-create-a-hierarchy-from-the-context-menu"></a>Para criar uma hierarquia no menu de contexto  
  
1.  No designer modelo (Exibição de Diagrama), em uma janela de tabela, clique com o botão direito do mouse em uma coluna e clique em **Criar Hierarquia**.  
  
     Para selecionar várias colunas, clique em cada coluna, clique com o botão direito do mouse para abrir o menu de contexto e clique em **Criar Hierarquia**.  
  
     Um nível de hierarquia pai é criado na parte inferior da janela da tabela e as colunas selecionadas são copiadas sob a hierarquia como níveis filho.  
  
2.  Digite um nome para a hierarquia.  
  
 Você pode arrastar colunas adicionais para o nível pai da sua hierarquia, que copia as colunas. Remova o nível filho para colocá-lo onde você desejar que ele seja exibido na hierarquia.  
  
> [!NOTE]  
>  O comando Criar Hierarquia estará desabilitado no menu de contexto se você fizer multisseleção de uma medida junto com uma ou mais colunas, ou se você selecionar colunas de várias tabelas.  
  
##  <a name="bkmk_edit"></a> Editar uma hierarquia  
 Você pode renomear uma hierarquia, renomear um nível filho, alterar a ordem dos níveis filho, adicionar colunas adicionais como níveis filho, remover um nível filho de uma hierarquia, mostrar o nome de origem de um nível filho (o nome da coluna) e ocultar um nível filho se tiver o mesmo nome como o nível pai da hierarquia.  
  
#### <a name="to-change-the-name-of-a-hierarchy-or-child-level"></a>Para alterar o nome de uma hierarquia ou nível filho  
  
1.  Clique com o botão direito do mouse no nível pai ou nível filho da hierarquia e clique em **Renomear**.  
  
2.  Digite um novo nome ou edite o nome existente.  
  
#### <a name="to-change-the-order-of-a-child-level-in-a-hierarchy"></a>Para alterar a ordem de um nível filho em uma hierarquia  
  
-   Clique e arraste um nível filho para uma nova posição na hierarquia.  
  
-   Ou clique com o botão direito em um nível filho da hierarquia e clique em Mover para Cima para mover o nível na lista ou clique em Mover para Baixo para mover para baixo na lista.  
  
-   Ou clique em um nível filho para selecioná-lo e pressione Alt + Seta para Cima para mover o nível para cima, ou pressione Alt + Seta para Baixo para mover o nível para baixo na lista.  
  
#### <a name="to-add-another-child-level-to-a-hierarchy"></a>Para adicionar outro nível filho a uma hierarquia  
  
-   Clique e arraste uma coluna para o nível pai ou um local específico da hierarquia. A coluna é copiada como um nível filho da hierarquia.  
  
-   Ou clique com o botão direito do mouse em uma coluna, aponte para **Adicionar à Hierarquia**e clique na hierarquia.  
  
> [!NOTE]  
>  Você pode adicionar uma coluna oculta (uma coluna que é oculta de relatórios) como um nível filho à hierarquia. O nível filho não está oculto.  
  
#### <a name="to-remove-a-child-level-from-a-hierarchy"></a>Para remover um nível filho de uma hierarquia  
  
-   Clique com o botão direito do mouse no nível filho e clique em **Remover da Hierarquia**.  
  
-   Ou clique no nível filho e pressione **Excluir**.  
  
> [!NOTE]  
>  Se você renomear um nível filho da hierarquia, ele não mais terá o mesmo nome que a coluna da qual foi copiado. Use o comando **Mostrar Nome de Origem** para ver de qual coluna ela foi copiada.  
  
#### <a name="to-show-a-source-name"></a>Para mostrar um nome de origem  
  
-   Clique com o botão direito do mouse no nível filho da hierarquia e clique em **Show Source Name (Mostrar Nome de Origem)** . O nome da coluna da qual ela foi copiada é exibido.  
  
##  <a name="bkmk_delete"></a> Excluir uma hierarquia  
  
#### <a name="to-delete-a-hierarchy-and-remove-its-child-levels"></a>Para excluir uma hierarquia e remover seus níveis filho  
  
-   Clique com o botão direito no nível pai da hierarquia e clique em Excluir Hierarquia.  
  
-   Ou clique no nível pai da hierarquia e pressione Excluir. Isto também remove todos os níveis filho.  
  
## <a name="see-also"></a>Consulte também  
 [Designer de modelo tabular](../../analysis-services/tabular-models/tabular-model-designer-ssas.md)   
 [Hierarquias](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)   
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)  
  
  
