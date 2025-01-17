---
title: Trabalhando com a função RollupChildren (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [MDX], RollupChildren function
- RollupChildren function
- custom member properties [MDX]
- IIf function
ms.assetid: 03c624d4-f277-451d-9995-623a07ea2f86
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 45db581de7b7aef2822597ef60d3b43ebad3acbd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074273"
---
# <a name="working-with-the-rollupchildren-function-mdx"></a>Trabalhando com a função RollupChildren (MDX)
  O MDX (Multidimensional Expressions) [RollupChildren](/sql/mdx/rollupchildren-mdx) função [Script de pesquisa e substituição] acumula os filhos de um membro, aplicando um operador unário diferente a cada filho e retorna o valor desse Rollup como um número. O operador unário pode ser fornecido por uma propriedade do membro associada ao membro filho ou pode ser uma expressão de cadeia de caracteres fornecida diretamente para a função.  
  
## <a name="rollupchildren-function-examples"></a>Exemplos da função RollupChildren  
 O uso da função `RollupChildren` em instruções MDX é simples de explicar, mas seu efeito sobre consultas MDX pode ser bastante abrangente.  
  
 O efeito da função `RollupChildren` ocorre em consultas MDX projetadas para executar a análise seletiva dos dados de um cubo. Por exemplo, a tabela a seguir contém uma lista de membros filhos do membro pai Vendas líquidas, com seus operadores unários (representados pela propriedade de membro `UNARY_OPERATOR`) mostrados entre parênteses.  
  
|Membro pai|Membro filho|  
|-------------------|------------------|  
|Vendas Líquidas|Vendas internas (+)<br /><br /> Lucros internos (-)<br /><br /> Exportações (+)<br /><br /> Lucros de exportações (-)|  
  
 O membro pai Vendas líquidas apresenta o total de vendas líquidas menos os valores brutos de vendas internas e exportações, sendo os lucros interno e de exportação subtraídos como parte do acúmulo.  
  
 Porém, você quer gerar uma previsão rápida e fácil das vendas brutas internas e exportações mais 10%, ignorando os lucros interno e de exportações. Para calcular esse valor, pode usar a função `RollupChildren` de uma destas maneiras: com uma propriedade de membro personalizado ou com a função `IIf`.  
  
### <a name="using-a-custom-member-property"></a>Usando uma propriedade de membro personalizado  
 Se o cálculo acumulado for uma operação realizada com frequência, um método seria criar uma propriedade membro capaz de armazenar o operador que será usado com cada filho para um função específica. A tabela a seguir exibe os operadores unários válidos e descreve o resultado esperado.  
  
|Operador|Resultado|  
|--------------|------------|  
|+|total = total + filho atual|  
|-|total = total – filho atual|  
|*|total = total * filho atual|  
|/|total = total / filho atual|  
|~|O filho não é usado no acúmulo. O valor do filho é ignorado.|  
  
 Por exemplo, uma propriedade de membro chamada `SALES_OPERATOR`) poderia ser criada e os seguintes operadores unários seriam atribuídos a ela, como mostrados na tabela a seguir.  
  
|Membro pai|Membro filho|  
|-------------------|------------------|  
|Vendas Líquidas|Vendas internas (+)<br /><br /> Lucros internos (~)<br /><br /> Exportações (+)<br /><br /> Lucros de exportações (~)|  
  
 Com essa nova propriedade de membro, a seguinte instrução MDX executaria a operação de estimativa das vendas brutas com rapidez e eficiência (ignorando os lucros interno e de exportação):  
  
```  
RollupChildren([Net Sales], [Net Sales].CurrentMember.Properties("SALES_OPERATOR")) * 1.1  
```  
  
 Quando a função é chamada, o valor de cada filho é aplicado ao total usando o operador armazenado na propriedade membro. Os membros de lucros interno e de exportação são ignorados e o total acumulado retornado pela função `RollupChildren` é multiplicado por 1,1.  
  
### <a name="using-the-iif-function"></a>Usando a função IIf  
 Se a operação de exemplo não for comum ou se a operação se aplica somente a uma consulta MDX, o [IIf](/sql/mdx/iif-mdx) função pode ser usada com o `RollupChildren` função para fornecer o mesmo resultado. A consulta MDX a seguir apresenta o mesmo resultado que o exemplo MDX anterior, mas sem reordenar para usar uma propriedade de membro personalizado:  
  
```  
RollupChildren([Net Sales], IIf([Net Sales].CurrentMember.Properties("UNARY_OPERATOR") = "-", "~", [Net Sales].CurrentMember.Properties("UNARY_OPERATOR))) * 1.1  
```  
  
 A instrução MDX analisa o operador unário do membro filho. Se ele for usado em uma subtração (como no caso dos membros de lucros interno e de exportação), a função `IIf` substituirá o operador unário til (~). Caso contrário, a função `IIf` utilizará o operador unário do membro filho. Por fim, o total acumulado retornado é então multiplicado por 1,1 para apresentar o valor estimado de vendas brutas internas e exportações.  
  
## <a name="see-also"></a>Consulte também  
 [Manipulando dados &#40;MDX&#41;](mdx-data-manipulation-manipulating-data.md)  
  
  
