---
title: Conceitos básicos (Analysis Services) de script MDX | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ca77b9c10f1dba24127e35e5fe55d7ffcdad3dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165842"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>Conceitos básicos de geração de scripts MDX (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  No [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], um script MDX é composto de uma ou mais linguagens ou instruções MDX que populam um cubo com cálculos.  
  
 Um script MDX define o processo de cálculo de um cubo. Um script MDX também é considerado parte do próprio cubo. Portanto, alterar um script MDX associado a um cubo altera imediatamente o processo de cálculo do cubo.  
  
 Para criar scripts MDX, você pode usar o Designer de Cubo no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [Definir atribuições e outros comandos de script](../../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md) e [Introdução ao script MDX no Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892).  
  
 Para questões de desempenho relacionadas a cálculos e consultas MDX, consulte a seção de otimização de MDX no [Guia de Desempenho do SQL Server Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=399050).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[O script básico de MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)|Detalhes sobre o script MDX básico, inclusive o script MDX padrão fornecido em cada cubo, e como os scripts MDX geralmente funcionam dentro de um cubo no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Gerenciando escopo e contexto &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/managing-scope-and-context-mdx.md)|Descreve como usar a instrução [CALCULATE](../../../mdx/mdx-scripting-calculate.md) , a instrução [SCOPE](../../../mdx/mdx-scripting-scope.md) e a função [This](../../../mdx/this-mdx.md) para gerenciar contexto e escopo dentro de um script MDX.|  
|[Usando variáveis e parâmetros &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|Descreve como utilizar variáveis e parâmetros em um script MDX.|  
|[Tratamento de erro &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/error-handling-mdx.md)|Explica a manipulação de erros dentro de um script MDX.|  
|[MDX com suporte &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/supported-mdx-mdx.md)|Fornece uma lista de operadores, instruções e funções MDX suportadas em um script MDX.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da linguagem MDX &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)  
  
  
