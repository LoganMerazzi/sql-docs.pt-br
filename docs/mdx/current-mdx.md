---
title: Current (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 821d517419b90df44b7943a1e0edde12ef667b6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047126"
---
# <a name="current-mdx"></a>Função Current (MDX)


  Retorna a tupla atual de um conjunto durante a iteração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Comentários  
 Em cada etapa durante uma iteração, a tupla que está sendo operada em é a tupla atual. O **atual** função retorna essa tupla. Essa função só é válida durante uma iteração em um conjunto.  
  
 Incluem funções MDX que iterar por meio de um conjunto de [gerar](../mdx/generate-mdx.md) função.  
  
> [!NOTE]  
>  Essa função funciona somente com conjuntos que são nomeados, seja usando um alias de conjunto ou definindo um conjunto nomeado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como usar o **atual** funcionar dentro **gerar**:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
