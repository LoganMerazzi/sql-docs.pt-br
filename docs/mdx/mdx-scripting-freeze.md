---
title: Instrução FREEZE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cd652a9f308bd7a564a61d165f9c47875a900737
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187570"
---
# <a name="mdx-scripting---freeze"></a>Script MDX – FREEZE


  Bloqueia os valores de célula de um subcubo especificado para seus valores atuais. Quando os valores de célula são bloqueados, as alterações nas outras células não têm nenhum efeito nas células que estão bloqueadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>Argumentos  
 *Subcube_Expression*  
 Uma linguagem MDX válida que retorna um subcubo.  
  
## <a name="remarks"></a>Comentários  
 O **CONGELAR** instrução bloqueia os valores de células em um subcubo especificado, impedindo que instruções subsequentes em um MDX script alterem seus valores em cálculo subsequente passa.  
  
 No exemplo a seguir, A e B representam subcubos em um script de cálculo MDX:  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 Nesse momento, A e B são iguais a 3.  
  
 Agora podemos inserir a **congelar** função para bloquear as células no subcubo:  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 Agora, A é igual a 2 e B é igual a 3.  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de script MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
