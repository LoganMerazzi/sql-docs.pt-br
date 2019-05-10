---
title: 'Lição 6: Definindo cálculos | Microsoft Docs'
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e4b4dbae844177fe121fcf1b22f4f6bf68c8584
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403878"
---
# <a name="lesson-6-defining-calculations"></a>Lição 6: Como definir cálculos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Nesta lição, você aprenderá a definir cálculos, que são scripts ou expressões MDX (Multidimensional Expressions). Os cálculos permitem que você defina membros calculados, conjuntos nomeados ou execute outros comandos de script para aumentar os recursos de um cubo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por exemplo, você pode executar um comando de script para definir um subcubo e depois atribuir um cálculo às células no subcubo.  
  
Ao definir um novo cálculo no Designer de Cubo, o cálculo é adicionado ao painel **Organizador de Script** da guia **Cálculos** do Designer de Cubo, e os campos deste tipo específico de cálculo são exibidos em um formulário de cálculos no painel **Expressões de Cálculo** . Os cálculos são executados na ordem em que estão listados no painel **Organizador de Script** . Você pode reordenar os cálculos clicando com o botão direito do mouse em um cálculo específico e selecionando **Mover para Cima** ou **Mover para Baixo**, ou clicando em cálculo específico e usando os ícones **Mover para Cima** ou **Mover para Baixo** na barra de ferramentas da guia **Cálculos** .  
  
Na guia **Cálculos** , você pode adicionar novos cálculos e exibir ou editar cálculos existentes nas seguintes exibições do painel **Expressões de Cálculo** :  
  
-   Exibição de formulário. Esta exibição mostra as expressões e propriedades de um único comando em um formato gráfico. Quando você edita um script MDX, uma caixa de expressão preenche a exibição Formulário.  
  
-   Exibição de script. Esta exibição mostra todos os scripts de cálculo em um editor de código que permite alterar os scripts de cálculo facilmente. Quando o painel **Expressões de Cálculo** está na Exibição de script, o **Organizador de Script** fica oculto. A Exibição de script fornece codificação por cor, correspondência de parênteses, preenchimento automático e regiões de código MDX. Você pode expandir ou recolher as regiões de código MDX para facilitar a edição.  
  
Para alternar entre esses exibições no painel **Expressões de Cálculo** , clique em **Exibição de Formulário** ou **Exibição de Script** na barra de ferramentas da guia **Cálculos** .  
  
> [!NOTE]  
> Se o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] detectar um erro de sintaxe em qualquer cálculo, a Exibição de formulário não será exibida até que o erro seja corrigido na Exibição de script.  
  
Você também pode usar o Assistente de Business Intelligence para adicionar determinados cálculos a um cubo. Por exemplo, você pode usar esse assistente para adicionar inteligência de tempo a um cubo, o que significa definir membros calculados para cálculos relacionados ao tempo como período até esta data, médias de movimentação ou crescimento de período sobre período. Para obter mais informações, consulte [Definir cálculos de inteligência de tempo com o Assistente de Business Intelligence](../multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md).  
  
> [!IMPORTANT]  
> Na guia **Cálculos** , o script de cálculo inicia com o comando CALCULATE. O comando CALCULATE controla a agregação das células do cubo e deve ser editado apenas se você pretender especificar manualmente como as células do cubo devem ser agregadas.  
  
Para obter mais informações, consulte [Cálculos](../multidimensional-models-olap-logical-cube-objects/calculations.md)e [Cálculos em modelos multidimensionais](../multidimensional-models/calculations-in-multidimensional-models.md).  
  
> [!NOTE]  
> Projetos concluídos de todas as lições deste tutorial estão disponíveis online. Você pode avançar para qualquer lição com o uso do projeto concluído na lição anterior como um ponto de partida. [Clique aqui](http://go.microsoft.com/fwlink/?LinkID=221866) para baixar os projetos de exemplo fornecidos com este tutorial.  
  
Esta lição contém as seguintes tarefas:  
  
[Definindo membros calculados](lesson-6-1-defining-calculated-members.md)  
Nesta tarefa, você aprenderá a definir membros calculados.  
  
[Definindo conjuntos nomeados](lesson-6-2-defining-named-sets.md)  
Nesta tarefa, você aprenderá a definir conjuntos nomeados.  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 7: Definindo indicadores chave de desempenho &#40;KPIs&#41;](lesson-7-defining-key-performance-indicators-kpis.md)  
  
## <a name="see-also"></a>Consulte também  
[Cenário do tutorial de Analysis Services](analysis-services-tutorial-scenario.md)  
[Criar conjuntos nomeados](../multidimensional-models/create-named-sets.md)  
[Criar membros calculados](../multidimensional-models/create-calculated-members.md)  
  
  
  
