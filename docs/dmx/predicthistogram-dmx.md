---
title: PredictHistogram (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 61a90dc7fa034fc8983246aa4eb7119832a2d47d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008016"
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna uma tabela que representa um histograma para a previsão de uma determinada coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Uma referência de coluna escalar ou uma referência de coluna de cluster. Pode ser usado com todos os tipos de algoritmo, exceto o algoritmo de Associação do [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
## <a name="return-type"></a>Tipo de retorno  
 Uma tabela.  
  
## <a name="remarks"></a>Comentários  
 Um histograma gera colunas de estatísticas. A estrutura da coluna do histograma retornado depende do tipo de referência de coluna que é usado com o **PredictHistogram** função.  
  
## <a name="scalar-columns"></a>Colunas escalares  
 Para um \<referência de coluna escalar >, o histograma que o **PredictHistogram** retornos de função consiste as seguintes colunas:  
  
-   Valor sendo previsto.  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de mineração de dados não suportam **$ProbabilityVariance**. Essa coluna sempre contém 0 para algoritmos do [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de mineração de dados não suportam **$ProbabilityStdev**. Essa coluna sempre contém 0 para algoritmos do [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   **$AdjustedProbability**  
  
     O **$AdjustedProbability** coluna é um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] extensão para o [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para mineração de dados.  
  
## <a name="cluster-columns"></a>Colunas cluster  
 O histograma que o **PredictHistogram** função retorna para um \<referência de coluna do cluster > consiste nas seguintes colunas:  
  
-   **$Cluster** (representa o nome do cluster)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o estado previsto da coluna Bike Buyer em uma consulta singleton. A consulta também retorna os estados de dois primeiros mais prováveis do atributo Bike Buyer, com base na probabilidade ajustada obtida usando o **PredictHistogram** função.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Consulte também  
 [Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
