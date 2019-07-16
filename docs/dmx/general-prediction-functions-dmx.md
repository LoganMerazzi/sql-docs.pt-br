---
title: Funções de previsão gerais (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8eff7603fa0d0be0e90af201e524554f5e336ea8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937793"
---
# <a name="general-prediction-functions-dmx"></a>Funções de previsão gerais (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Você pode usar o **selecionar** instrução em extensões DMX (Data Mining) para criar diferentes tipos de consultas. Uma consulta pode ser usada para retornar informações sobre o próprio modelo de mineração, fazer novas previsões ou alterar o modelo treinando-o com novos dados. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Fornece uma variedade de funções especializadas que controlam o tipo de informação que é retornado em uma consulta. Adicionando essas funções a uma consulta DMX, você pode recuperar estatísticas ou colunas de dados adicionais. No entanto, cada tipo de consulta e cada tipo modelo suporta apenas algumas funções.  
  
## <a name="common-functions"></a>Funções comuns  
 Você pode usar funções para ampliar os resultados retornados por um modelo de mineração. Você pode usar as funções a seguir para qualquer **selecionar** instrução que retorna uma expressão de tabela:  
  
|||  
|-|-|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|  
|[Prever &#40;DMX&#41;](../dmx/predict-dmx.md)|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 Além disso, as funções a seguir são suportadas em quase todos os tipos de modelo:  
  
-   [Existe &#40;DMX&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)  
  
-   [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Prever &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [Structurecolumn=3='<nome &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)  
  
 Os algoritmos individuais podem dar suporte a funções adicionais. Para obter uma lista das funções que são compatíveis com cada tipo de modelo, consulte [consultas de mineração de dados](../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="functions-specific-to-select-syntax"></a>Funções específicas da sintaxe SELECT  
 A tabela a seguir lista as funções que você pode usar para cada tipo de **selecionar** instrução.  
  
 Para obter informações gerais sobre as funções em DMX, consulte [extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
|Tipo de consulta|Funções suportadas|Comentários|  
|----------------|-------------------------|-------------|  
|[SELECT DISTINCT FROM \<modelo >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|Essas funções podem ser usadas para fornecer valores máximos, valores mínimos e médias para qualquer coluna que contenha tipos de dados numéricos, independentemente de a coluna ser contínua ou ter sido diferenciada.|  
|[SELECT FROM \<modelo >. CONTEÚDO](../dmx/select-from-model-content-dmx.md)<br /><br /> ou<br /><br /> [SELECT FROM \<modelo >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Essa função recupera nós filho para o nó especificado no modelo e pode ser usada, por exemplo, para iterar através de nós no conteúdo do modelo de mineração. A organização dos nós no conteúdo do modelo de mineração depende do tipo de modelo. Para obter informações sobre a estrutura para cada tipo de modelo de mineração, consulte [conteúdo do modelo de mineração &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).<br /><br /> Se você tiver salvo o conteúdo do modelo de mineração como uma dimensão, também poderá usar outras funções MDX que estão disponíveis para consultar uma hierarquia de atributo.|  
|[SELECT FROM \<modelo >. CASOS](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [ClientSettingsGeneralFlag Class](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|A função Lag é suportada somente para modelos de série temporal.<br /><br /> A função IsTestCase é suportada em modelos se baseiam em uma estrutura que foi criada usando a opção de validação para criar um conjunto de dados de teste. Se o modelo não for baseado em uma estrutura com um conjunto de teste de validação, todos os casos serão considerados como casos de treinamento.|  
|[SELECT FROM \<modelo >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|Nesse contexto, a função IsInNode retornará um caso que pertence a um conjunto de casos de amostra idealizados.|  
|SELECT FROM \<modelo >. PMML|Não aplicável. Em vez disso, use funções de consulta XML.|As representações PMML são suportadas apenas pelos tipos de modelo a seguir:<br /><br /> Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)]<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering|  
|[SELECT FROM \<modelo > PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)|Funções de previsão que são específicas do algoritmo usado para criar o modelo.|Para obter uma lista das funções de previsão para cada tipo de modelo, consulte [consultas de mineração de dados](../analysis-services/data-mining/data-mining-queries.md).|  
|[SELECT FROM \<modelo >](../dmx/select-from-model-dmx.md)|Funções de previsão que são específicas do algoritmo usado para criar o modelo.|Para obter uma lista das funções de previsão para cada tipo de modelo, consulte [consultas de mineração de dados](../analysis-services/data-mining/data-mining-queries.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
