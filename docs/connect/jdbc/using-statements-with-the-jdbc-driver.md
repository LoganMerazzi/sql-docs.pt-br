---
title: Usando instruções com o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7646903fc9efcbdb838b4a2d585735dc3a105639
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005928"
---
# <a name="using-statements-with-the-jdbc-driver"></a>Usando instruções com o JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] pode ser usado para trabalhar com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de diversas formas. O driver JDBC pode ser usado para executar instruções SQL no banco de dados ou pode ser usado para chamar procedimentos armazenados no banco de dados, usando parâmetros de entrada e saída. O driver JDBC também dá suporte ao uso de sequências de escape de SQL, contagens de atualização, chaves automaticamente geradas e realização de atualizações dentro de uma operação de lote.  
  
O driver JDBC fornece três classes para recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1. [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) – usado para executar instruções SQL sem parâmetros.  
  
2. [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) – (herdado de SQLServerStatement), usado para executar instruções SQL compiladas que podem conter parâmetros IN.  
  
3. [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) – (herdado de SQLServerPreparedStatement), usado para executar procedimentos armazenados que podem conter parâmetros IN, parâmetros OUT ou ambos.  
  
 Os tópicos nesta seção discutem como você pode usar cada uma das três classes de instrução para trabalhar com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  

| Tópico                                                                                                    | Descrição                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)                             | Descreve como usar instruções SQL com o driver JDBC para trabalhar com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    |
| [Usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md) | Descreve como usar procedimentos armazenados com o driver JDBC para trabalhar com os dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. |
| [Usando vários conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md)                           | Descreve como usar o driver JDBC para recuperar dados de vários conjuntos de resultados.                                                                       |
| [Usando sequências de escape do SQL](../../connect/jdbc/using-sql-escape-sequences.md)                           | Descreve como usar sequências de escape de SQL, como literais e funções de data e hora.                                                               |
| [Usando chaves geradas automaticamente](../../connect/jdbc/using-auto-generated-keys.md)                             | Descreve como usar chaves automaticamente geradas.                                                                                                     |
| [Executando operações em lote](../../connect/jdbc/performing-batch-operations.md)                         | Descreve como usar o driver JDBC para realizar operações em lote.                                                                                      |
| [Tratando instruções complexas](../../connect/jdbc/handling-complex-statements.md)                         | Descreve como usar o driver JDBC para executar instruções complexas que realizam uma variedade de tarefas e podem retornar tipos diferentes de dados.               |
  
## <a name="see-also"></a>Consulte Também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
