---
title: Dados Long e SQLSetPos e SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 578c85331a65c15cb25b5d9b75b7156ab509e910
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036413"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Dados Long e SQLSetPos e SQLBulkOperations
Como é o caso com parâmetros em instruções SQL, os dados longos podem ser enviados quando atualizar as linhas com **SQLBulkOperations** ou **SQLSetPos** ou ao inserir linhas com **SQLBulkOperations**. Os dados são enviados em partes, com várias chamadas para **SQLPutData**. Colunas para o qual os dados são enviados em tempo de execução são conhecidas como *colunas de dados em execução*.  
  
> [!NOTE]  
>  Um aplicativo, na verdade, pode enviar qualquer tipo de dados em tempo de execução com **SQLPutData**, embora somente os caracteres e dados binários podem ser enviados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, há geralmente não há motivo para usar **SQLPutData**. É muito mais fácil associar o buffer e permitir que o driver recupera os dados do buffer.  
  
 Porque as colunas de dados long normalmente não são associadas, o aplicativo deve associar a coluna antes de chamar **SQLBulkOperations** ou **SQLSetPos** e, desvincule-a depois de chamar **SQLBulkOperations**  ou **SQLSetPos**. A coluna deve ser associada porque **SQLBulkOperations** ou **SQLSetPos** funciona apenas em colunas associadas e deve ser desassociado, de modo que **SQLGetData** pode ser usado para recuperar dados de uma coluna.  
  
 Para enviar dados em tempo de execução, o aplicativo faz o seguinte:  
  
1.  Coloca um valor de 32 bits no buffer de conjunto de linhas em vez de um valor de dados. Esse valor será retornado para o aplicativo mais tarde, para que o aplicativo deverá defini-lo em um valor significativo, como o número da coluna ou o identificador de um arquivo que contém dados.  
  
2.  Define o valor no buffer de comprimento/indicador para o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro. Esse valor indica para o driver que serão enviados com os dados para o parâmetro **SQLPutData**. O *comprimento* valor é usado ao enviar dados longos para uma fonte de dados que precisa saber quantos bytes de dados long serão enviados para que ele pode alocar antecipadamente espaço. Para determinar se uma fonte de dados solicita este valor, o aplicativo chama **SQLGetInfo** com a opção SQL_NEED_LONG_DATA_LEN. Todos os drivers devem dar suporte a esta macro; Se a fonte de dados não requer o comprimento em bytes, o driver pode ignorá-lo.  
  
3.  Chamadas **SQLBulkOperations** ou **SQLSetPos**. O driver detecta que um buffer de comprimento/indicador contém o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro e retorna SQL_NEED_DATA como o valor de retorno da função.  
  
4.  Chamadas **SQLParamData** em resposta ao SQL_NEED_DATA o valor de retorno. Se precisam ser enviada, dados longos **SQLParamData** retornará SQL_NEED_DATA. No buffer apontado pela *ValuePtrPtr* argumento, o driver retorna o valor exclusivo que o aplicativo é colocado no buffer de conjunto de linhas. Se houver mais de uma coluna de dados em execução, o aplicativo usa esse valor para determinar qual coluna para enviar dados para; o driver não é necessário para solicitar dados para colunas de dados em execução em uma ordem específica.  
  
5.  Chamadas **SQLPutData** para enviar os dados da coluna para o driver. Se os dados da coluna não couberem em um único buffer, pois geralmente é o caso de dados longo, o aplicativo chama **SQLPutData** repetidamente para enviar os dados em partes; cabe a fonte de dados e o driver para remontar os dados. Se o aplicativo passa os dados de cadeia de caracteres terminada em nulo, a driver ou fonte de dados deve remover o caractere de terminação null como parte do processo de remontagem.  
  
6.  Chamadas **SQLParamData** novamente para indicar que ele enviou todos os dados da coluna. Se houver qualquer coluna de dados em execução para o qual os dados não foram enviados, o driver retorna SQL_NEED_DATA e o valor exclusivo para a próxima coluna de dados em execução; o aplicativo retorna para a etapa 5. Se dados foram enviados para todas as colunas de dados em execução, os dados para a linha serão enviados à fonte de dados. **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO e pode retornar qualquer SQLSTATE **SQLBulkOperations** ou **SQLSetPos** pode retornar.  
  
 Após **SQLBulkOperations** ou **SQLSetPos** retornará SQL_NEED_DATA e antes de dados seja completamente enviados para a última coluna de dados em execução, a instrução está em um estado de dados necessário. Nesse estado, o aplicativo pode chamar apenas **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, ou **SQLGetDiagRec**; todas as outras funções retornam SQLSTATE HY010 (erro de sequência de função). Chamando **SQLCancel** cancela a execução da instrução e o retorna ao estado anterior. Para obter mais informações, consulte [apêndice b: Tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
