---
title: PredictProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e3a948ce783593ce649ad161d0db73a22a909885
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041719"
---
# <a name="predictprobability-dmx"></a>PredictProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna a probabilidade para um estado especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Uma coluna escalar.  
  
## <a name="return-type"></a>Tipo de retorno  
 Valor escalar.  
  
## <a name="remarks"></a>Comentários  
 Se o estado previsto for omitido, o estado que tiver a mais alta probabilidade será usado, excluindo-se o bucket de estados ausentes. Para incluir a partição de estados faltantes, defina as \<estado previsto > para **INCLUDE_NULL**. Para retornar a probabilidade para os estados faltantes, defina o \<estado previsto > como NULL.  
  
> [!NOTE]  
>  Alguns modelos de mineração não fornecem valores de probabilidade e, portanto, não podem usar esta função. Além disso, os valores de probabilidade de qualquer valor de destino em particular são calculados de modo diferente ou podem ter uma interpretação diferente dependendo do tipo de modelo que você está consultando. Para obter mais informações sobre como a probabilidade é calculada para um determinado tipo de modelo, consulte o tópico de algoritmo individual no [conteúdo do modelo de mineração &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa uma junção de previsão natural para determinar se um indivíduo é provavelmente um comprador de bicicletas, com base no modelo de mineração da Árvore de decisão TM, e determina também a probabilidade para a previsão. Neste exemplo, há duas funções PredictProbability, uma para cada valor possível. Se você omitir este argumento, a função retornará a probabilidade do valor mais provável.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictProbability([Bike Buyer], 1) AS [Bike Buyer = Yes],  
  PredictProbability([Bike Buyer], 0) AS [Bike Buyer = No]  
FROM [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Resultados do exemplo:  
  
|Bike Buyer|Comprador de Bicicleta = Sim|Comprador de Bicicleta = Não|  
|----------------|-----------------------|----------------------|  
|1|0.867074195848097|0.132755556974282|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
