---
title: Transações em ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f076622b30d1f1102bac8ff6c89ecf2e36a96860
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913160"
---
# <a name="performing-transactions-in-odbc"></a>Executar transações no ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  As transações em ODBC são gerenciadas no nível da conexão. Quando um aplicativo conclui uma transação, ele confirma ou reverte todo o trabalho concluído através de todos os identificadores de instrução nessa conexão. Para confirmar ou reverter uma transação, os aplicativos devem chamar [SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md) , em vez de enviar uma instrução COMMIT ou ROLLBACK.  
  
 Um aplicativo chama [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para alternar entre os dois modos ODBC de gerenciamento de transações:  
  
-   Modo de confirmação automática  
  
     Cada instrução é confirmada automaticamente quando concluída com êxito. Quando o modo de confirmação automática é executado, nenhuma outra função de gerenciamento de transação é necessária.  
  
-   Modo de confirmação manual  
  
     Todas as instruções executadas são incluídas na mesma transação até que ela seja interrompida especificamente chamando **SQLEndTran**.  
  
 O modo de confirmação automática é o modo de transação padrão para ODBC. Quando uma conexão é estabelecida, ela está em modo de confirmação automática até **SQLSetConnectAttr** ser chamado para alternar para o modo de confirmação manual desativando o modo de confirmação automática. Quando um aplicativo desativa a confirmação automática, a instrução seguinte enviada para o banco de dados inicia uma transação. A transação permanece ativa até que o aplicativo chame **SQLEndTran** com as opções SQL_COMMIT ou SQL_ROLLBACK. O comando enviado para o banco de dados após **SQLEndTran** inicia a transação seguinte.  
  
 Se um aplicativo alternar do modo de confirmação manual para o modo de confirmação automática, o driver confirmará todas as transações abertas na conexão no momento.  
  
 Os aplicativos ODBC não devem usar instruções de transação Transact-SQL como BEGIN TRANSACTION, COMMIT TRANSACTION ou ROLLBACK TRANSACTION porque isso pode causar um comportamento indeterminado no driver. Um aplicativo ODBC deve ser executado em modo de confirmação automática e não deve usar nenhuma função ou instrução de gerenciamento de transações, ou deve ser executado em modo de confirmação manual e usar a função **SQLEndTran** de ODBC para confirmar ou reverter transações.  
  
## <a name="see-also"></a>Consulte também  
 [Executando transações &#40;ODBC&#41;](https://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
