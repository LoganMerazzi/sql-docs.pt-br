---
title: Distribuições (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f4789a0e312decb2a46a9a1ba656fc5e4d3e9d47
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070748"
---
# <a name="distributions-dmx"></a>Distribuições (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Na [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você pode definir o conteúdo das colunas em uma estrutura de mineração para afetar como os algoritmos processarão os dados nessas colunas quando você cria modelos de mineração. Com relação a certos algoritmos, é útil definir a distribuição de colunas contínuas antes de processar o modelo, principalmente quando se sabe que as colunas contêm distribuições comuns de valores. Se as distribuições não estiverem definidas, os modelos de mineração resultantes poderão produzir previsões menos precisas do que se as distribuições estiverem definidas, uma vez que os algoritmos terão menos informações com as quais interpretar dados.  
  
 Os algoritmos de mineração de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)] oferecem suporte aos seguintes tipos de distribuição:  
  
 **NORMAL**  
 Os valores para a coluna contínua formam um histograma com uma distribuição Gaussiana normal.  
  
 **Log Normal**  
 Os valores da coluna contínua formam um histograma, onde o logaritmo dos valores é normalmente distribuído.  
  
 **UNIFORME**  
 Os valores para a coluna contínua formam uma curva plana, na qual todos os valores são igualmente prováveis.  
  
 Para obter mais informações sobre [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de mineração de dados, consulte [algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md). Provedores de algoritmo de terceiros podem oferecer suporte a tipos de distribuição adicionais. Para determinar os tipos de distribuição um algoritmo oferece suporte, use o **SUPPORTED_DISTRIBUTION_FLAGS** linhas de esquema.  
  
 Para obter mais informações sobre tipos de distribuição, consulte [distribuições de colunas &#40;mineração de dados&#41;](../analysis-services/data-mining/column-distributions-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de conteúdo &#40;Data Mining&#41;](../analysis-services/data-mining/content-types-data-mining.md)   
 [Referência de DMX &#40;extensões DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
