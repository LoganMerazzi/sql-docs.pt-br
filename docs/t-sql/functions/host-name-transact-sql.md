---
title: HOST_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HOST_NAME_TSQL
- HOST_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- HOST_NAME function
- workstation names [SQL Server]
ms.assetid: 4b8b0705-c083-4b07-b954-c83ee73b2ebb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c39d56ec338be798f9e9dd5589d3a63a65b95d6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024407"
---
# <a name="hostname-transact-sql"></a>HOST_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna o nome da estação de trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HOST_NAME ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
 Quando o parâmetro para uma função de sistema for opcional, o banco de dados atual, o computador host, o usuário do servidor ou o usuário do banco de dados será presumido. As funções internas sempre devem ser seguidas por parênteses.  
  
 As funções de sistema podem ser usadas na lista de seleção, na cláusula WHERE e em qualquer local onde uma expressão for permitida.  
  
> [!IMPORTANT]  
>  O aplicativo cliente fornece o nome da estação de trabalho e pode fornecer dados inexatos. Não confie em HOST_NAME como um recurso de segurança.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma tabela que usa `HOST_NAME()` em uma definição `DEFAULT` para registrar o nome da estação de trabalho dos computadores que inserem linhas em uma tabela que registra ordens.  
  
```  
CREATE TABLE Orders  
   (OrderID     int        PRIMARY KEY,  
    CustomerID  nchar(5)   REFERENCES Customers(CustomerID),  
    Workstation nchar(30)  NOT NULL DEFAULT HOST_NAME(),  
    OrderDate   datetime   NOT NULL,  
    ShipDate    datetime   NULL,  
    ShipperID   int        NULL REFERENCES Shippers(ShipperID));  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
