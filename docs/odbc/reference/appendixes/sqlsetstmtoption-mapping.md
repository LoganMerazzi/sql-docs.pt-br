---
title: Mapeamento SQLSetStmtOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad53ba3fa02107d4902c43084beadda7a420e586
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735297"
---
# <a name="sqlsetstmtoption-mapping"></a>Mapeamento SQLSetStmtOption
Quando um aplicativo chama **SQLSetStmtOption** por meio de um ODBC 3 *. x* driver, a chamada para  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 resulta da seguinte maneira:  
  
-   Se *fOption* indica um atributo de instrução definidas pelo ODBC é uma cadeia de caracteres, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indica um atributo de instrução definidas pelo ODBC que retorna um valor inteiro de 32 bits, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indica um atributo de instrução definidos pelo driver, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 Nos três casos anteriores, o **StatementHandle** argumento é definido como o valor na *hstmt*, o *atributo* argumento é definido como o valor em *fOption* e o *ValuePtr* argumento é definido como o valor de *vParam*.  
  
 Porque o Gerenciador de Driver não sabe se o atributo de instrução definidos pelo driver precisa de uma cadeia de caracteres ou um valor de inteiro de 32 bits, ele deve passar um valor válido para o *StringLength* argumento de **SQLSetStmtAttr**. Se o driver definiu semântica especial para atributos de instrução definidos pelo driver e precisa ser chamado usando **SQLSetStmtOption**, ele deve suportar **SQLSetStmtOption**.  
  
 Se um aplicativo chamar **SQLSetStmtOption** para definir uma opção de instrução específicos de driver em um ODBC 3 *. x* driver e a opção foi definida em um ODBC 2. *x* versão do driver, uma nova constante de manifesto deve ser definido para a opção em ODBC 3 *. x* driver. Se a constante de manifesto antiga é usada na chamada para **SQLSetStmtOption**, o Gerenciador de Driver chamará **SQLSetStmtAttr** com o *StringLength* argumento definido como 0.  
  
 Quando um aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_USE_BOOKMARKS como SQL_UB_ON em um ODBC 3 *. x* driver, o atributo da instrução SQL_ATTR_USE_BOOKMARKS está definido como SQL_UB_FIXED. SQL_UB_ON é a mesma constante como SQL_UB_FIXED. O Gerenciador de Driver passa SQL_UB_FIXED por meio do driver. SQL_UB_FIXED foi preterido no ODBC 3 *. x*, mas um ODBC 3 *. x* driver deve implementar para funcionar com o ODBC 2. *x* aplicativos que usam indicadores de comprimento fixo.  
  
 Para um ODBC 3 *. x* driver, o Gerenciador de Driver não verifica se *opção* está entre SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX ou é maior que SQL_CONNECT_OPT_DRVR_START.
