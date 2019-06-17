---
title: Levels (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e8edfdc3c6888c34dd789c521bc42c6b919e1a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63269949"
---
# <a name="levels-mdx"></a>Função Levels (MDX)


  Retorna o nível cuja posição em uma dimensão ou hierarquia é especificada por uma expressão numérica ou cujo nome é especificado por uma expressão de cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Uma linguagem MDX válida que retorna uma hierarquia.  
  
 *Level_Number*  
 Uma expressão numérica válida que especifica um número de nível.  
  
 *Level_Name*  
 Uma expressão de cadeia de caracteres válida que especifica um nome de nível.  
  
## <a name="remarks"></a>Comentários  
 Se um número de nível for especificado, o **níveis** função retorna o nível associado a posição de base zero especificada.  
  
 Se um nome de nível for especificado, o **níveis** função retorna o nível especificado.  
  
> [!NOTE]  
>  Use a sintaxe de expressão de cadeia de caracteres para funções definidas pelo usuário.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir ilustram cada um dos **níveis** sintaxes de função.  
  
### <a name="numeric"></a>Numeric  
 O exemplo a seguir retorna o nível País:  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>Cadeia de caracteres  
 O exemplo a seguir retorna o nível País:  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
