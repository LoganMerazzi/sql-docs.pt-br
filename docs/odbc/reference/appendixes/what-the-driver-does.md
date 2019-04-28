---
title: O que faz o Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 685f67c9f24593a5c50097de426b76fef068d6e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735012"
---
# <a name="what-the-driver-does"></a>O que o driver faz
A tabela a seguir resume quais funções e um ODBC 3 de atributos de instrução *. x* driver deve implementar para cursores roláveis e bloco.  
  
|Função ou<br /><br /> atributo de instrução|Comentários|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Define o endereço da matriz de status de linha é preenchido por **SQLFetch** e **SQLFetchScroll**. Essa matriz também é preenchido por **SQLSetPos** se **SQLSetPos** é chamado no estado de instrução S6. Se **SQLSetPos** é chamado no estado S7, essa matriz não está preenchido, mas a matriz apontada pela *RowStatusArray* argumento da **SQLExtendedFetch** é preenchido. Para obter mais informações, consulte [transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md) no Apêndice b: Tabelas de transição de estado do ODBC.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Define o endereço do buffer no qual **SQLFetch** e **SQLFetchScroll** retornar o número de linhas buscadas. Se **SQLExtendedFetch** é chamado, esse buffer não está preenchido, mas o *RowCountPtr* argumento aponta para o número de linhas buscadas.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Define o tamanho do conjunto de linhas usado pelo **SQLFetch** e **SQLFetchScroll**.|  
|SQL_ROWSET_SIZE|Define o tamanho do conjunto de linhas usado pelo **SQLExtendedFetch**. 3 de ODBC *. x* drivers implementam isso, se eles desejam trabalhar com ODBC 2. *x* aplicativos que chamam **SQLExtendedFetch** ou **SQLSetPos**.|  
|**SQLBulkOperations**|Se um ODBC 3 *. x* driver deve funcionar com o ODBC 2. *x* aplicativos que usam **SQLSetPos** com um *operação* de SQL_ADD, o driver deve oferecer suporte **SQLSetPos** com um  *Operação* de SQL_ADD além **SQLBulkOperations** com um *operação* de SQL_ADD.|  
|**SQLExtendedFetch**|Retorna o conjunto de linhas especificado. 3 de ODBC *. x* drivers implementam isso, se eles desejam trabalhar com ODBC 2. *x* aplicativos que chamam **SQLExtendedFetch** ou **SQLSetPos**. A seguir estão os detalhes de implementação:<br /><br /> -O driver recupera o tamanho do conjunto de linhas do valor do atributo de instrução SQL_ROWSET_SIZE.<br />-O driver recupera o endereço da matriz de status de linha do *RowStatusArray* argumento, não o atributo da instrução SQL_ATTR_ROW_STATUS_PTR. O *RowStatusArray* argumento em uma chamada para **SQLExtendedFetch** não deve ser um ponteiro nulo. (Observe que, no ODBC 3 *. x*, o atributo da instrução SQL_ATTR_ROW_STATUS_PTR pode ser um ponteiro nulo.)<br />-O driver recupera o endereço do buffer de linhas buscadas a *RowCountPtr* argumento, não o atributo da instrução SQL_ATTR_ROWS_FETCHED_PTR.<br />-O driver retornará SQLSTATE 01S01 (erro na linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLExtendedFetch**. Um ODBC 3 *. x* driver deve retornar SQLSTATE 01S01 (erro na linha) somente quando **SQLExtendedFetch** é chamado, não quando **SQLFetch** ou **SQLFetchScroll** é chamado. Para preservar a compatibilidade com versões anteriores, quando SQLSTATE 01S01 (erro na linha) é retornado por **SQLExtendedFetch**, o Gerenciador de Driver não ordena os registros de status na fila de erros de acordo com as regras mencionadas no "sequência de Status Secção de "registros [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Retorna o próximo conjunto de linhas. A seguir estão os detalhes de implementação:<br /><br /> -O driver recupera o tamanho do conjunto de linhas do valor do atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE.<br />-O driver recupera o endereço da matriz de status de linha do atributo de instrução SQL_ATTR_ROW_STATUS_PTR.<br />-O driver recupera o endereço de linhas buscadas buffer do atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR.<br />-O aplicativo pode combinar chamadas entre **SQLFetchScroll** e **SQLFetch**.<br />-   **SQLFetch** retorna indicadores, se a coluna 0 está associada.<br />-   **SQLFetch** pode ser chamado para retornar mais de uma linha.<br />-O driver não retorna um SQLSTATE 01S01 (erro na linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLFetch**.|  
|**SQLFetchScroll**|Retorna o conjunto de linhas especificado. A seguir estão os detalhes de implementação:<br /><br /> -O driver recupera o tamanho do conjunto de linhas do atributo de instrução de SQL_ATTR_ROW_ARRAY_SIZE.<br />-O driver recupera o endereço da matriz de status de linha do atributo de instrução SQL_ATTR_ROW_STATUS_PTR.<br />-O driver recupera o endereço de linhas buscadas buffer do atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR.<br />-O aplicativo pode combinar chamadas entre **SQLFetchScroll** e **SQLFetch**.<br />-O driver não retorna um SQLSTATE 01S01 (erro na linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLFetchScroll**.|  
|**SQLSetPos**|Executa várias operações posicionadas. A seguir estão os detalhes de implementação:<br /><br /> -Isso pode ser chamado nos Estados de instrução S6 ou S7. Para obter mais detalhes, consulte [transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md) no Apêndice b: Tabelas de transição de estado do ODBC.<br />-Se que isso é chamado no estado de instrução S5 ou S6, o driver recupera o tamanho do conjunto de linhas do atributo SQL_ATTR_ROWS_FETCHED_PTR de instrução e o endereço da matriz de status de linha do atributo de instrução SQL_ATTR_ROW_STATUS_PTR.<br />-Se que isso é chamado no estado de instrução S7, o driver recupera o tamanho do conjunto de linhas do atributo da instrução SQL_ROWSET_SIZE e o endereço da matriz de status de linha do *RowStatusArray* argumento de  **SQLExtendedFetch**.<br />-O driver retornará SQLSTATE 01S01 (erro na linha) apenas para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLSetPos** para executar uma operação em massa quando a função é chamada no estado S7. Para preservar a compatibilidade com versões anteriores, se SQLSTATE 01S01 (erro na linha) é retornado por **SQLSetPos**, o Gerenciador de Driver não ordena os registros de status na fila de erros de acordo com as regras mencionadas no "sequência de registros de Status" seção de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />-Se o driver deve trabalhar com ODBC 2. *x* aplicativos que chamam **SQLSetPos** com um *operação* argumento de SQL_ADD, o driver deve oferecer suporte **SQLSetPos** com um  *Operação* argumento de SQL_ADD.|
