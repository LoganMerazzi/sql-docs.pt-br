---
title: Usando uma instrução SQL para modificar dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cbcdf01eed0114e1788f23cec3a24cf4a69329e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004017"
---
# <a name="using-an-sql-statement-to-modify-data"></a>Usando uma instrução SQL para modificar dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para modificar os dados contidos em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando-se uma instrução SQL, é possível usar o método [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). O método executeUpdate passará a instrução SQL para o banco de dados para processamento e, em seguida, retornará um valor que indica o número de linhas afetadas.

Para isso, você deve primeiro criar um objeto SQLServerStatement usando o método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

No exemplo a seguir, uma conexão aberta com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função; é construída uma instrução SQL que adiciona novos dados à tabela; em seguida, a instrução é executada e o valor retornado é exibido.

[!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]

> [!NOTE]  
> Se você precisar usar uma instrução SQL que contenha parâmetros pra modificar os dados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deverá usar o método [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) da classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).
>
> Se a coluna em que estiver tentando inserir dados contiver caracteres especiais como espaços, você deverá fornecer os valores a serem inseridos, mesmo se forem valores padrão. Se isso não acontecer, haverá falha na operação.
>
> Se você quiser que o driver JDBC retorne todas as contagens de atualização, inclusive contagens de atualização retornadas por gatilhos que possam ter sido acionados, defina a propriedade da cadeia de conexão lastUpdateCount como "false". Para obter mais informações sobre a propriedade lastUpdateCount, consulte [definindo as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md).

## <a name="see-also"></a>Consulte Também

[Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)
