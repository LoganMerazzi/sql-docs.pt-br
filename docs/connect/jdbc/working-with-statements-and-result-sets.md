---
title: Trabalhando com instruções e conjuntos de resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cc917534-f5f8-4844-87c8-597c48b4e06d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb6d545a3a7f8c3b29e5bc372aa4fdadf95edd52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003791"
---
# <a name="working-with-statements-and-result-sets"></a>Trabalhando com instruções e conjuntos de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando você trabalha com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] e os objetos Statement e ResultSet fornecidos por ele, há várias técnicas a serem empregadas para melhorar o desempenho e a confiabilidade dos aplicativos.

## <a name="use-the-appropriate-statement-object"></a>Use o objeto de instrução apropriado

Quando você usa um dos objetos de Instrução do driver JDBC, como o objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) ou [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), verifique se você está usando o objeto apropriado para o trabalho.

- Se você não tiver parâmetros de saída, não será necessário usar o objeto SQLServerCallableStatement. Em vez disso, use o objeto SQLServerStatement ou SQLServerPreparedStatement.

- Se você não pretende executar a instrução mais de uma vez ou não tem parâmetros de entrada ou saída, não é necessário usar o objeto SQLServerCallableStatement ou SQLServerPreparedStatement. Em vez disso, use o objeto SQLServerStatement.

## <a name="use-the-appropriate-concurrency-for-resultset-objects"></a>Use a simultaneidade apropriada para objetos ResultSet

Não peça simultaneidade atualizável ao criar instruções que geram conjuntos de resultados a menos que você realmente pretenda atualizar os resultados. O modelo de cursor padrão somente avanço, somente leitura é o mais rápido para ler conjuntos de resultados pequenos.

## <a name="limit-the-size-of-your-result-sets"></a>Limitar o tamanho dos seus conjuntos de resultados

Considere usar o método [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) (ou a sintaxe de SQL SET ROWCOUNT ou SELECT TOP N) para limitar o número de linhas retornado de conjuntos de resultados potencialmente grandes. Se você precisa lidar com conjuntos de resultados grandes, use um buffer de resposta adaptável configurando a propriedade da cadeia de conexão responseBuffering=adaptive, que é o modo padrão. Esta abordagem permite que o aplicativo processe conjuntos de resultados grandes sem exigir cursores do lado do servidor e minimiza o uso de memória de aplicativo. Para obter mais informações, consulte [usando o buffer adaptável](../../connect/jdbc/using-adaptive-buffering.md).

## <a name="use-the-appropriate-fetch-size"></a>Use o tamanho da busca apropriado

Para cursores de servidor somente leitura, é preciso haver equilíbrio entre as viagens de ida e volta ao servidor e a quantidade de memória usada no driver. Para cursores de servidor atualizáveis, o tamanho da busca influencia também a sensibilidade do conjunto de resultados a alterações e simultaneidade no servidor. As atualizações para linhas dentro do buffer de busca atual não são visíveis até que um método [refreshRow](../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md) explícito seja emitido ou até que o cursor deixe o buffer de busca. Os buffers de busca grandes terão melhor desempenho (menos viagens de ida e volta ao servidor), mas são menos sensíveis a alterações e reduzirão a simultaneidade no servidor se CONCUR_SS_SCROLL_LOCKS (1009) for usado. Para obter sensibilidade máxima a alterações, use um tamanho da busca de 1. Porém, observe que isto implicará uma viagem de ida e volta ao servidor para cada linha buscada.

## <a name="use-streams-for-large-in-parameters"></a>Usar fluxos para parâmetros IN grandes

Use fluxos ou BLOBs e CLOBs que são materializados incrementalmente para gerenciar atualização de valores de coluna grandes ou enviar parâmetros IN grandes. O driver JDBC "corta" essas partes para o servidor em várias viagens de ida e volta, permitindo definir e atualizar valores maiores que o que caberá na memória.

## <a name="see-also"></a>Consulte Também

[Melhorando o desempenho e a confiabilidade com o JDBC Driver](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
