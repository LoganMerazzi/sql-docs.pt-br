---
title: 'Lição 4: Criar relações | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8cad8c81021587a9dc3742983d7c7c2cd80fc174
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404848"
---
# <a name="lesson-4-create-relationships"></a>Lição 4: Criar Relações
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você aprenderá a verificar as relações que foram criadas automaticamente quando os dados foram importados e adicionará novas relações entre tabelas diferentes. Uma relação é uma conexão criada entre duas tabelas que estabelece como os dados dessas tabelas devem ser correlacionados. Por exemplo, a tabela DimProduct e a tabela DimProductSubcategory têm uma relação baseada no fato de que cada produto pertence a uma subcategoria. Para obter mais informações, consulte [relações](../tabular-models/relationships-ssas-tabular.md).
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 3: Marcar como tabela de data](lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Revisar relações existentes e adicionar novas relações  
Quando você importar dados usando o Assistente de importação de tabela, você obteve sete tabelas do banco de dados AdventureWorksDW. Em geral, quando você importa dados de uma fonte de dados relacional, as relações existentes são importadas automaticamente junto com os dados. No entanto, antes de dar continuidade à criação do modelo, você deve verificar se essas relações entre tabelas foram criadas corretamente. Para este tutorial, você adicionará também três novas relações.  
  
#### <a name="to-review-existing-relationships"></a>Para revisar relações existentes  
  
1.  Clique o **modelo** menu > **exibição de modelo** > **exibição de diagrama**.  

    Agora, o designer de modelos aparece em Exibição de Diagrama, um formato gráfico que exibe todas as tabelas que você importou com linhas entre elas. As linhas entre tabelas indicam as relações que foram criadas automaticamente quando você importar os dados.
    
    ![as-tabular-lesson4-diagram](media/as-tabular-lesson4-diagram.png)
  
    Use os controles de minimapa no canto inferior direito do designer de modelos para ajustar a exibição para que ela inclua o máximo de tabelas possível. Você pode também clique e arrastar tabelas para locais diferentes, reunindo o mais próximo de tabelas ou colocá-las em uma ordem específica. A movimentação de tabelas não afeta as relações já existentes entre elas. Para exibir todas as colunas em uma tabela específica, clique e arraste uma borda de tabela para expandir ou diminuí-lo.  
  
2.  Clique na linha sólida entre a **DimCustomer** tabela e o **DimGeography** tabela. A linha sólida entre essas duas tabelas mostra que essa relação está ativa, ou seja, ela é usada por padrão durante o cálculo das fórmulas DAX.  
  
    Observe a **GeographyKey** coluna na **DimCustomer** tabela e o **GeographyKey** coluna no **DimGeography** tabela agora ambos cada um aparecem dentro de uma caixa. Nesta apresentação, essas são as colunas usadas na relação. As propriedades da relação agora também aparecem na **propriedades** janela.  
  
    > [!TIP]  
    > Além de usar o designer de modelo na exibição de diagrama, você também pode usar a caixa de diálogo Gerenciar relações para mostrar as relações entre todas as tabelas em um formato de tabela. Clique com botão direito **relacionamentos** no Gerenciador de modelos tabulares e clique **gerenciar relações**. A caixa de diálogo Gerenciar relações mostram as relações que foram criadas automaticamente quando você importou os dados.  
  
3.  Use o designer de modelo na exibição de diagrama ou a caixa de diálogo Gerenciar relações, para verificar se as seguintes relações foram criadas quando cada uma das tabelas foi importada do banco de dados AdventureWorksDW:  
  
    |Ativa|Table|Tabela de Pesquisa Relacionada|  
    |----------|---------|------------------------|  
    |Sim|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Sim|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Sim|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Sim|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Sim|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Se qualquer uma das relações na tabela acima estiver ausente, verifique se o modelo inclui as tabelas a seguir: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory e FactInternetSales. Se as tabelas da mesma conexão de fonte de dados forem importadas em momentos distintos, não será criada nenhuma relação entre essas tabelas; essa relações deverão ser criadas manualmente.  

### <a name="take-a-closer-look"></a>Uma visão mais detalhada
Na exibição de diagrama, você observará uma seta, um asterisco e um número de linhas que mostram a relação entre tabelas.

![as-tabular-lesson4-line](media/as-tabular-lesson4-line.png)

A seta mostra a direção do filtro, que o asterisco mostra essa tabela é o lado muitos na cardinalidade da relação, e o 1 mostra que essa tabela é o um lado da relação. Se você precisar editar uma relação; Por exemplo, alterar a direção da relação do filtro ou cardinalidade, clique duas vezes na linha da relação na exibição de diagrama para abrir a caixa de diálogo Editar relação.

![as-tabular-lesson4-edit](media/as-tabular-lesson4-edit.png)

Provavelmente, você nunca precisará editar uma relação. Esses recursos são destinados a modelagem de dados avançada e estão fora do escopo deste tutorial. Para obter mais informações, consulte [bidirecional entre os filtros para modelos de tabela no SQL Server 2016 Analysis Services](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

Em alguns casos, talvez seja necessário criar relações adicionais entre tabelas no modelo para oferecer suporte a uma lógica corporativa específica. Para este tutorial, você precisa criar três relações adicionais entre as tabelas FactInternetSales e a tabela DimDate.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Para adicionar novas relações entre tabelas  
  
1.  No designer de modelo, no **FactInternetSales** de tabela, clique e segure na **OrderDate** coluna, em seguida, arraste o cursor para o **data** coluna no  **DimDate** tabela e, em seguida, solte.  

    Uma linha sólida aparece, indicando que você criou uma relação ativa entre a **OrderDate** coluna o **vendas pela Internet** tabela e o **data** coluna em que o **Data** tabela. 
  
      ![as-tabular-lesson4-new](media/as-tabular-lesson4-new.png) 
  
    > [!NOTE]  
    > Ao criar relações, a direção de cardinalidade e de filtragem entre a tabela primária e a tabela de pesquisa relacionada é selecionada automaticamente.  
  
2.  No **FactInternetSales** de tabela, clique e segure na **DueDate** coluna, em seguida, arraste o cursor para o **data** coluna no **DimDate** tabela e, em seguida, solte.  
  
    Uma linha pontilhada aparece, indicando que você criou uma relação inativa entre a **DueDate** coluna o **FactInternetSales** tabela e o **data** coluna o  **DimDate** tabela. Você pode ter várias relações entre tabelas, mas só uma relação pode estar ativa por vez.  
  
3.  Por fim, crie mais uma relação; no **FactInternetSales** de tabela, clique e segure na **ShipDate** coluna, em seguida, arraste o cursor para o **data** coluna no **DimDate**da tabela e, em seguida, solte.  
    
     ![as-tabular-lesson4-newinactive](media/as-tabular-lesson4-newinactive.png)
  
## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [Lição 5: Criar colunas calculadas](lesson-5-create-calculated-columns.md).
  
  
  
