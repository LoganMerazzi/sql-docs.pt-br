---
title: Usando uma instrução SQL com parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6716f670c42172f1721968124d7113e8f1936ddc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916373"
---
# <a name="using-an-sql-statement-with-parameters"></a>Usando uma instrução SQL com parâmetros

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para trabalhar com os dados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando uma instrução SQL contendo parâmetros IN, é possível usar o método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) da classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) para retornar um [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) que conterá os dados solicitados. Para isso, você deve primeiro criar um objeto SQLServerPreparedStatement usando o método [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

Quando você constrói a instrução SQL, os parâmetros IN são especificados usando-se o caractere ? (ponto de interrogação), que funciona como um espaço reservado para os valores de parâmetro que, posteriormente, serão passados para a instrução SQL. Para especificar um valor para um parâmetro, você pode usar um dos métodos setter da classe SQLServerPreparedStatement. O método setter que é possível pode usar é determinado pelo tipo de valor que você deseja passar para a instrução SQL.

Ao passar um valor para o método setter, você deve especificar não somente o valor real a ser usado na instrução SQL, mas também o posicionamento ordinal do parâmetro na instrução SQL. Por exemplo, se a instrução SQL contiver um único parâmetro, seu valor ordinal será 1. Se a instrução contiver dois parâmetros, o primeiro valor ordinal será 1, e o segundo valor ordinal será 2.

No exemplo a seguir, uma conexão aberta com o banco de dados de amostra [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passado para a função, uma instrução SQL preparada é criada e executada com um único valor de parâmetro String e, em seguida, os resultados são lidos do conjunto de resultados.

[!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]

## <a name="see-also"></a>Consulte Também

[Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)
