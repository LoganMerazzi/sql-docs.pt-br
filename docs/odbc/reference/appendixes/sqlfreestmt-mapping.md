---
title: Mapeamento SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1872806265470327f3e7bff468be2ba6d9011421
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199426"
---
# <a name="sqlfreestmt-mapping"></a>Mapeamento SQLFreeStmt
Quando um aplicativo chama **SQLFreeStmt** com um *opção* argumento de SQL_DROP por meio de um ODBC 3 *. x* driver, a chamada para  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 é mapeado para  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 com o *manipular* argumento definido como o valor na *hstmt*.
