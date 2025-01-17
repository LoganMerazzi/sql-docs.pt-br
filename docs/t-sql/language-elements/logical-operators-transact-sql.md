---
title: Operadores lógicos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], logical
- testing truth
- truth testing
- "TRUE"
- "FALSE"
- logical operators [SQL Server], Transact-SQL
ms.assetid: edd92f08-76fb-4fd7-a4b6-8520d6a81df1
author: rothja
ms.author: jroth
ms.openlocfilehash: a26896076c0c9ee12eae61a3e324090379b10df2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122133"
---
# <a name="logical-operators-transact-sql"></a>Operadores lógicos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Os operadores lógicos testam a legitimidade de algumas condições. Os operadores lógicos, como operadores de comparação, retornam um tipo de dados **Boolean** com um valor TRUE, FALSE ou UNKNOWN.  
  
|Operador|Significado|  
|--------------|-------------|  
|[ALL](../../t-sql/language-elements/all-transact-sql.md)|TRUE se tudo em um conjunto de comparações for TRUE.|  
|[AND](../../t-sql/language-elements/and-transact-sql.md)|TRUE se as duas expressões boolianas forem TRUE.|  
|[ANY](../../t-sql/language-elements/any-transact-sql.md)|TRUE se qualquer conjunto de comparações for TRUE.|  
|[BETWEEN](../../t-sql/language-elements/between-transact-sql.md)|TRUE se o operando estiver dentro de um intervalo.|  
|[EXISTS](../../t-sql/language-elements/exists-transact-sql.md)|TRUE se uma subconsulta tiver qualquer linha.|  
|[IN](../../t-sql/language-elements/in-transact-sql.md)|TRUE se o operando for igual a um de uma lista de expressões.|  
|[LIKE](../../t-sql/language-elements/like-transact-sql.md)|TRUE se o operando corresponder a um padrão.|  
|[NOT](../../t-sql/language-elements/not-transact-sql.md)|Inverte o valor de qualquer outro operador booliano.|  
|[OR](../../t-sql/language-elements/or-transact-sql.md)|TRUE se qualquer expressão booliana for TRUE.|  
|[SOME](../../t-sql/language-elements/some-any-transact-sql.md)|TRUE se algum conjunto de comparações for TRUE.|  
  
## <a name="see-also"></a>Consulte Também  
 [Precedência do operador &#40;Transact-SQL&#41;](../../t-sql/language-elements/operator-precedence-transact-sql.md)  
  
  
