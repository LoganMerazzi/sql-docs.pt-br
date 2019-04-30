---
title: Criando uma estrutura de cesta de compras e um modelo (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 659b7a4e-f687-44d9-a60a-86490ccbf90f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 207d82f740b7b5ff174e220e647d67d5bac7f9ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63190836"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>Criando uma estrutura e um modelo de cesta de compras (Tutorial de mineração de dados intermediário)
  Agora que você criou uma exibição da fonte de dados, usará o Assistente de Mineração de Dados para criar uma nova estrutura de mineração. Nesta tarefa, você criará uma estrutura de mineração e um modelo de mineração baseado no algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association.  
  
> [!NOTE]  
>  Se você encontrar um erro indicando que vAssocSeqLineItems não pode ser usado como uma tabela aninhada, volte para a tarefa anterior da lição e crie a junção muitos para um, arrastando da tabela vAssocSeqLineItems (o lado muitos) para a tabela vAssocSeqOrders (o lado um). Você também pode editar a relação entre as tabelas, clicando com o botão direito em a linha de junção.  
  
### <a name="to-create-an-association-mining-structure"></a>Para criar uma estrutura de mineração de associação  
  
1.  No Gerenciador de soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique com botão direito **estruturas de mineração** e selecione **nova estrutura de mineração** para abrir o Assistente de mineração de dados.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  No **Selecionar método de definição** página, verifique **de warehouse existente de banco de dados ou dados relacional** está selecionado e, em seguida, clique em **próxima**.  
  
4.  Sobre o **criar a estrutura de mineração de dados** página, em **qual técnica de mineração de dados você deseja usar?**, selecione **regras de associação da Microsoft** na lista e, em seguida, clique **Próxima**. O **Selecionar exibição da fonte de dados** página será exibida.  
  
5.  Selecione **pedidos**sob **modos de exibição de fonte de dados disponíveis**e, em seguida, clique em **próxima**.  
  
6.  No **especificar tipos de tabela** página, na linha para a tabela vAssocSeqLineItems, selecione o **Nested** caixa de seleção e, na linha para a tabela aninhada vAssocSeqOrders, selecione o **caso** caixa de seleção. Clique em **Avançar**.  
  
7.  Sobre o **especificar os dados de treinamento** página, desmarque qualquer caixa que possam ser verificada. Defina a chave para a tabela de casos vAssocSeqOrders, marcando a **chave** caixa de seleção ao lado de OrderNumber.  
  
     Como é o objetivo da análise de cesta de compras determinar quais produtos estão incluídos em uma única transação, você não precisa usar o **CustomerKey** campo.  
  
8.  Defina a chave para a tabela aninhada, vAssocSeqLineItems, marcando a **chave** caixa de seleção ao lado do modelo. O **entrada** caixa de seleção é marcada automaticamente quando você fizer isso. Selecione o **previsível** caixa de seleção `Model` também.  
  
     Em um modelo de cesta de compras, você não se importam a sequência de produtos no carrinho de compras e, portanto, você não deve incluir **LineNumber** como uma chave para a tabela aninhada. Você usaria **LineNumber** como uma chave somente em um modelo em que a sequência é importante. Você criará um modelo que use o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering na Lição 4.  
  
9. Marque a caixa de seleção à esquerda de IncomeGroup e de Região, mas não faça outras seleções. Verificar a coluna mais à esquerda adiciona as colunas à estrutura para referência futura, mas as colunas não serão usadas no modelo. As suas seleções deverão ficar assim:  
  
     ![como a caixa de diálogo deve parecer](../../2014/tutorials/media/tutorial-configassocmodel.gif "deve ser a aparência de caixa de diálogo")  
  
10. Clique em **Avançar**.  
  
11. Sobre o **colunas especificar conteúdo e tipo de dados**, examine as seleções, que devem ser conforme mostrado na tabela a seguir e, em seguida, clique em **próxima**.  
  
    |Colunas|Tipo de Conteúdo|Tipo de Dados|  
    |-------------|------------------|---------------|  
    |IncomeGroup|Discreto|Text|  
    |Número do pedido|Chave|Text|  
    |Região|Discreto|Text|  
    |vAssocSeqLineItems|||  
    |Modelo|Chave|Text|  
  
12. No **criar o teste definido** página, o valor padrão para a opção **porcentagem de dados de teste** é 30 %). Altere-a para **0**. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece gráficos diferentes para medir a exatidão do modelo. No entanto, alguns tipos de gráfico de precisão, como o gráfico de comparação de precisão e o relatório de validação cruzada, foram criados para classificação e estimativa. Eles não são suportados para previsão associativa.  
  
13. Sobre o **Concluindo o assistente** página, na **nome da estrutura de mineração**, tipo `Association`.  
  
14. Na **nome do modelo de mineração**, tipo `Association`.  
  
15. Selecione a opção **Permitir drill-through**e, em seguida, clique em **concluir**.  
  
     Designer de mineração de dados é aberta para exibir o `Association` estrutura de mineração que você acabou de criar.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Modificando e processando o modelo de cesta de compras &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo Associação da Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Tipos de conteúdo &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  
