---
title: Drivers de banco de dados de diagnóstico para a área de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4e7c8ea96708886f9edf54047bd2a2104ba0ec8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031225"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnóstico para drivers de banco de dados de área de trabalho
Todos os erros e avisos não verificados ou parcialmente verificado pelo Gerenciador de Driver são tratados pelo driver. O driver também mapeia nativo erros ou erros retornados pela fonte de dados, para SQLSTATEs. Cada função listada na *referência do programador de ODBC* contém uma seção de "Diagnóstico" que especifica as condições e mensagens.  
  
 Aplicativos chamam **SQLGetDiagRec** para recuperar o SQLSTATE, código de erro nativo e mensagens de diagnóstico. Chamando **SQLGetDiagField** e especificando o campo recupera os campos de diagnóstico individuais. O nível de suporte dos identificadores de diagnóstico é listado na tabela a seguir.  
  
|DiagIdentifiers|Nível de suporte|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Sem suporte|  
|SQL_DIAG_CLASS_ORIGIN|Com suporte. Sempre "ODBC 3.0" para versões 3.0 e posterior do driver em questão.|  
|SQL_DIAG_COLUMN_NUMBER|Tem suporte|  
|SQL_DIAG_CURSOR_ROW_COUNT|Sem suporte|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Sem suporte|  
|SQL_DIAG_MESSAGE_TEXT|Tem suporte|  
|SQL_DIAG_NATIVE|Tem suporte|  
|SQL_DIAG_NUMBER|Tem suporte|  
|SQL_DIAG_RETURNCODE|Com suporte, mas implementado pelo Gerenciador de Driver|  
|SQL_DIAG_ROW_COUNT|Tem suporte|  
|SQL_DIAG_ROW_NUMBER|Tem suporte|  
|SQL_DIAG_SERVER_NAME|Sem suporte|  
|SQL_DIAG_SQLSTATE|Tem suporte|  
|SQL_DIAG_SUBCLASS_ORIGIN|Tem suporte|
