---
title: Tamanho do conjunto de linhas de cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bff145e7e3c6e429ca0877c81c5188b02e428809
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63207170"
---
# <a name="cursor-rowset-size"></a>Tamanho do conjunto de linhas de cursor
  Os cursores ODBC não se limitam a buscar uma linha de cada vez. Eles podem recuperar várias linhas em cada chamada para **SQLFetch** ou [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md). Quando você está trabalhando com um banco de dados cliente/servidor, como o Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é mais eficaz buscar várias linhas de uma vez. O número de linhas retornadas em uma busca é chamado o tamanho do conjunto de linhas e é especificado com SQL_ATTR_ROW_ARRAY_SIZE de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md).  
  
```  
SQLUINTEGER uwRowsize;  
SQLSetStmtAttr(m_hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)uwRowsetSize, SQL_IS_UINTEGER);  
```  
  
 Os cursores com um tamanho de conjunto de linhas maior que 1 são chamados de cursores em bloco.  
  
 Há duas opções para associar colunas do conjunto de resultados para cursores em bloco:  
  
-   A associação por coluna  
  
     Cada coluna é associada a uma matriz de variáveis. Cada matriz possui o mesmo número de elementos que o tamanho do conjunto de linhas.  
  
-   Associação por linha  
  
     Uma matriz baseada em estruturas que armazenam os dados e indicadores de todas as colunas em uma linha. A matriz tem o mesmo número de estruturas que o tamanho do conjunto de linhas.  
  
 Quando a ligação com reconhecimento de coluna ou linha é usada, cada chamada para **SQLFetch** ou **SQLFetchScroll** preenche as matrizes associadas com os dados do conjunto de linhas recuperado.  
  
 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) também pode ser usado para recuperar dados da coluna de um cursor em bloco. Porque **SQLGetData** funciona ao mesmo tempo, uma linha **SQLSetPos** deve ser chamado para definir uma linha específica no conjunto de linhas como a linha atual antes de chamar **SQLGetData**.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece uma otimização usando conjuntos de linhas para recuperar um conjunto rapidamente de resultados inteiro. Para usar essa otimização, defina os atributos de cursor com seus padrões (tamanho do conjunto de linhas de somente avanço, somente leitura, = 1) no momento **SQLExecDirect** ou **SQLExecute** é chamado. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client configura um conjunto de resultados padrão. Esse procedimento é mais eficaz do que o uso de cursores de servidor ao transferir resultados para o cliente sem fazer rolagem. Depois que a instrução tiver sido executada, aumente o tamanho do conjunto de linhas e use a associação de coluna ou de linha. Isso permite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] use um resultado padrão definido para enviar linhas de resultados ao cliente, enquanto o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client continua a receber linhas dos buffers de rede no cliente.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do cursor](cursor-properties.md)  
  
  
