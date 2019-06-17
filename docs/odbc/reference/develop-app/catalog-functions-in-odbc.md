---
title: Funções de catálogo em ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84c870d45cc487fc9ec5497e43b764bd4187d2f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63217621"
---
# <a name="catalog-functions-in-odbc"></a>Funções de catálogo em ODBC
ODBC contém as seguintes funções de catálogo:  
  
|Função|Descrição|  
|--------------|-----------------|  
|**SQLTables**|Retorna uma lista de catálogos, esquemas, tabelas ou tipos de tabela na fonte de dados.|  
|**SQLColumns**|Retorna uma lista de colunas em uma ou mais tabelas.|  
|**SQLStatistics**|Retorna uma lista de estatísticas sobre uma única tabela. Também retorna uma lista de índices associados à tabela.|  
|**SQLSpecialColumns**|Retorna uma lista de colunas que identifica exclusivamente uma linha em uma única tabela. Também retorna uma lista de colunas na tabela que são atualizadas automaticamente.|  
|**SQLPrimaryKeys**|Retorna uma lista de colunas que compõem a chave primária de uma única tabela.|  
|**SQLForeignKeys**|Retorna uma lista de chaves estrangeiras em uma única tabela ou uma lista de chaves estrangeiras em outras tabelas que fazem referência a uma única tabela.|  
|**SQLTablePrivileges**|Retorna uma lista de privilégios associados a uma ou mais tabelas.|  
|**SQLColumnPrivileges**|Retorna uma lista de privilégios associados a uma ou mais colunas em uma única tabela.|  
|**SQLProcedures**|Retorna uma lista de procedimentos na fonte de dados.|  
|**SQLProcedureColumns**|Retorna uma lista de parâmetros de entrada e saída, o valor de retorno e as colunas no conjunto de resultados de um único procedimento.|  
|**SQLGetTypeInfo**|Retorna uma lista dos tipos de dados SQL com suporte pela fonte de dados. Esses tipos de dados são geralmente usados em **CREATE TABLE** e **ALTER TABLE** instruções.|  
  
 Porque **SQLTables**, **SQLColumns**, **SQLStatistics**, e **SQLSpecialColumns** estão em conformidade com a CLI de grupo aberto e o **SQLGetTypeInfo** está de acordo com o ISO CLI 92, eles são implementados pela maioria dos drivers. As funções de catálogo restantes estão em nível de conformidade com ODBC.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Exibições do esquema](../../../odbc/reference/develop-app/schema-views.md)
