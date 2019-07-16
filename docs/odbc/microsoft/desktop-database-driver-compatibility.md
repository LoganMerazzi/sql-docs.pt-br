---
title: Compatibilidade de Driver de banco de dados da área de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31263162526b6bd2e0a116a473f09f9e2caeba94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077280"
---
# <a name="desktop-database-driver-compatibility"></a>Compatibilidade de driver de banco de dados de área de trabalho
O Unicode é um método de codificação de caracteres de software trata todos os caracteres como tendo uma largura fixa de dois bytes. Esse método é usado como uma alternativa para codificação de caracteres ANSI do Windows, que, porque ele representa os caracteres em um byte, é limitada a 256 caracteres. Porque o Unicode pode representar mais de 65.000 caracteres, que inclui muitos idiomas cujos caracteres não são representados na codificação ANSI.  
  
 O Gerenciador de Driver ODBC 3.5 (ou posterior) está habilitado para Unicode. Isso afeta duas áreas principais: chamadas de função e tipos de dados de cadeia de caracteres. Os argumentos de cadeia de caracteres de função do Gerenciador de Driver mapas e dados de cadeia de caracteres, conforme exigido pelo aplicativo e do driver, ambos os quais podem ser habilitado para Unicode ou ANSI habilitados.  
  
 O Gerenciador de Driver ODBC 3.5 (ou posterior) suporta o uso de um driver de Unicode com um aplicativo Unicode e um aplicativo ANSI. Ele também suporta o uso de um driver de ANSI com um aplicativo ANSI. O Gerenciador de Driver fornece o mapeamento de Unicode para ANSI limitado para um aplicativo Unicode trabalhando com um driver de ANSI. Isso permite o acesso a bancos de dados Jet 3.5 e suporte de todos os tipos de arquivo ISAM existentes.  
  
 Quando um aplicativo ANSI usa o Driver de banco de dados ODBC Desktop 4.0 e acessa o Microsoft Access 4.0 ou posterior, o driver expõe o tipo de dados como SQL_CHAR, SQL_VARCHAR ou SQL_LONGVARCHAR, embora o Jet 4.0 suporta a versão ampla. Não há suporte para versões mais antigas do Jet SQL_WCHAR, SQL_WVARCHAR e SQL_WLONGVARCHAR. Essa restrição também se aplica nos casos em que os antigos formatos são usados com o mecanismo de banco de dados do Jet 4.0.  
  
 Para obter mais informações sobre problemas de Unicode com ODBC, consulte [Unicode](../../odbc/reference/develop-app/unicode.md) em considerações de programação.
