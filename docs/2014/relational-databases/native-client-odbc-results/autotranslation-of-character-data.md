---
title: Tradução automática de dados de caractere | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5182ab1a72caac4181e50df2199f3e0457d3aaac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200216"
---
# <a name="autotranslation-of-character-data"></a>Tradução automática de dados de caracteres
  Dados de caractere, como ANSI de caracteres variáveis declaradas com SQL_C_CHAR ou dados armazenados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o **char**, **varchar**, ou **texto** tipos de dados, pode representa apenas um número limitado de caracteres. Os dados de caractere armazenados que usam um byte por caractere podem representar apenas 256 caracteres. Os valores armazenados em variáveis SQL_C_CHAR são interpretados usando a ACP (página de código ANSI) do computador cliente. Os valores armazenados usando **char**, **varchar**, ou **texto** tipos de dados no servidor são avaliados usando a ACP do servidor.  
  
 Se o servidor e o cliente tiverem a mesma ACP, eles não terão problemas na interpretação dos valores armazenados em SQL_C_CHAR, **char**, **varchar**, ou **texto** objetos. Se o servidor e o cliente tiverem ACPs diferentes, os dados SQL_C_CHAR do cliente podem ser interpretados como um caractere diferente no servidor se ele é usado no **char**, **varchar**, ou **texto** colunas, variáveis ou parâmetros. Por exemplo, um byte do caractere que contém o valor 0xA5 é interpretado como o caractere?? em um computador usando o código de página 437 e é interpretado conforme a iene entrar (?) em um computador executando a página de código 1252.  
  
 Dados de Unicode são armazenados usando dois bytes por caractere. Todos os caracteres estendidos são abordados pela especificação de Unicode. Dessa forma, todos os caracteres Unicode são interpretados da mesma maneira por todos os computadores.  
  
 O recurso AutoTranslate do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client tenta minimizar os problemas na movimentação de dados de caractere entre um cliente e um servidor que têm diferentes páginas de código. AutoTranslate pode ser definido na cadeia de conexão do [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md), na cadeia de configuração do [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md), ou ao configurar fontes de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC driver usando o administrador ODBC.  
  
 Quando AutoTranslate está definido como "não", nenhuma conversão é feita nos dados movidos entre as variáveis SQL_C_CHAR no cliente e **char**, **varchar**, ou **texto** colunas, variáveis, ou parâmetros em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. Os padrões de bit poderão ser interpretados de forma diferente nos computadores cliente e servidor se os dados contiverem caracteres estendidos e os dois computadores tiverem páginas de código diferentes. Os dados serão interpretados da mesma maneira se ambos os computadores tiverem a mesma página de código.  
  
 Quando AutoTranslate está definido como "Sim", o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client usa Unicode para converter os dados movidos entre as variáveis SQL_C_CHAR no cliente e **char**, **varchar**, ou **texto** colunas, variáveis ou parâmetros em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados:  
  
-   Quando os dados são enviados de uma variável SQL_C_CHAR no cliente para um **char**, **varchar**, ou **texto** coluna, variável ou parâmetro em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados ODBC driver primeiro converte de SQL_C_CHAR em Unicode usando a ACP do cliente, em seguida, de Unicode novamente em caractere usando a ACP do servidor.  
  
-   Quando os dados são enviados de um **char**, **varchar**, ou **texto** coluna, variável ou parâmetro em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados a uma variável SQL_C_CHAR no cliente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Driver do Native Client ODBC primeiro converte de caractere em Unicode usando a ACP do servidor, em seguida, de Unicode novamente em SQL_C_CHAR usando a ACP do cliente.  
  
 Como todas essas conversões são feitas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client em execução no cliente, a ACP do servidor deve ser uma das páginas de código instaladas no computador cliente.  
  
 Fazer as conversões de caractere por Unicode assegura a conversão adequada de todos os caracteres que existem nas duas páginas de código. Se um caractere existir em uma página de código, mas não em outra, entretanto, o caractere não poderá ser representado na página de código de destino. Por exemplo, a página de código 1252 tem o símbolo de marca registrada (?), enquanto a página de código 437 não tem.  
  
 A configuração AutoTranslate não tem nenhum efeito sobre essas conversões:  
  
-   Mover dados entre variáveis de cliente do SQL_C_CHAR de caractere e Unicode **nchar**, **nvarchar**, ou **ntext** colunas, variáveis ou parâmetros no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados.  
  
-   Mover dados entre variáveis de cliente SQL_C_WCHAR de Unicode e o caractere **char**, **varchar**, ou **texto** colunas, variáveis ou parâmetros no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados.  
  
 Os dados devem sempre ser convertidos quando movidos de caractere para Unicode.  
  
## <a name="see-also"></a>Consulte também  
 [Processando resultados &#40;ODBC&#41;](processing-results-odbc.md)   
 [Suporte a ordenações e a Unicode](../collations/collation-and-unicode-support.md)  
  
  
