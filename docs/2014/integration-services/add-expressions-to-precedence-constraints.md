---
title: Adicionar expressões às restrições de precedência | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- precedence executables [Integration Services]
- precedence constraints [Integration Services], adding expressions
- adding expressions
- constrained executables [Integration Services]
- combining constraints
- expressions [Integration Services], constraints
ms.assetid: 5574d89a-a68e-4b84-80ea-da93305e5ca1
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4066b5b5c6ebd18d6dbbf02f6a150770d5e3b51f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115496"
---
# <a name="add-expressions-to-precedence-constraints"></a>Adicionar expressões a restrições de precedência
  Uma restrição de precedência pode usar uma expressão para definir a restrição entre dois executáveis: o executável de precedência e o executável de restrição. Os executáveis podem ser tarefas ou contêineres. A expressão pode ser usada sozinha ou em combinação com o resultado de execução do executável da restrição. O resultado da execução de um executável pode ter sucesso ou falha. Quando você configura o resultado de execução de uma restrição de precedência, pode definir o resultado de execução como `Success`, `Failure` ou `Completion`. `Success` exige que o executável de precedência tenha sucesso, `Failure` exige que o executável de precedência falhe e `Completion` indica que o executável de restrição deve ser executado independentemente da tarefa de restrição ter sucesso ou falhar. Para obter mais informações, consulte [Precedence Constraints](control-flow/precedence-constraints.md).  
  
 A expressão deve avaliar como `True` ou `False` e deve ser uma expressão [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] válida. A expressão pode usar literais, variáveis personalizadas e de sistema e as funções e operadores que a gramática de expressão [!INCLUDE[ssIS](../includes/ssis-md.md)] fornece. Por exemplo, a expressão `@Count == SQRT(144) + 10` usa a variável `Count`, a função SQRT e os operadores de igual (==) e soma (+). Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 Na ilustração a seguir, as tarefas A e B estão vinculadas por uma restrição de precedência que usa um resultado de execução e uma expressão. O valor da restrição é definido como `Success` e a expressão é `@X >== @Z`. A tarefa B, a tarefa de restrição, só é executada se a tarefa A for concluída com sucesso e o valor da variável `X` for maior que ou igual ao valor da variável `Z`.  
  
 ![Restrição de precedência entre duas tarefas](media/mw-dts-03.gif "Restrição de precedência entre duas tarefas")  
  
 Os executáveis também podem ser vinculados usando múltiplas restrições de precedência que contenham expressões diferentes. Por exemplo, na ilustração a seguir, as tarefas B e C estão vinculadas à tarefa A por restrições de precedência que usam resultados de execução e expressões. Ambos os valores de restrição são definidos como `Success.` uma restrição de precedência inclui a expressão `@X >== @Z`, e a restrição de precedência inclui a expressão `@X < @Z`. Dependendo dos valores da variável `X` e da variável `Z`, uma das tarefas C ou B será executada.  
  
 ![Expressões em restrições de precedência](media/mw-dts-04.gif "Expressões em restrições de precedência")  
  
 Você pode adicionar ou modificar uma expressão usando o **Editor de Restrição de Precedência** no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)], e a janela Propriedades que o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fornece. Entretanto, a janela Propriedades não fornece verificação da sintaxe de expressão.  
  
 Se uma restrição de precedência incluir uma expressão, um ícone será exibido na superfície de design da guia **Fluxo de Controle** , próximo à restrição de precedência e a dica de ferramenta sobre o ícone exibirá a expressão.  
  
## <a name="combining-execution-values-and-expressions"></a>Combinando valores de execução e expressões  
 A tabela a seguir descreve os efeitos de combinar uma restrição de valor de execução e uma expressão em uma restrição de precedência.  
  
|Operação de avaliação|A restrição avalia como|A expressão avalia como|O executável restrito executa|  
|--------------------------|-----------------------------|-----------------------------|---------------------------------|  
|Constraint|True|N/A|True|  
|Constraint|Falso|N/A|Falso|  
|Expression|N/A|True|Verdadeiro|  
|Expression|N/A|Falso|Falso|  
|Restrição e expressão|True|True|True|  
|Restrição e expressão|True|Falso|Falso|  
|Restrição e expressão|Falsa|True|Falso|  
|Restrição e expressão|Falso|Falso|Falso|  
|Restrição ou expressão|True|True|Verdadeira|  
|Restrição ou expressão|True|Falso|True|  
|Restrição ou expressão|Falso|True|Verdadeira|  
|Restrição ou expressão|Falso|Falso|Falso|  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>Como adicionar uma expressão a uma restrição de precedência  
  
-   [Usar uma expressão em uma restrição de precedência](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
-   [Definir as propriedades de uma restrição de precedência](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
## <a name="external-resources"></a>Recursos externos  
 Artigo técnico, [Exemplos de expressões SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), em social.technet.microsoft.com  
  
## <a name="see-also"></a>Consulte também  
 [Várias restrições de precedência](../../2014/integration-services/multiple-precedence-constraints.md)   
 [Restrições de precedência](control-flow/precedence-constraints.md)  
  
  