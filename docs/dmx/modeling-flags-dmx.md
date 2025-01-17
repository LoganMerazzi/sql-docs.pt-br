---
title: Sinalizadores de modelagem (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 01be0e2d0ead01a3b6c630e0ddd0f53e55620104
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008324"
---
# <a name="modeling-flags-dmx"></a>Sinalizadores de modelagem (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Use sinalizadores de modelagem no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para fornecer informações adicionais para um algoritmo de mineração de dados sobre os dados definidos em uma tabela de casos. O algoritmo pode usar essas informações para criar um modelo de mineração de dados mais preciso. É possível definir sinalizadores de modelagem em colunas de estrutura de mineração e em colunas de modelo de mineração.  
  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte aos seguintes sinalizadores de modelagem:  
  
 **NOT NULL**  
 Os valores da coluna de atributo não devem jamais conter um valor nulo. Ocorrerá um erro se o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] encontrar um valor nulo nessa coluna de atributo durante o processo de treinamento do modelo. Esse sinalizador é definido em uma coluna de estrutura de mineração.  
  
 **REGRESSOR**  
 Indica que o algoritmo pode usar a coluna especificada na fórmula de regressão de algoritmos de regressão. Esse sinalizador tem suporte nos algoritmos [!INCLUDE[msCoName](../includes/msconame-md.md)]Regressão linear[!INCLUDE[msCoName](../includes/msconame-md.md)] e Árvores de decisão, sendo definido em uma coluna de modelo de mineração.  
  
 **MODEL_EXISTENCE_ONLY**  
 Os valores da coluna de atributo são menos importantes que a presença do atributo. Esse sinalizador é definido em uma coluna de modelo de mineração.  
  
 Os algoritmos de terceiros podem oferecer suporte a sinalizadores de modelagem adicionais. Para determinar os sinalizadores de modelagem um algoritmo oferece suporte, use o **SUPPORTED_MODELING_FLAGS** linhas de esquema. Também é possível consultar os serviços de mineração no servidor para determinar quais sinalizadores de modelagem têm suporte para um determinado algoritmo. Por exemplo, a consulta a seguir retorna os sinalizadores de modelagem com suporte do algoritmo Regressão Linear da Microsoft no servidor atual:  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 Resultados esperados:  
  
 NOT NULL, REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>Especificando sinalizadores de modelagem em um modelo de mineração  
 Para obter exemplos da sintaxe que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte para especificar um sinalizador em uma coluna de estrutura de mineração, consulte [criar estrutura de MINERAÇÃO &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Para obter um exemplo da sintaxe para especificar um sinalizador de modelagem em uma coluna de modelo de mineração, consulte [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
 Para obter mais informações sobre como trabalhar com colunas do modelo de mineração, consulte [colunas do modelo de mineração](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
