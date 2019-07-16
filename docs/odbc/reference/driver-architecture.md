---
title: Arquitetura de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd9bbb74d77a0b56b6b1f1aa5d8f1a6b5e97f5aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915472"
---
# <a name="driver-architecture"></a>Arquitetura do driver
Arquitetura do driver se enquadra em duas categorias, dependendo de quais instruções SQL de processos de software:  
  
-   **Drivers baseados em arquivo** o driver acessa os dados físicos diretamente. Nesse caso, o driver atua como o driver e a fonte de dados; ou seja, ele processa chamadas ODBC e instruções SQL. Por exemplo, drivers do dBASE são drivers baseados em arquivo, pois dBASE não fornece que um mecanismo de banco de dados autônomo, o driver pode usar. É importante observar que os desenvolvedores de drivers baseados em arquivo devem escrever seus próprios mecanismos de banco de dados.  
  
-   **Drivers baseados em DBMS** o driver acessa os dados físicos por meio de um mecanismo de banco de dados separado. Nesse caso, o driver processa somente as chamadas ODBC; ele passa instruções SQL para o mecanismo de banco de dados para processamento. Por exemplo, drivers do Oracle são drivers baseados em DBMS porque Oracle tem um mecanismo de banco de dados autônomo que usa o driver. Em que reside o mecanismo de banco de dados é irrelevante. Ele pode residir no mesmo computador que o driver ou um computador diferente na rede; ele ainda pode ser acessado por meio de um gateway.  
  
 Arquitetura do driver é geralmente interessante apenas para gravadores de driver; ou seja, a arquitetura do driver geralmente não faz diferença para o aplicativo. No entanto, a arquitetura pode afetar se um aplicativo pode usar o SQL específicas do DBMS. Por exemplo, o Microsoft Access fornece um mecanismo de banco de dados autônomo. Se um driver do Microsoft Access for baseados em DBMS, acessa os dados por meio desse mecanismo – o aplicativo pode passar instruções de SQL do Microsoft Access para o mecanismo para processamento.  
  
 No entanto, se o driver for baseado em arquivo, ou seja, ele contém um mecanismo de proprietário que acessa o arquivo. mdb do Microsoft® Access diretamente - qualquer tentativa de passar instruções SQL específicas da Microsoft Access para o mecanismo é provavelmente resultará em erros de sintaxe. O motivo é que o mecanismo de proprietário é provavelmente, implementarão somente ODBC SQL.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Drivers baseados em arquivo](../../odbc/reference/file-based-drivers.md)  
  
-   [Drivers baseados em DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Exemplo de rede](../../odbc/reference/network-example.md)  
  
-   [Outras arquiteturas do driver](../../odbc/reference/other-driver-architectures.md)
