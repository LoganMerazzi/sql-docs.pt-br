---
title: COL_LENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COL_LENGTH
- COL_LENGTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lengths [SQL Server], columns
- COL_LENGTH function
- column properties [SQL Server]
- column length [SQL Server]
ms.assetid: cf891206-c49f-40eb-858e-eefd2b638a33
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bf23672374db7d8348154e95ca6228723934aa5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064726"
---
# <a name="collength-transact-sql"></a>COL_LENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função retorna o comprimento definido de uma coluna em bytes.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COL_LENGTH ( 'table' , 'column' )   
```  
  
## <a name="arguments"></a>Argumentos  
**'** *table* **'**  
O nome da tabela cujas informações de comprimento de coluna queremos determinar. *table* é uma expressão do tipo **nvarchar**.
  
**'** *column* **'**  
O nome da coluna cujo comprimento queremos determinar. *column* é uma expressão do tipo **nvarchar**.
  
## <a name="return-type"></a>Tipo de retorno
**smallint**
  
## <a name="exceptions"></a>Exceções  
Retornará NULL em caso de erro ou se um chamador não tiver a permissão correta para exibir o objeto.
  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário pode exibir apenas os metadados de itens protegíveis de sua propriedade ou para os quais ele tenha recebido permissão. Isso significa que as funções internas que emitem metadados, como COL_LENGTH, poderão retornar NULL se o usuário não tiver a permissão correta para o objeto. Veja [Configuração de Visibilidade de Metadados](../../relational-databases/security/metadata-visibility-configuration.md) para obter mais informações.
  
## <a name="remarks"></a>Remarks  
Para colunas **varchar** declaradas com o especificador **max** (**varchar(max)** ), COL_LENGTH retornará o valor -1.
  
## <a name="examples"></a>Exemplos  
Este exemplo mostra os valores retornados para uma coluna do tipo `varchar(40)` e uma coluna do tipo `nvarchar(40)`:
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE t1(c1 varchar(40), c2 nvarchar(40) );  
GO  
SELECT COL_LENGTH('t1','c1')AS 'VarChar',  
      COL_LENGTH('t1','c2')AS 'NVarChar';  
GO  
DROP TABLE t1;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
VarChar     NVarChar  
40          80  
```  
  
## <a name="see-also"></a>Confira também
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COL_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/col-name-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)
  
  
