---
title: Excluindo linhas por indicador com SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a34f96dd7f5c2f0e2ac4bbb3feae06ea4856a248
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076811"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Excluir linhas por indicador com SQLBulkOperations
Ao excluir uma linha por indicador, **SQLBulkOperations** faz com que a fonte de dados exclua uma ou mais linhas selecionadas da tabela. As linhas são identificadas pelo indicador em uma coluna de indicador associado.  
  
 Para excluir linhas por indicador com **SQLBulkOperations**, o aplicativo faz o seguinte:  
  
1.  Recupera e armazena em cache os indicadores de todas as linhas a serem excluídos. Se houver mais de um indicador e a associação é usada, os indicadores são armazenados em uma matriz; Se houver mais de um indicador e a associação por linha é usada, os indicadores são armazenados em uma matriz de estruturas de linha.  
  
2.  Define o atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de indicadores e associa o buffer que contém o valor de indicador ou a matriz de indicadores, a coluna 0.  
  
3.  Chamadas **SQLBulkOperations** com *operação* definido como SQL_DELETE_BY_BOOKMARK.
