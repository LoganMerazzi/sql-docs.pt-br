---
title: O Script básico de MDX (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2bebee1057180259c9813d7a650594c0c6d4736d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208705"
---
# <a name="the-basic-mdx-script-mdx"></a>O script básico de MDX (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Um script MDX define o processo de cálculo para um cubo no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Existem dois tipos de scripts MDX:  
  
 **O script MDX padrão**  
 Quando você cria um cubo, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria um script MDX padrão para esse cubo. Esse script define uma passagem de cálculo para o cubo inteiro.  
  
 **Script MDX definido pelo usuário**  
 Depois que você criar um cubo, poderá adicionar scripts MDX definidos pelo usuário que ampliam os recursos de cálculo do cubo.  
  
## <a name="the-default-mdx-script"></a>O script MDX padrão  
 O script MDX padrão criado pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] quando você define um cubo contém uma única instrução CALCULATE. Essa única instrução CALCULATE fica no início do script MDX padrão e indica que o cubo inteiro deve ser calculado durante a primeira passagem de cálculo.  
  
 O script MDX padrão também contém comandos de script que criam conjuntos nomeados, atribuições e membros calculados criados no Designer de Cubo:  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] adiciona diretamente comandos de script ao script MDX padrão.  
  
-   Para cada conjunto nomeado do cubo, existe uma instrução CREATE SET correspondente no script MDX padrão.  
  
-   Para cada membro calculado definido no cubo, existe uma instrução CREATE MEMBER correspondente no script MDX padrão.  
  
 Você controla a ordem de comandos de script, conjuntos nomeados e membros calculados no script MDX padrão usando a guia **Cálculos** do Designer de Cubo. Para obter mais informações sobre como definir cálculos armazenados no script MDX padrão, consulte [Cálculos em modelos multidimensionais](../../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md).  
  
 Se não houver um script MDX associado a um cubo, este assumirá o script MDX padrão. Um cubo precisa estar associado a pelo menos um script MDX porque o cubo depende do script MDX para determinar o comportamento do cálculo. Em outras palavras, um cubo que não foi associado a um script MDX ou foi associado a um script MDX vazio não poderia e não deveria ser capaz de calcular células. Se você criar cubos programaticamente, seja usando comandos do Analysis Services Scripting Language (ASSL) ou usando o Analysis Management Objects (AMO), é recomendável que você crie um script MDX padrão que contenha uma única instrução CALCULATE para o cubo.  
  
## <a name="mdx-script-content"></a>Conteúdo do script MDX  
 Um script MDX pode conter as seguintes instruções e expressões:  
  
 Todas as instruções de script MDX  
 Em scripts MDX, as instruções de script MDX controlam o contexto e o escopo dos cálculos e gerenciam o comportamento de outras instruções do script MDX. Essa categoria inclui as seguintes instruções:  
  
-   [CALCULATE](../../../mdx/mdx-scripting-calculate.md)  
  
-   [FREEZE](../../../mdx/mdx-scripting-freeze.md)  
  
-   [SCOPE](../../../mdx/mdx-scripting-scope.md)  
  
 Para obter mais informações sobre instruções de scripts MDX, consulte [Instruções de script MDX &#40;MDX&#41;](../../../mdx/mdx-scripting-statements-mdx.md).  
  
 [CREATE MEMBER](../../../mdx/mdx-data-definition-create-member.md)  
 Uma instrução CREATE MEMBER cria membros calculados. Para obter mais informações sobre como criar membros calculados, consulte [Criando membros calculados em MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
 [CREATE SET](../../../mdx/mdx-data-definition-create-set.md)  
 A instrução CREATE SET cria conjuntos nomeados. Para obter mais informações sobre como criar conjuntos de nomes, consulte [Criando conjuntos nomeados em MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md).  
  
 Instruções condicionais  
 As instruções condicionais adicionam lógica condicional a scripts MDX. Essa categoria inclui as instruções [CASE](../../../mdx/case-statement-mdx.md) e [IF](../../../mdx/mdx-scripting-if.md) .  
  
 Expressões de atribuição  
 Uma expressão de atribuição atribui uma expressão, como um valor, a um subcubo restrito. Uma expressão de subcubo restrito é uma coleção de expressões de conjunto restritas que definem as "bordas" de um subcubo em um script MDX. Os códigos a seguir mostram a sintaxe de uma expressão de subcubo restrito:  
  
```  
<Constrained subcube> ::= (   
    ( <Constrained set> [<Crossjoin operator> <Constrained set>...] |  
    <ROOT function> |  
    <TREE function> |  
    LEAVES() |  
    * ) [, <Constrained subcube>...]  
<Constrained set> ::=   
    <Natural hierarchy>.MEMBERS |   
    <Natural hierarchy>.LEVEL(<numeric expression>).MEMBERS |   
    { <Natural hierarchy member> } |   
    DESCENDANTS( <Natural hierarchy member>, <Level expression>, ( SELF | AFTER | SELF_AND_AFTER ) ) |   
    DESCENDANTS( <Natural hierarchy member>, , LEAVES )  
<Natural hierarchy> ::= <Hierarchy identifier>  
<Natural hierarchy member> ::= <Natural hierarchy>.<identifier>[.<identifier>...]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência da linguagem MDX &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [Conceitos básicos do script MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
