---
title: LinRegPoint (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3719071beca4dbd8cc991befbb7b2b74f8982c89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905570"
---
# <a name="linregpoint-mdx"></a>LinRegPoint (MDX)


  Calcula a regressão linear de um conjunto e retorna o valor da *origem y* na linha de regressão, y = ax + b para um determinado valor de x.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LinRegPoint(Slice_Expression_x, Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Slice_Expression_x*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula que retorna um número que representa valores do eixo do slicer.  
  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Numeric_Expression_y*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo y.  
  
 *Numeric_Expression_x*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número que representa valores do eixo x.  
  
## <a name="remarks"></a>Comentários  
 A regressão linear, que usa o método dos mínimos quadrados, calcula a equação de uma linha de regressão (ou seja, a linha mais adequada para uma série de pontos). A linha de regressão tem a seguinte equação, em que um é a inclinação e b é a interceptação:  
  
 y = ax+b  
  
 O **LinRegPoint** função avalia o conjunto especificado em relação à segunda expressão numérica para obter os valores para o eixo y. Em seguida, a função avalia o conjunto especificado em relação à terceira expressão numérica, se especificada, para obter o conjunto de valores para o eixo x. Se a terceira expressão numérica não for especificada, a função utilizará o contexto atual das células no conjunto especificado como os valores para o eixo x. A não especificação do argumento de eixo x geralmente é usada com a dimensão Tempo.  
  
 Assim que a linha de regressão linear tiver sido calculada, o valor da equação será calculado para a primeira expressão numérica e, em seguida, retornado.  
  
> [!NOTE]  
>  O **LinRegPoint** função ignora células vazias ou células que contêm texto. Porém, a função contém células com valores zero.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir retorna o valor previsto de Vendas de unidade nos últimos 10 períodos com base na relação estatística entre Vendas de unidade e Vendas na loja.  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
