---
title: '&gt;(Maior que) (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Greater
- Than
- '> (Greater Than)'
- '>_TSQL'
- Greater Than
- '>'
dev_langs:
- TSQL
helpviewer_keywords:
- greater than operator (>)
- '> (greater than operator)'
ms.assetid: 50a7b098-a3fb-4df6-ae42-1272d6346338
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 20d07527184cd767723198509bff3b55b0562595
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="gt-greater-than-transact-sql"></a>&gt;(Maior que) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Compara duas expressões (um operador de comparação) no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Ao comparar expressões não nulas, o resultado será TRUE se o operando da esquerda tiver um valor maior que o operando da direita; caso contrário, o resultado será FALSE. Se um ou ambos os operandos forem NULL, consulte o tópico [SET ANSI_NULLS &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
expression > expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md). Ambas as expressões devem ter tipos de dados implicitamente conversíveis. A conversão depende das regras de [precedência de tipo de dados](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using--in-a-simple-query"></a>A. Usando > em uma consulta simples  
 O exemplo a seguir retorna todas as linhas da tabela `HumanResources.Department` contendo um valor `DepartmentID` que seja superior ao valor 13.  
  
```  
--Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID > 13  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
14           Facilities and Maintenance  
15           Shipping and Receiving  
16           Executive  
  
(3 row(s) affected)  
  
```  
  
### <a name="b-using--to-compare-two-variables"></a>B. Usando > para comparar duas variáveis  
  
```  
DECLARE @a int = 45, @b int = 40;  
SELECT IIF ( @a > @b, 'TRUE', 'FALSE' ) AS Result;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------  
TRUE  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [IIF &#40; Transact-SQL &#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  