---
title: Sequência de Escape da chamada de procedimento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa936eb9f8ef3328945d4ece63fb36432a5fd618
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100588"
---
# <a name="procedure-call-escape-sequence"></a>Sequência de escape da chamada de procedimento
ODBC usa sequências de escape para chamadas de procedimento. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
 **{** [? =]**chamar** *nome do procedimento*[ **(** [*parâmetro*] [, [*parâmetro*]]... **)** ] **}**  
  
 Na notação BNF, a sintaxe é:  
  
 *Escape de procedimento de ODBC* :: =  
  
 &#124;*Esc-ODBC-iniciador* [? =] chamar *procedimento terminador de esc ODBC*  
  
 *procedure* ::= *procedure-name* &#124; *procedure-name* (*procedure-parameter-list*)  
  
 *Identificador de procedimento* :: = *nome definido pelo usuário*  
  
 *nome do procedimento* :: = *identificador de procedimento*  
  
 &#124;*nome do proprietário*. *Identificador de procedimento*  
  
 &#124;*separador de catálogo do nome do catálogo* *identificador de procedimento*  
  
 &#124;*separador de catálogo do nome do catálogo* [*nome do proprietário*]. *Identificador de procedimento*  
  
 (A sintaxe a terceira é válida somente se a fonte de dados não der suporte a proprietários.)  
  
 *nome do proprietário* :: = *nome definido pelo usuário*  
  
 *nome do catálogo* :: = *nome definido pelo usuário*  
  
 *separador de catálogo* :: = {*definido pela implementação*}  
  
 (O separador de catálogo é retornado por **SQLGetInfo** com a opção de informações SQL_CATALOG_NAME_SEPARATOR.)  
  
 *lista de parâmetros de procedimento* :: = *parâmetro de procedimento*  
  
 &#124; *procedure-parameter*, *procedure-parameter-list*  
  
 *parâmetro de procedimento* :: = *parâmetro dinâmico* &#124; *literal* &#124; *cadeia de caracteres vazia*  
  
 *cadeia de caracteres vazia* :: =  
  
 *Iniciador do ODBC-esc* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 (Se um parâmetro de procedimento é uma cadeia de caracteres vazia, o procedimento usa o valor padrão para esse parâmetro.)  
  
 Para determinar se a fonte de dados oferece suporte aos procedimentos e o driver dá suporte a sintaxe de invocação de procedimento ODBC, um aplicativo pode chamar **SQLGetInfo** com o tipo de informação SQL_PROCEDURES.
