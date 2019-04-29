---
title: Membros (cadeia de caracteres) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 302445cadc829de35eca28db2888aaa01673ca75
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63048441"
---
# <a name="members-string-mdx"></a>Membros (cadeia de caracteres) (MDX)


  Retorna um membro especificado por uma expressão de cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Uma expressão de cadeia de caracteres válida que especifica um nome de membro.  
  
## <a name="remarks"></a>Comentários  
 O **membros (cadeia de caracteres)** função retorna um membro único cujo nome é especificado. Normalmente, você usa o **membros (cadeia de caracteres)** função com funções externas, fornecendo para o **membros (cadeia de caracteres)** uma cadeia de caracteres que identifica um membro de função e o **membros (cadeia de caracteres)**  função retorna o valor para o membro especificado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa o **membros (cadeia de caracteres)** de função para converter a cadeia de caracteres especificada em um membro válido e, em seguida, retorna a medida padrão para o membro especificado na cadeia de caracteres. A cadeia de caracteres especificada está entre aspas simples. A medida padrão é a medida Valor das Vendas do Revendedor.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
