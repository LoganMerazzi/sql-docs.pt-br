---
title: TopCount (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 48621e242fae86b0b9fca689149ed1364cb7ff1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079841"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o número especificado de linhas superiores em ordem decrescente de classificação, conforme especificado por uma expressão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Uma expressão que retorna uma tabela, como um \<referência de coluna de tabela >, ou uma função que retorna uma tabela.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<expressão de tabela >  
  
## <a name="remarks"></a>Comentários  
 O valor fornecido pelo \<expressão de classificação > argumento determina a ordem decrescente de classificação para as linhas que são fornecidos no \<expressão de tabela > argumento e o número de linhas superiores especificado na \<contagem > argumento será retornado.  
  
 A função TopCount originalmente foi introduzida para permitir previsões associativas e, em geral, produz os mesmos resultados que uma instrução que inclui **SELECT TOP** e **ORDER BY** cláusulas. Você obterá melhor desempenho para previsões associativas se você usar o **prever (DMX)** função, que oferece suporte à especificação de um número de previsões a serem retornadas.  
  
 No entanto, há situações em que você talvez ainda precise usar TopCount. Por exemplo, o DMX não oferece suporte a **superior** qualificador em uma instrução de Subseleção. O [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) função também não oferece suporte a adição de **superior**.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir são consultas de previsão no modelo de associação que você compila usando o [Tutorial básico de mineração de dados](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). As consultas retornam os mesmos resultados, mas o primeiro exemplo usa TopCount e o segundo exemplo usa a função Predict.  
  
 Para entender como funciona o TopCount, pode ser útil primeiro executar uma consulta de previsão que retorna apenas a tabela aninhada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  Neste exemplo, o valor fornecido como entrada contém uma única aspa e, portanto, deve ser precedido por outra aspa. Se você não tiver certeza da sintaxe para inserção de um caractere de escape, use o Construtor de Consultas de Previsão para criar a consulta. Quando você seleciona o valor da lista suspensa, o caractere de escape exigido é inserido. Para obter mais informações, consulte [criar uma consulta Singleton no Designer de mineração de dados](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md).  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Tubo de pneu de estrada|1588|0.106727603|0.101229538|  
|Capacete para Ciclismo|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
  
 A função TopCount utiliza os resultados dessa consulta e retorna o número especificado de linhas de menor valor.  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 O primeiro argumento para a função TopCount é o nome de uma coluna de tabela. Neste exemplo, a tabela aninhada é retornada ao chamar a função Predict e usando o argumento INCLUDE_STATISTICS.  
  
 O segundo argumento para a função TopCount é a coluna na tabela aninhada que você usa para ordenar os resultados. Neste exemplo, a opção INCLUDE_STATISTICS retorna as colunas $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. Este exemplo usa $SUPPORT para classificar os resultados.  
  
 O terceiro argumento para a função TopCount Especifica o número de linhas a serem retornadas como um número inteiro. Para obter os três principais produtos, ordenados por $SUPPORT, digite 3.  
  
 Resultados do exemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29...|0,25...|  
|Water Bottle|2866|0.19...|0.17...|  
|Patch kit|2113|0,14...|0.13...|  
  
 No entanto, esse tipo de consulta pode afetar o desempenho em uma configuração de produção. Isso é porque a consulta retorna um conjunto de todas as previsões do algoritmo, classifica essas previsões e retorna as três principais.  
  
 O exemplo a seguir fornece uma instrução alternativa que retorna os mesmos resultados, mas é executada de maneira significativamente mais rápida. Este exemplo substitui TopCount com a função de previsão, que aceita um número de previsões como um argumento. Este exemplo também usa o **$SUPPORT** palavra-chave para recuperar diretamente a coluna de tabela aninhada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 Os resultados contêm as três principais previsões classificadas pelo valor de suporte. Você pode substituir $SUPPORT por $PROBABILITY ou $ADJUSTED_PROBABILITY para retornar previsões classificadas por probabilidade ou probabilidade ajustada. Para obter mais informações, consulte **prever (DMX)** .  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
