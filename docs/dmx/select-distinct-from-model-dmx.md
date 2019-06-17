---
title: SELECT DISTINCT FROM &lt;model &gt; (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 95a8a1d40792c2993d44624a321bccf99030e181
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62658888"
---
# <a name="select-distinct-from-ltmodel-gt-dmx"></a>SELECT DISTINCT FROM &lt;model &gt; (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna todos os possíveis estados para a coluna selecionada no modelo. Os valores retornados variam dependendo se a coluna especificada contém valores discretos, valores numéricos diferenciados ou valores numéricos contínuos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT [FLATTENED] DISTINCT [TOP <n>] <expression list> FROM <model>   
[WHERE <condition list>][ORDER BY <expression>]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Número inteiro que especifica quantas linhas serão retornadas.  
  
 *lista de expressões*  
 Lista de identificadores, separada por vírgulas, de colunas ou expressões relacionadas (derivadas do modelo).  
  
 *modelo*  
 Identificador de modelo.  
  
 *lista de condições*  
 Uma condição para restringir os valores retornados da lista de colunas.  
  
 *Expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 O **SELECT DISTINCT FROM** instrução só funciona com uma única coluna ou com um conjunto de colunas relacionadas. Essa cláusula não funciona com um conjunto de colunas não relacionadas.  
  
 O **SELECT DISTINCT FROM** instrução permite que você faça referência diretamente a uma coluna dentro de uma tabela aninhada. Por exemplo:  
  
```  
<model>.<table column reference>.<column reference>  
```  
  
 Os resultados do **SELECT DISTINCT FROM \<modelo >** instrução variam, dependendo do tipo de coluna. A tabela a seguir descreve os tipos de coluna com suporte e a saída da instrução.  
  
|Tipo de coluna|Saída|  
|-----------------|------------|  
|Discreto|Valores únicos na coluna.|  
|Discretizado|Ponto central de cada partição diferenciada na coluna.|  
|Contínuo|Ponto central para os valores da coluna.|  
  
## <a name="discrete-column-example"></a>Exemplo de coluna Discrete  
 O exemplo de código a seguir se baseia a `[TM Decision Tree]` criadas no modelo a [Tutorial básico de mineração de dados](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). A consulta retorna os valores exclusivos que existem na coluna discreta `Gender`.  
  
```  
SELECT DISTINCT [Gender]  
FROM [TM Decision Tree]  
```  
  
 Resultados do exemplo:  
  
|Gênero|  
|------------|  
||  
|F|  
|M|  
  
 Para colunas que contêm valores discretos, os resultados incluem sempre o estado Ausente, mostrado como um valor nulo.  
  
## <a name="continuous-column-example"></a>Exemplo de coluna Continuous  
 O exemplo de código a seguir retorna os valores de ponto central, idade máxima e idade mínima para todos os valores na coluna.  
  
```  
SELECT DISTINCT [Age] AS [Midpoint Age],   
    RangeMin([Age]) AS [Minimum Age],   
    RangeMax([Age]) AS [Maximum Age]  
FROM [TM Decision Tree]  
```  
  
 Resultados do exemplo:  
  
|Idade de ponto médio|Idade mínima|Idade máxima|  
|------------------|-----------------|-----------------|  
||||  
|62|26|97|  
  
 A consulta também retorna uma única linha de valores nulos, para representar valores ausentes.  
  
## <a name="discretized-column-example"></a>Exemplo de coluna Discretized  
 O exemplo de código a seguir retorna os valores de ponto médio, máximo e mínimo de cada bucket criado pelo algoritmo para a coluna, [`Yearly Income]`. Para reproduzir os resultados deste exemplo, crie uma nova estrutura de mineração igual à de `[Targeted Mailing]`. No assistente, altere o tipo de conteúdo a `Yearly Income` coluna a partir **contínuo** à **Discretized**.  
  
> [!NOTE]  
>  Também é possível alterar o modelo de mineração criado no Tutorial Mineração Básica para diferenciar a coluna da estrutura de mineração, [`Yearly Income]`. Para obter informações sobre como fazer isso, consulte [alterar a diferenciação de uma coluna em um modelo de mineração](../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md). No entanto, quando você altera a diferenciação da coluna, isso força a estrutura de mineração a ser reprocessada, o que altera os resultados dos outros modelos criados com o uso dessa estrutura.  
  
```  
SELECT DISTINCT [Yearly Income] AS [Bucket Average],   
    RangeMin([Yearly Income]) AS [Bucket Minimum],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
 Resultados do exemplo:  
  
|Média de bucket|Mínimo de bucket|Máximo de bucket|  
|--------------------|--------------------|--------------------|  
||||  
|24610.7|10000|39221.41|  
|55115.73|39221.41|71010.05|  
|84821.54|71010.05|98633.04|  
|111633.9|98633.04|124634.7|  
|147317.4|124634.7|170000|  
  
 Você pode observar que os valores da coluna [Renda Anual] foram diferenciados em cinco buckets, mais uma linha adicional de valores nulos, para representar valores ausentes.  
  
 O número de casas decimais nos resultados depende do cliente usado para a consulta. Aqui, elas foram arredondadas para duas casas decimais, para simplificar e refletir os valores exibidos no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Por exemplo, se você procurar o modelo usando o visualizador de Árvore de Decisão e clicar em um nó que contenha os clientes agrupados por renda, as propriedades de nó a seguir serão exibidas na Dica de Ferramenta:  
  
 Idade > = gt;=69 AND Renda anual < 39221.41  
  
> [!NOTE]  
>  O valor mínimo do bucket mínimo e o valor máximo do bucket máximo são apenas os valores mais alto e mais baixo observados. Os valores dentro desse intervalo observado são considerados como pertencentes aos buckets mínimo e máximo.  
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
