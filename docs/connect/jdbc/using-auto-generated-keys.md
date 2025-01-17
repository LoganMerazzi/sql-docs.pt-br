---
title: Usando chaves geradas automaticamente | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 55a062c7-45ce-40e3-9a6f-4a0f4da4e2a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55541d7487f27a6fa4e38fef8baf47a6ef3ff6d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003989"
---
# <a name="using-auto-generated-keys"></a>Usando chaves geradas automaticamente

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dá suporte às APIs opcionais do JDBC 3.0 para recuperar identificadores de linha gerados automaticamente. O principal valor deste recurso é fornecer um modo de disponibilizar valores de IDENTITY para um aplicativo que esteja atualizando uma tabela de banco de dados sem precisar de uma consulta e de uma segunda viagem de ida e volta ao servidor.

Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é compatível com pseudocolunas para identificadores, as atualizações que precisam usar o recurso de chave gerada automaticamente devem operar em uma tabela que contém uma coluna IDENTITY. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite somente uma única coluna IDENTITY por tabela. O conjunto de resultados retornado pelo método [getGeneratedKeys](../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) só terá uma coluna, com o nome de coluna retornado GENERATED_KEYS. Se forem solicitadas chaves geradas em uma tabela que não tenha uma coluna de IDENTITY, o driver JDBC retornará um conjunto de resultados nulo.

Como exemplo, crie a seguinte tabela no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE TABLE TestTable
   (Col1 int IDENTITY,
    Col2 varchar(50),
    Col3 int);  
```

No exemplo a seguir, uma conexão aberta com o banco de dados de exemplo da [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função; é construída uma instrução SQL que adicionará dados à tabela; em seguida, a instrução é executada e o valor da coluna de IDENTITY é exibido.

[!code[JDBC#UsingAutoGeneratedKeys1](../../connect/jdbc/codesnippet/Java/using-auto-generated-keys_1.java)]

## <a name="see-also"></a>Consulte Também

[Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)
