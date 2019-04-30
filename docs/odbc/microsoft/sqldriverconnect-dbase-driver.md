---
title: SQLDriverConnect (dBASE Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e4eeaa7ba710814bfeb8c5b4f5aa0dbd2d30ef7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63060949"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE Driver)
> [!NOTE]  
>  Este tópico fornece informações específicas do Driver do dBASE. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** permite que você se conecte a um driver sem criar uma fonte de dados (DSN).  
  
 As seguintes palavras-chave têm suporte na cadeia de conexão para todos os drivers: **DSN**, **DBQ**, e **FIL**.  
  
 Quando o driver do Paradox é usado, depois um arquivo protegido por senha tiver sido aberto por um usuário, outros usuários não são permitidos para abrir o mesmo arquivo.  
  
 A tabela a seguir mostra as palavras-chave mínimas necessárias para conectar a cada driver e fornece um exemplo de pares de palavra-chave/valor usada com **SQLDriverConnect**. Para obter uma lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).  
  
> [!NOTE]  
>  Se DBQ ou DefaultDir não for especificado para o dBASEdriver, o driver se conectar ao diretório atual.  
  
|Driver|Palavras-chave necessárias|Exemplos|  
|------------|-----------------------|--------------|  
|dBASE|Driver, DriverID|Driver={Microsoft dBASE Driver (*.dbf)}; DBQ=c:\temp; DriverID=277|
