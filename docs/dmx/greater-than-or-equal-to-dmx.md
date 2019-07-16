---
title: '&gt;= (Maior que ou igual a) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3615dc8b5de0e5057e2dedaa0077aae51ed87ebe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074795"
---
# <a name="gt-greater-than-or-equal-to-dmx"></a>&gt;= (Maior que ou igual a) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza uma operação de comparação que determina se o valor de uma expressão DMX (Data Mining Extensions) é maior do que ou igual ao valor de outra expressão DMX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DMX_Expression >= DMX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DMX_Expression*  
 Expressão DMX válida.  
  
## <a name="return-value"></a>Valor retornado  
 Valor booliano que conterá TRUE se ambos os parâmetros forem não nulos e o valor do primeiro parâmetro for maior do que ou igual ao valor do segundo parâmetro. Valor Booliano contendo FALSE se ambos os parâmetros forem não nulos e se o valor do primeiro parâmetro for menor do que o valor do segundo parâmetro. O valor Booliano conterá um valor nulo se um ou ambos os parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Operadores de comparação &#40;DMX&#41;](../dmx/operators-comparison.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
