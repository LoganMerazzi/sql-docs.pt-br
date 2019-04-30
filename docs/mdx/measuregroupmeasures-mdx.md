---
title: MeasureGroupMeasures (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55e00420ad3f941d50d9179dcd4a87d678cc28a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267936"
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)


  Retorna um conjunto de medidas que pertence ao grupo de medidas especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>Argumentos  
 *MeasureGroupName*  
 Uma expressão de cadeia de caracteres válida que contém o nome do grupo de medidas a partir do qual o conjunto de medidas será recuperado.  
  
## <a name="remarks"></a>Comentários  
 A cadeia de caracteres especificada deve coincidir exatamente com o nome do grupo de medidas. Os colchetes para nomes de grupo de medidas com espaços não são necessários.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna todas as medidas no grupo de medidas Vendas da Internet no cubo Adventure Works.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
