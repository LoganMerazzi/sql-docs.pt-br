---
title: 'Lição 9: Criar hierarquias | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 388df29badcde95c04c3db3604af63ed995666ac
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403738"
---
# <a name="lesson-9-create-hierarchies"></a>Lição 9: Criar hierarquias
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará hierarquias. Hierarquias são grupos de colunas organizados em níveis; por exemplo, uma hierarquia Geografia poderia ter subníveis para País, Estado, Município e Cidade. As hierarquias podem aparecer separadas de outras colunas em uma lista de campo de aplicativo cliente de relatório, tornando mais fácil para os usuários clientes navegarem e incluírem itens em um relatório. Para obter mais informações, consulte [hierarquias](../tabular-models/hierarchies-ssas-tabular.md).  
  
Para criar hierarquias, você usará o designer de modelo na *exibição de diagrama*. Não há suporte para criar e gerenciar hierarquias na exibição de dados.  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 8: Criar perspectivas](lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Criar hierarquias  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>Para criar uma hierarquia de categoria na tabela DimProduct  
  
1.  No designer de modelo (exibição de diagrama), clique com botão direito do **DimProduct** tabela > **criar hierarquia**. A nova hierarquia aparece na parte inferior da janela de tabela. Renomeie a hierarquia **categoria**.  
  
2.  Clique e arraste a **ProductCategoryName** coluna para a nova **categoria** hierarquia.  
  
3.  No **categoria** hierarquia, clique com botão direito do **ProductCategoryName** > **Renomear**e, em seguida, digite **categoria**.  
  
    > [!NOTE]  
    > A renomeação de uma coluna em uma hierarquia não renomeia essa coluna na tabela. Uma coluna em uma hierarquia é apenas uma representação da coluna na tabela.  
  
4.  Clique e arraste a **ProductSubcategoryName** coluna para o **categoria** hierarquia. Renomeá-lo **subcategoria**. 
  
5.  Clique com botão direito do **ModelName** coluna > **adicionar à hierarquia**e, em seguida, selecione **categoria**. Faça o mesmo para **EnglishProductName**. Renomeie as colunas na hierarquia **modelo** e **produto**.  

    ![as-tabular-lesson9-category](media/as-tabular-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>Para criar hierarquias na tabela DimDate  
  
1.  No **DimDate** da tabela, crie uma nova hierarquia chamada **calendário**.  
  
3.  Adicione as seguintes colunas em ordem:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  No **DimDate** da tabela, criar um **Fiscal** hierarquia. Inclua as seguintes colunas:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Por fim, na **DimDate** da tabela, criar um **ProductionCalendar** hierarquia. Inclua as seguintes colunas:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [Lição 10: Criar partições](lesson-10-create-partitions.md). 
  
  
