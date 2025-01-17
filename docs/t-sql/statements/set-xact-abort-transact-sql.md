---
title: SET XACT_ABORT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- XACT_ABORT_TSQL
- XACT_ABORT
- SET XACT_ABORT
- SET_XACT_ABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- XACT_ABORT option
- automatic transaction roll backs
- transactions [SQL Server], rolling back
- rolling back transactions, SET XACT_ABORT
- roll back transactions [SQL Server]
- SET XACT_ABORT statement
ms.assetid: cbcaa433-58f2-4dc3-a077-27273bef65b5
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5e46cccf161d06d6c44ab7a00923c7e6df7f27c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100060"
---
# <a name="set-xactabort-transact-sql"></a>SET XACT_ABORT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

    
> [!NOTE]  
>  A instrução **THROW** segue **SET XACT_ABORT**. Isso não ocorre com **RAISERROR**. Os novos aplicativos devem usar **THROW** em vez de **RAISERROR**.  
  
 Especifica se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reverte automaticamente a transação atual quando uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] gerar um erro em tempo de execução.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```    
SET XACT_ABORT { ON | OFF }  
```  

  
## <a name="remarks"></a>Remarks  
 Quando SET XACT_ABORT for ON, se uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] gerar um erro em tempo de execução, a transação inteira será encerrada e revertida.  
  
 Quando SET XACT_ABORT é OFF, em alguns casos, somente a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que gerou o erro é revertida e a transação continua a ser processada. Dependendo da gravidade do erro, a transação inteira pode ser revertida mesmo quando SET XACT_ABORT é OFF. OFF é a configuração padrão.  
  
 Os erros de compilação, como erros de sintaxe, não são afetados por SET XACT_ABORT.  
  
 XACT_ABORT deve ser definido como ON para instruções de modificação de dados em uma transação implícita ou explícita na maioria dos provedores OLE DB, incluindo o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O único caso em que essa opção não é necessária é quando o provedor oferece suporte a transações aninhadas.  
  
 Quando ANSI_WARNINGS=OFF, as violações de permissões causam anulação das transações.  
  
 A configuração de SET XACT_ABORT é definida no momento da execução ou em tempo de execução e não no momento da análise.  
  
 Para exibir a configuração atual dessa configuração, execute a consulta a seguir.  
  
```  
DECLARE @XACT_ABORT VARCHAR(3) = 'OFF';  
IF ( (16384 & @@OPTIONS) = 16384 ) SET @XACT_ABORT = 'ON';  
SELECT @XACT_ABORT AS XACT_ABORT;  
  
```  
  
## <a name="examples"></a>Exemplos  
 O exemplo de código a seguir causa um erro de violação de chave estrangeira em uma transação com outras instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. No primeiro conjunto de instruções, o erro é gerado, mas as outras instruções são executadas com êxito e a transação é confirmada com êxito. No segundo conjunto de instruções, `SET XACT_ABORT` é definido como `ON`. Isto faz o erro de instrução encerrar o lote e a transação ser revertida.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N't2', N'U') IS NOT NULL  
    DROP TABLE t2;  
GO  
IF OBJECT_ID(N't1', N'U') IS NOT NULL  
    DROP TABLE t1;  
GO  
CREATE TABLE t1  
    (a INT NOT NULL PRIMARY KEY);  
CREATE TABLE t2  
    (a INT NOT NULL REFERENCES t1(a));  
GO  
INSERT INTO t1 VALUES (1);  
INSERT INTO t1 VALUES (3);  
INSERT INTO t1 VALUES (4);  
INSERT INTO t1 VALUES (6);  
GO  
SET XACT_ABORT OFF;  
GO  
BEGIN TRANSACTION;  
INSERT INTO t2 VALUES (1);  
INSERT INTO t2 VALUES (2); -- Foreign key error.  
INSERT INTO t2 VALUES (3);  
COMMIT TRANSACTION;  
GO  
SET XACT_ABORT ON;  
GO  
BEGIN TRANSACTION;  
INSERT INTO t2 VALUES (4);  
INSERT INTO t2 VALUES (5); -- Foreign key error.  
INSERT INTO t2 VALUES (6);  
COMMIT TRANSACTION;  
GO  
-- SELECT shows only keys 1 and 3 added.   
-- Key 2 insert failed and was rolled back, but  
-- XACT_ABORT was OFF and rest of transaction  
-- succeeded.  
-- Key 5 insert error with XACT_ABORT ON caused  
-- all of the second transaction to roll back.  
SELECT *  
    FROM t2;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
