---
title: Rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], about tracing
- driver manager [ODBC], tracing
ms.assetid: 77ed4c6c-d976-4eb2-8526-a12697b0ef83
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a00861365df27357099176151bcd681e15e585e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985118"
---
# <a name="tracing"></a>Rastreamento
O Gerenciador de Driver ODBC tem um recurso de rastreamento que permite que a sequência de chamadas de função feitas por um aplicativo ODBC a ser gravado e transcrita em um arquivo de log. O rastreamento é executado por uma DLL de rastreamento que captura chamadas entre o aplicativo e o Gerenciador de Driver e entre o Gerenciador de Driver e o driver. Esse método de rastreamento substitui o rastreamento executado pelo ODBC 2 *. x* Gerenciador de Driver e o rastreamento realizadas em ODBC 2 *. x* pelo ODBC espião.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [DLL de rastreamento](../../../odbc/reference/develop-app/trace-dll.md)  
  
-   [Arquivo de rastreamento](../../../odbc/reference/develop-app/trace-file.md)  
  
-   [Habilitando o rastreamento](../../../odbc/reference/develop-app/enabling-tracing.md)  
  
-   [Rastreamento dinâmico](../../../odbc/reference/develop-app/dynamic-tracing.md)
