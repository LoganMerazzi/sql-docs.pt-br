---
title: Classificado colunas (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content types [data mining]
- STDEV column
- VARIANCE column
- PROBABLILITY column
- PROBABILITY_STDEV column
- columns [data mining], classified
- classified columns [data mining]
- PROBABILITY_VARIANCE column
- SUPPORT column
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4c96ee3cbaa5ae25404d61054dccd1860c6596f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085692"
---
# <a name="classified-columns-data-mining"></a>Colunas classificadas [mineração de dados]
  Quando você define uma coluna classificada, cria uma relação entre a coluna atual e outra coluna na estrutura de mineração. Os dados na coluna da estrutura de mineração que você designa como a coluna classificada contém informações categóricas que descrevem os valores em outra coluna na estrutura de mineração.  
  
 Por exemplo, suponha que você tenha duas colunas com dados numéricos: uma coluna, [Compras Anuais], contém as compras anuais totais por cliente durante um ano civil específico e a outra coluna, [Desvios Padrão], contém os desvios padrão para obter esses valores. Neste caso, você pode designar a coluna [Compras Anuais] como a coluna classificada e o modelo poderia usar esta relação na análise.  
  
> [!NOTE]  
>  Os algoritmos fornecidos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não dão suporte ao uso de colunas classificadas; este recurso é fornecido para uso na criação de algoritmos personalizados.  
  
## <a name="defining-a-classified-column"></a>Definindo uma coluna classificada  
 O tipo de dados de uma coluna classificada deve ser `Long` ou `Double`.  
  
 A lista a seguir descreve os tipos de conteúdo para os quais o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte para colunas classificadas.  
  
 **PROBABILITY**  
 O valor na coluna é a probabilidade do valor associado e é um número entre 0 e 1.  
  
 **VARIANCE**  
 O valor na coluna é a variância do valor associado.  
  
 **STDEV**  
 O valor na coluna é o desvio padrão do valor associado.  
  
 **PROBABILITY_VARIANCE**  
 O valor na coluna é a variância da probabilidade para o valor associado.  
  
 **PROBABILITY_STDEV**  
 O valor na coluna é o desvio padrão da probabilidade para o valor associado.  
  
 **SUPPORT**  
 O valor na coluna é o peso ou o fator de replicação do caso do valor associado.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de conteúdo &#40;Data Mining&#41;](content-types-data-mining.md)   
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](mining-structures-analysis-services-data-mining.md)   
 [Tipos de dados &#40;Mineração de dados&#41;](data-types-data-mining.md)  
  
  
