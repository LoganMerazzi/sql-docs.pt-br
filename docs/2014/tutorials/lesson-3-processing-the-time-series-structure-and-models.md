---
title: 'Lição 3: A série de tempo de processamento estrutura e modelos | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 16e27b57-eae1-47a7-a02c-47b6ed487d87
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 493d27c9836eb765c655eba5bbb004e4d48cde40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042872"
---
# <a name="lesson-3-processing-the-time-series-structure-and-models"></a>Lição 3: Como processar a estrutura e os modelos de série temporal
  Nesta lição, você aprenderá a usar o [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) instrução para processar a série temporal, estruturas de mineração e modelos de mineração que você criou.  
  
 Ao processar uma estrutura de mineração, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] lê os dados de origem e compila as estruturas que dão suporte a modelos de mineração. Sempre será necessário processar um modelo e uma estrutura de mineração em sua criação. Se você especificar a estrutura de mineração ao usar INSERT INTO, a instrução processará a estrutura de mineração e todos os seus modelos de mineração associados.  
  
 Quando você adicionar um modelo de mineração a uma estrutura de mineração que já foi processada, será possível usar a instrução `INSERT INTO MINING MODEL` para processar somente o novo modelo de mineração usando os dados existentes.  
  
 Para obter mais informações sobre como processar modelos de mineração, consulte [considerações e requisitos de processamento de &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
## <a name="insert-into-statement"></a>Instrução INSERT INTO  
 Para treinar a estrutura de mineração de série temporal e todos os seus modelos de mineração associados, use o [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) instrução. O código na instrução pode ser dividido nas seguintes partes.  
  
-   Identificando a estrutura de mineração  
  
-   Listando as colunas na estrutura de mineração  
  
-   Definindo os dados de treinamento  
  
 A seguir, um exemplo genérico da instrução `INSERT INTO`:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY (<source data definition>)  
```  
  
 A primeira linha do código identifica a estrutura de mineração a ser treinada:  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 As linhas seguintes do código especificam as colunas definidas pela estrutura de mineração. É preciso listar cada coluna na estrutura de mineração, e cada coluna deve mapear para uma coluna contida nos dados da consulta de origem.  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 As linhas finais do código definem os dados que serão usados para treinar a estrutura de mineração.  
  
```  
OPENQUERY (<source data definition>)  
```  
  
 Nesta lição, use `OPENQUERY` para definir os dados de origem. Para obter mais informações sobre outros métodos de definição de consulta na fonte de dados, consulte [ &#60;consulta de fonte de dados&#62;](/sql/dmx/source-data-query).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará a seguinte tarefa nesta lição:  
  
-   Processar a estrutura de mineração Forecasting_MIXED_Structure  
  
-   Processar os modelos de mineração relacionados Forecasting_MIXED, Forecasting_ARIMA e Forecasting_ARTXP  
  
## <a name="processing-the-time-series-mining-structure"></a>Processando a estrutura de mineração de série temporal  
  
#### <a name="to-process-the-mining-structure-and-related-mining-models-by-using-insert-into"></a>Para processar a estrutura de mineração e os modelos de mineração relacionados usando INSERT INTO  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico da instrução INSERT INTO no campo em branco da consulta.  
  
3.  Substitua o seguinte:  
  
    ```  
    [<mining structure>]  
    ```  
  
     por:  
  
    ```  
    Forecasting_MIXED_Structure  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <mining structure columns>  
    ```  
  
     por:  
  
    ```  
    [ReportingDate],  
    [ModelRegion]   
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    OPENQUERY(<source data definition>)  
    ```  
  
     por:  
  
    ```  
    OPENQUERY([Adventure Works DW 2008R2],'SELECT [ReportingDate], [ModelRegion], [Quantity], [Amount]  
    FROM vTimeSeries ORDER BY [ReportingDate]')  
    ```  
  
     A consulta de fonte faz referência a [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] fonte de dados definida no projeto de exemplo IntermediateTutorial. Ela usa esta fonte de dados para acessar a exibição vTimeSeries. Essa exibição contém os dados de origem que serão usados para treinar o modelo de mineração. Se você não estiver familiarizado com esse projeto ou essas exibições, consulte[lição 2: Criando um cenário de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
     A instrução completa agora deve ser:  
  
    ```  
    INSERT INTO MINING STRUCTURE [Forecasting_MIXED_Structure]  
    (  
       [ReportingDate],[ModelRegion],[Quantity],[Amount])  
    )  
    OPENQUERY(  
    [Adventure Works DW 2008R2],  
    'SELECT [ReportingDate],[ModelRegion],[Quantity],[Amount] FROM vTimeSeries ORDER BY [ReportingDate]'  
    )   
    ```  
  
6.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
7.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `ProcessForecastingAll.dmx`.  
  
8.  Na barra de ferramentas, clique o **Execute** botão.  
  
 Depois que execução da consulta for concluída, você poderá criar previsões usando os modelos de mineração processados. Na próxima lição, você criará várias previsões com base nos modelos de mineração que criou.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 4: Criando previsões de série temporal usando DMX](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e considerações de processamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)   
 [&#60;consulta de fonte de dados&#62;](/sql/dmx/source-data-query)   
 [OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery)  
  
  
