---
title: '&lt;&gt; (Não igual a) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 032505ee0714bc10baa698b1a229e5456710c81d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088326"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (Não igual a) (MDX)


  Realiza uma operação de comparação que determina se o valor de uma linguagem MDX não é igual ao valor de outra linguagem MDX.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor booliano baseado nas seguintes condições:  
  
-   **True** se ambos os parâmetros forem não nulos e o primeiro parâmetro não é igual ao segundo parâmetro.  
  
-   **False** se ambos os parâmetros forem não nulos e o primeiro parâmetro for igual ao segundo parâmetro.  
  
-   nulo se um ou os dois parâmetros forem avaliados como um valor nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de operador MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
