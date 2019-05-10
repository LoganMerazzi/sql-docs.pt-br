---
title: 'Lição 5: Criar colunas calculadas | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df9b5a6d490b33b9aea786290acb7454d0066453
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404178"
---
# <a name="lesson-5-create-calculated-columns"></a>Lição 5: Criar colunas calculadas
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará novos dados no modelo adicionando colunas calculadas. Uma coluna calculada se baseia nos dados que já existem no modelo. Para obter mais informações, consulte [colunas calculadas](../tabular-models/ssas-calculated-columns.md).  
  
Você criará cinco novas colunas calculadas em três tabelas diferentes. As etapas são ligeiramente diferentes para cada tarefa. O objetivo disso é mostrar que há vários modos de criar novas colunas, renomeá-las e colocá-las em vários locais em uma tabela.  
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 4: Criar relações](lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Criar colunas calculadas  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>Criar uma coluna calculada MonthCalendar na tabela DimDate  
  
1.  Clique o **modelo** menu > **exibição de modelo** > **exibição de dados**.  
  
    Colunas calculadas só podem ser criadas usando o designer de modelos na exibição de dados.  
  
2.  No designer de modelo, clique o **DimDate** tabela (guia).  
  
3.  Clique com botão direito do **CalendarQuarter** cabeçalho de coluna e clique **Inserir coluna**.  
  
    Uma nova coluna nomeada **Calculated Column 1** é inserida à esquerda da coluna **Calendar Quarter** .  
  
4.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir. O recurso Preenchimento Automático ajuda a digitar os nomes totalmente qualificados de colunas e tabelas e lista as funções que estão disponíveis.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Os valores são preenchidos em todas as linhas da coluna calculada. Se você rolar para baixo na tabela, verá que as linhas podem ter valores diferentes para essa coluna baseados nos dados que estão em cada linha.    
  
5.  Renomeie esta coluna como **MonthCalendar**. 

    ![as-tabular-lesson5-newcolumn](media/as-tabular-lesson5-newcolumn.png) 
  
O MonthCalendar calculado coluna fornece um nome classificável para o mês.  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>Criar uma coluna calculada DayOfWeek na tabela DimDate  
  
1.  Com o **DimDate** da tabela ainda ativa, clique no **coluna** menu e, em seguida, clique **adicionar coluna**.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Quando você terminar a criação da fórmula, pressione ENTER. A nova coluna será adicionada à extrema direita da tabela.  
  
3.  Renomeie a coluna como **DayOfWeek**.  
  
4.  Clique no título de coluna e, em seguida, arraste a coluna entre a **EnglishDayNameOfWeek** coluna e o **DayNumberOfMonth** coluna.  
  
    > [!TIP]  
    > A movimentação das colunas na tabela facilita a navegação.  
  
A coluna calculada DayOfWeek fornece um nome classificável para o dia da semana.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>Criar uma coluna calculada ProductSubcategoryName na tabela DimProduct  
  
  
1.  No **DimProduct** tabela, role até a extrema direita da tabela. Observe que a coluna mais à direita é chamada **Adicionar Coluna** (em itálico); clique no título de coluna.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir.  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Renomeie a coluna como **ProductSubcategoryName**.  
  
A coluna calculada ProductSubcategoryName é usada para criar uma hierarquia na tabela DimProduct que inclui dados da coluna EnglishProductSubcategoryName na tabela DimProductSubcategory. As hierarquias não podem ultrapassar mais de uma tabela. Você criará hierarquias posteriormente na lição 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>Criar uma coluna calculada ProductCategoryName na tabela DimProduct  
  
1.  Com o **DimProduct** ainda ativa, clique de tabela os **coluna** menu e, em seguida, clique **adicionar coluna**.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Renomeie a coluna como **ProductCategoryName**.  
  
A coluna calculada ProductCategoryName é usada para criar uma hierarquia na tabela DimProduct que inclui dados da coluna EnglishProductCategoryName na tabela DimProductCategory. As hierarquias não podem ultrapassar mais de uma tabela.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>Criar uma coluna calculada Margin na tabela FactInternetSales  
  
1.  No designer de modelo, selecione a **FactInternetSales** tabela.  
  
2.  Adicione uma nova coluna.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Renomeie a coluna como **Margin**.  
  
5.  Arraste a coluna entre a **SalesAmount** coluna e o **TaxAmt** coluna. 
 
      ![as-tabular-lesson5-newmargin](media/as-tabular-lesson5-newmargin.png)
      
    A coluna calculada Margin é usada para analisar as margens de lucro de cada venda.  
  
## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [Lição 6: Criar medidas](lesson-6-create-measures.md).
  
  
  
