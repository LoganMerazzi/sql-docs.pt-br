---
title: AGRUPAMENTO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GROUPING
- GROUPING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], GROUPING function
- grouping columns
- ROLLUP operator
- GROUP BY clause, GROUPING function
- GROUPING function
- CUBE operator
ms.assetid: 4efa3868-1fc4-4626-8fb1-e863cc03e422
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d83b68d9d5fb52c67ca3a1910fe9541dfd6f5552
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="grouping-transact-sql"></a>GROUPING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Indica se uma expressão de coluna especificada em uma lista GROUP BY é agregada ou não. GROUPING retorna 1 para agregada ou 0 para não agregada no conjunto de resultados. AGRUPAMENTO pode ser usado apenas em SELECT \<selecione > Listar, HAVING e ORDER BY cláusulas quando GROUP BY é especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GROUPING ( <column_expression> )  
```  
  
## <a name="arguments"></a>Argumentos  
 \<column_expression >  
 É uma coluna ou uma expressão que contém uma coluna em uma [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) cláusula.  
  
## <a name="return-types"></a>Tipos de retorno  
 **tinyint**  
  
## <a name="remarks"></a>Comentários  
 GROUPING é usado para distinguir os valores nulos retornados por ROLLUP, CUBE ou GROUPING SETS dos valores nulos padrão. O NULL retornado como resultado de uma operação ROLLUP, CUBE ou GROUPING SETS é um uso especial de NULL. Isto atua como um espaço reservado de coluna no conjunto de resultados e significa tudo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir agrupa `SalesQuota` e agrega quantias de `SaleYTD` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A função `GROUPING` é aplicada à coluna `SalesQuota`.  
  
```  
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 O conjunto de resultados mostra dois valores nulos em `SalesQuota`. O primeiro `NULL` representa o grupo de valores nulos desta coluna na tabela. O segundo `NULL` está na linha de resumo somada pela operação ROLLUP. A linha de resumo mostra o `TotalSalesYTD` valores para todos os `SalesQuota` grupos e é indicada por `1` no `Grouping` coluna.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `SalesQuota     TotalSalesYTD       Grouping`  
  
 `------------   -----------------   --------`  
  
 `NULL           1533087.5999          0`  
  
 `250000.00      33461260.59           0`  
  
 `300000.00      9299677.9445          0`  
  
 `NULL           44294026.1344         1`  
  
 `(4 row(s) affected)`  
  
## <a name="see-also"></a>Consulte também  
 [GROUPING_ID &#40; Transact-SQL &#41;](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY &#40; Transact-SQL &#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  