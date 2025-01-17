---
title: Revisando propriedades de dimensão e cubo | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 97b12ad51affaebb87f152938bdfbfae16bd8900
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403728"
---
# <a name="lesson-2-4---reviewing-cube-and-dimension-properties"></a>Lição 2-4 – propriedades de dimensão e revisando o cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Depois que você definir um cubo, você pode revisar os resultados usando o Designer de Cubos. Na tarefa a seguir, você revisará a estrutura do cubo no projeto do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
### <a name="to-review-cube-and-dimension-properties-in-cube-designer"></a>Para revisar as propriedades de cubo e dimensão no Designer de Cubo  
  
1.  Para abrir o Designer de Cubo, clique duas vezes no cubo do **Tutorial do Analysis Services** no nó **Cubos** do Gerenciador de Soluções.  
  
2.  No painel **Medidas** da guia **Estrutura do Cubo** do Designer de Cubo, expanda o grupo de medidas **Vendas pela Internet** para exibir as medidas definidas.  
  
    Você pode alterar a ordem arrastando as medidas para que ordem desejada. A ordem que você cria afeta o modo como determinados aplicativos cliente ordenarão essas medidas. O grupo de medidas e cada medida que ele contém têm propriedades que podem ser editadas na janela Propriedades.  
  
3.  No painel **Dimensões** da guia **Estrutura do Cubo** no Designer de Cubo, revise as dimensões do cubo do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
    Observe que, apesar de somente três dimensões terem sido criadas no nível do banco de dados, como exibido no Gerenciador de Soluções, há cinco dimensões de cubo no cubo do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O cubo contém mais dimensões que o banco de dados. Isso acontece porque a dimensão do banco de dados Data é usada como base para três dimensões de cubo diferentes relacionadas a data, com base em fatos diferentes relacionados ao tempo na tabela de fatos. Essas dimensões relacionadas a data também são chamadas de *dimensões com função múltipla*. As três dimensões de cubo relacionadas a data permitem que os usuários dimensionem o cubo por três fatos distintos que estão relacionados a cada venda de produto: a data de pedido do produto, a data de vencimento para preenchimento do pedido e a data de remessa do pedido. Ao reutilizar uma única dimensão de banco de dados para várias dimensões de cubo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] simplifica o gerenciamento da dimensão, usa menos espaço em disco e reduz o tempo de processamento total.  
  
4.  No painel **Dimensões** da guia **Estrutura do Cubo** , expanda **Cliente**e depois clique em **Editar Cliente** para abrir a dimensão no Designer de Dimensão.  
  
    Designer de dimensão contém as seguintes guias: **Estrutura da dimensão**, **relações de atributo**, **traduções**, e **navegador**. Observe que o **estrutura da dimensão** guia inclui três painéis: **Atributos**, **hierarquias**, e **exibição da fonte de dados**. Os atributos da dimensão são exibidos no painel **Atributos** . Para obter mais informações, consulte [Referência de propriedades de atributo de dimensão](../multidimensional-models/dimension-attribute-properties-reference.md), [Criar hierarquias definidas pelo usuário](../multidimensional-models/user-defined-hierarchies-create.md) e [Definir relações de atributo](../multidimensional-models/attribute-relationships-define.md).  
  
5.  Para mudar para o Designer de Cubo, clique com o botão direito do mouse no cubo do **Tutorial do Analysis Services** do nó **Cubos** do Gerenciador de Soluções e clique em **Designer de Exibição**.  
  
6.  No Designer de Cubo, clique na guia **Uso da Dimensão** .  
  
    Nessa exibição do cubo do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode ver as dimensões do cubo que são usadas pelo grupo de medidas Vendas pela Internet. Além disso, você pode definir um tipo de relação entre cada dimensão e cada grupo de medidas no qual ela é usada.  
  
7.  Clique na guia **Partições** .  
  
    O Assistente para Cubos define uma partição única para o cubo, usando o modo de armazenamento MOLAP (processamento analítico online multidimensional) sem agregações. Com o MOLAP, todos os dados de nível folha e todas as agregações são armazenadas dentro do cubo para obter desempenho máximo. As agregações são resumos pré-calculados de dados que melhoram o tempo de resposta de consultas, pois têm respostas antes que as perguntas sejam feitas. Você pode definir partições adicionais, configurações de armazenamento e configurações write-back na guia **Partições** . Para obter mais informações, consulte [Partições &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md) e [Agregações e designs de agregação](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
8.  Clique na guia **Navegador** .  
  
    Observe que o cubo não pode ser navegado porque ainda não foi implantado em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Nesse momento, o cubo no projeto do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é apenas uma definição de um cubo que você pode implantar em qualquer instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Ao implantar e processar um cubo, você cria objetos definidos em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e preenche esses objetos com dados das fontes de dados subjacentes.  
  
9. No Gerenciador de Soluções, clique com o botão direito do mouse no **Tutorial do Analysis Services** do nó **Cubos** e clique em **Exibir Código**. Talvez você precise esperar um pouco.  
  
    O código XML do cubo do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é exibido na guia **[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Tutorial.cube [XML]** . Esse é o código real usado para criar o cubo em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durante a implantação. Para obter mais informações, consulte [Exibir o XML de um projeto do Analysis Services &#40;SSDT&#41;](../multidimensional-models/view-the-xml-for-an-analysis-services-project-ssdt.md).  
  
10. Feche a guia do código XML.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Implantando um projeto do Analysis Services](lesson-2-5-deploying-an-analysis-services-project.md)  
  
## <a name="see-also"></a>Consulte também  
[Procurar dados de dimensão no Designer de Dimensão](../multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)  
  
  
  
