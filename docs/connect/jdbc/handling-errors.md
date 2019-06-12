---
title: Tratamento de erros | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a69bf1d98d666b0b4b76be604abc31e28958adb4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781694"
---
# <a name="handling-errors"></a>Tratando erros
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ao usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], todas as condições de erro de banco de dados são retornadas para seu aplicativo Java como exceções, usando a classe [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md). Os seguintes métodos da classe SQLServerException são herdados de java.sql.SQLException e java.lang.Throwable; e eles podem ser usados para retornar informações específicas sobre o erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ocorreu:  
  
-   O `getSQLState()` retorna o X/Open padrão ou código de estado SQL99 da exceção.
  
-   O `getErrorCode()` retorna o número de erro de banco de dados específico.
  
-   O `getMessage()` retorna o texto completo da exceção. O texto de mensagem de erro descreve o problema e geralmente inclui espaços reservados para informações, como nomes de objeto, que são inseridos na mensagem de erro quando é exibido.
  
-   O `getNextException()` retorna o próximo objeto `SQLServerException` ou nulo se não houver nenhum outro objeto de exceção para retornar.

-   `getSQLServerError()` Retorna o `SQLServerError` objeto que contém informações detalhadas sobre a exceção, como recebidos do SQL Server. Esse método retornará nulo se nenhum erro de servidor.

Os seguintes métodos do `SQLServerError` classe pode ser usado para obter detalhes adicionais sobre o erro gerado a partir do servidor.

-   `SQLServerError.getErrorMessage()` Retorna a mensagem de erro, como recebidos do servidor.

-   `SQLServerError.getErrorNumber()` Retorna um número que identifica o tipo do erro.

-   `SQLServerError.getErrorState()` Retorna um código de erro numérico do SQL Server que representa um erro, aviso ou mensagem de "nenhum dado foi encontrado".

-   `SQLServerError.getErrorSeverity()` Retorna o nível de gravidade do erro recebido.

-   `SQLServerError.getServerName()` Retorna o nome do computador que está executando uma instância do SQL Server que gerou o erro.

-   `SQLServerError.getProcedureName()` Retorna o nome do procedimento armazenado ou chamada de procedimento remoto (RPC) que gerou o erro.

-   `SQLServerError.getLineNumber()` Retorna o número de linha dentro do lote de comandos Transact-SQL ou procedimento armazenado que gerou o erro.
  
 No exemplo a seguir, uma conexão aberta para o banco de dados de amostra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função e uma instrução SQL malformada é construída, que não tem uma cláusula FROM. Em seguida, a instrução é executada e uma exceção SQL é processada.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>Consulte Também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
