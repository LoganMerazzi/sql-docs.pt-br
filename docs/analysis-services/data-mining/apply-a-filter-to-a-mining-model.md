---
title: Aplicar um filtro a um modelo de mineração | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5430aa0125e621a574d8fb9cc6b28f6b73794b46
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68184449"
---
# <a name="apply-a-filter-to-a-mining-model"></a>Aplicar um filtro a um modelo de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se a sua estrutura de mineração tiver uma tabela aninhada, você poderá aplicar um filtro à tabela de casos, à tabela aninhada ou a ambas.  
  
 O procedimento a seguir indica como criar os dois tipos de filtros: filtros de caso e filtros nas linhas da tabela aninhada.  
  
 A condição na tabela de casos restringe os clientes àqueles com renda entre 30000 e 40000. A condição na tabela aninhada restringe os clientes àqueles que não compraram um item específico.  
  
 A condição completa do filtro criada neste exemplo é a seguinte:  
  
```  
[Income] > '30000'   
AND  [Income] < '40000'   
AND EXISTS (SELECT * FROM [<nested table name>]   
WHERE [Model] <> 'Water Bottle' )   
```  
  
### <a name="to-create-a-case-filter-on-a-mining-model"></a>Para criar um filtro de caso em um modelo de mineração  
  
1.  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no Gerenciador de Soluções, clique na estrutura de mineração que contém o modelo de mineração a filtrar.  
  
2.  Clique na guia **Modelos de Mineração** .  
  
3.  Selecione o modelo, e clique com o botão direito do mouse para abrir o menu de atalho.  
  
     - ou -  
  
     Selecione o modelo. Em seguida, no menu **Modelo de Mineração** , selecione **Definir Filtro de Modelos**.  
  
4.  Na caixa de diálogo **Filtro de Modelos** , clique na linha superior da grade, na caixa de texto **Coluna da Estrutura de Mineração** .  
  
5.  Se a fonte de dados tiver uma tabela simples, a listagem suspensa exibirá somente os nomes das colunas nessa tabela.  
  
     Se a estrutura de mineração tiver várias tabelas, a lista mostrará os nomes das tabelas de origem. Os nomes de coluna não são exibidos enquanto não for selecionada uma tabela.  
  
     Se a sua estrutura de mineração tiver uma tabela de casos e uma tabela aninhada, a listagem suspensa indicará as colunas da tabela de casos e o nome da tabela aninhada.  
  
6.  Selecione uma coluna na lista suspensa.  
  
     O ícone no lado esquerdo da caixa de texto muda para indicar que o item selecionado é uma tabela ou uma coluna.  
  
7.  Clique na caixa de texto **Operador** e selecione um operador na lista. Os operadores válidos são alterados dependendo do tipo de dados da coluna que você selecionou.  
  
8.  Clique na caixa de texto **Valor** e digite um valor na caixa.  
  
     Por exemplo, selecione **Renda** como coluna, selecione o operador maior que (>) e digite **30000**.  
  
9. Na grade, clique na linha seguinte.  
  
     A condição do filtro que você criou é automaticamente adicionada à caixa de texto Expressão. Por exemplo, `[Income] > '30000'`  
  
10. Clique na caixa de texto **AND/OR** na linha seguinte da grade para adicionar uma condição.  
  
     Por exemplo, para criar uma condição BETWEEN, selecione **AND** na lista suspensa de operandos lógicos.  
  
11. Selecione um operador e digite um valor conforme descrito nas etapas 7 e 8.  
  
     Por exemplo, selecione novamente **Renda** como coluna, selecione o operador menor que (<) e digite **40000**.  
  
12. Na grade, clique na linha seguinte.  
  
13. A condição de filtro na caixa de texto Expressão é atualizada automaticamente para incluir a nova condição. A expressão completa é a seguinte: `[Income] > '30000'AND [Income] < '40000'`  
  
### <a name="to-add-a-filter-on-the-nested-table-in-a-mining-model"></a>Para adicionar um filtro na tabela aninhada em um modelo de mineração  
  
1.  No  **\<nome > filtro de modelos** caixa de diálogo, clique em uma linha vazia na grade, em **coluna da estrutura de mineração**.  
  
2.  Selecione o nome da tabela aninhada na lista suspensa.  
  
     O ícone no lado esquerdo da caixa de texto muda para indicar que o item selecionado é o nome de uma tabela.  
  
3.  Clique na caixa de texto **Operador** e selecione **Contém** ou **Não Contém**.  
  
     Essas são as únicas condições disponíveis para a tabela aninhada na caixa de diálogo **Filtro de Modelos** , pois você está restringindo a tabela de casos a apenas aqueles que têm um determinado valor na tabela aninhada. Você definirá o valor da condição na tabela aninhada na próxima etapa.  
  
4.  Clique o **valor** caixa e, em seguida, clique no **(...)**  botão para criar uma expressão.  
  
     O  **\<nome > filtro** caixa de diálogo é aberta. Essa caixa de diálogo só pode definir condições na tabela atual, que neste caso é a tabela aninhada.  
  
5.  Clique na caixa **Coluna da Estrutura de Mineração** e selecione o nome de coluna nas listas suspensas das colunas da tabela aninhada.  
  
6.  Clique em **Operador** e selecione um operador na lista de operadores válidos para a coluna.  
  
7.  Clique em **Valor** e digite um valor.  
  
     Por exemplo, para **Coluna da Estrutura de Mineração** selecione **Modelo**. Para **Operador**, selecione **<>** e digite o valor **Garrafa de Água**. Essa condição cria a seguinte expressão de filtro:  
  
```  
EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] <> 'Water Bottle' )   
```  
  
> [!NOTE]  
>  Como o número de atributos da tabela aninhada é potencialmente ilimitado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não fornece a lista dos possíveis valores a serem selecionados. Você deve digitar o valor exato. Você não pode usar um operador LIKE em uma tabela aninhada.  
  
1.  Adicione mais condições conforme a necessidade, combinando as condições ao selecionar **AND** ou **OR** na caixa **AND/OR** à esquerda da grade **Condições** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
2.  Na caixa de diálogo **Filtro de Modelos** , examine as condições que você criou usando a caixa de diálogo **Filtro** . As condições para a tabela aninhada são acrescentadas às condições da tabela de casos, e o conjunto completo das condições de filtro é exibido na caixa de texto **Expressão** .  
  
3.  Se desejar, clique em **Editar Consulta** para alterar manualmente a expressão de filtro.  
  
    > [!NOTE]  
    >  Se você alterar manualmente qualquer parte da expressão de filtro, a grade será desabilitada e, assim sendo, você deverá trabalhar com a expressão de filtro apenas no modo de edição de texto. Para restaurar o modo de edição da grade, você deve apagar a expressão de filtro e iniciar novamente.  
  
## <a name="see-also"></a>Consulte também  
 [Filtros para modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Excluir um filtro de um modelo de mineração](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)  
  
  
