---
title: Atualizando dados com SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1c31ef622281b4f52f62ca3867c5afa7dcae8ca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63194416"
---
# <a name="updating-data-with-sqlsetpos"></a>Atualizar dados com SQLSetPos
Aplicativos podem atualizar ou excluir qualquer linha no conjunto de linhas com **SQLSetPos**. Chamando **SQLSetPos** é uma alternativa conveniente para construir e executar uma instrução SQL. Ele permite que um driver ODBC dão suporte a atualizações posicionadas até mesmo quando a fonte de dados não dá suporte a instruções de SQL posicionadas. Ele faz parte do paradigma de conseguir acesso completo de banco de dados por meio de chamadas de função.  
  
 **SQLSetPos** opera no conjunto de linhas atual e pode ser usado somente após uma chamada para **SQLFetchScroll**. O aplicativo especifica o número da linha para atualizar, excluir ou inserir, e o driver recupera os novos dados para aquela linha dos buffers de conjunto de linhas. **SQLSetPos** também pode ser usado para designar uma linha especificada como a linha atual, ou atualizar uma linha específica no conjunto de linhas da fonte de dados.  
  
 Tamanho do conjunto de linhas é definido por uma chamada para **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** usa um novo tamanho do conjunto de linhas, no entanto, apenas após uma chamada para **SQLFetch** ou **SQLFetchScroll**. Por exemplo, se o tamanho do conjunto de linhas é alterado, **SQLSetPos** é chamado e então **SQLFetch** ou **SQLFetchScroll** é chamado e a chamada para **SQLSetPos** usa o tamanho do conjunto de linhas anterior ao **SQLFetch** ou **SQLFetchScroll** usa o novo tamanho do conjunto de linhas.  
  
 A primeira linha do conjunto de linhas é o número de linha 1. O *RowNumber* argumento **SQLSetPos** deve identificar uma linha no conjunto de linhas; ou seja, seu valor deve estar no intervalo entre 1 e o número de linhas buscado mais recentemente (que pode ser menor do que o tamanho do conjunto de linhas). Se *RowNumber* for 0, a operação se aplica a todas as linhas no conjunto de linhas.  
  
 Como a maioria dos interação com bancos de dados relacionais é feita por meio do SQL, **SQLSetPos** não tem amplo suporte. No entanto, um driver pode facilmente emulá-la, construir e executar uma **atualização** ou **excluir** instrução.  
  
 Para determinar quais operações **SQLSetPos** dá suporte, um aplicativo chama **SQLGetInfo** com o SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ Dos atributos1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 a opção de informações (dependendo do tipo de cursor).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Atualizando linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Excluindo linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
