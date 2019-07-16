---
title: 'SQL para C: Binário | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e280afb03eeac46a58943d276137e2019340a0a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057001"
---
# <a name="sql-to-c-binary"></a>SQL para C: Binary
Os identificadores para os tipos de dados SQL ODBC binários são:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 A tabela a seguir mostra os tipos de dados para o qual os dados binários do SQL podem ser convertidos de ODBC C. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Comprimento em bytes de dados) \* 2 < *BufferLength*<br /><br /> (Comprimento em bytes de dados) \* 2 > = *BufferLength*|Data<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|(Caractere de comprimento de dados) \* 2 < *BufferLength*<br /><br /> (Caractere de comprimento de dados) \* 2 > = *BufferLength*|Data<br /><br /> Dados truncados|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres|n/d<br /><br /> 01004|  
|SQL_C_BINARY|Comprimento de bytes de dados < = *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Data<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
  
 Quando dados binários do SQL são convertidos em dados de caractere C, cada byte (8 bits) de fonte de dados é representado como dois caracteres ASCII. Esses caracteres são a representação de caractere ASCII do número em formato hexadecimal. Por exemplo, um 00000001 binário é convertido em "01" e um binário 11111111 é convertido em "FF".  
  
 O driver sempre converte bytes individuais em pares de dígitos hexadecimais e encerra a cadeia de caracteres com um byte nulo. Por isso, se *BufferLength* é o mesmo e é menor que o comprimento dos dados convertidos, o último byte do **TargetValuePtr* buffer não é usado. (Os dados convertidos requerem um número par de bytes, o próximo ao último byte é um byte nulo e o último byte não pode ser usado.)  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos são desaconselhável de associação de dados binárias do SQL em um tipo de dados do caractere C. Geralmente, essa conversão é ineficiente e lento.
