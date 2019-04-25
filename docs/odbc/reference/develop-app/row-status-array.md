---
title: Matriz de Status de linha | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d2a04f5052a0b686d3669c976ec7c4bee09e52b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468623"
---
# <a name="row-status-array"></a>Matriz de status da linha
Além dos dados, **SQLFetch** e **SQLFetchScroll** pode retornar uma matriz que fornece o status de cada linha no conjunto de linhas. Essa matriz é especificado por meio do atributo de instrução SQL_ATTR_ROW_STATUS_PTR. Essa matriz é alocada pelo aplicativo e deve ter tantos elementos que sejam especificadas pelo atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE. Os valores na matriz são definidos pelo **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, e **SQLSetPos.** Os valores descrevem o status da linha e se o status foi alterado desde que foi buscada pela última vez.  
  
|Valor de matriz de status de linha|Descrição|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|A linha foi obtida com êxito e não foi alterado desde que foi buscada pela última vez.|  
|SQL_ROW_SUCCESS_WITH_INFO|A linha foi obtida com êxito e não foi alterado desde que foi buscada pela última vez. No entanto, um aviso sobre a linha foi retornado.|  
|SQL_ROW_ERROR|Ocorreu um erro ao buscar a linha.|  
|SQL_ROW_UPDATED|A linha foi obtida com êxito e foi atualizada desde que foi buscada pela última vez. Se a linha é novamente buscada ou atualizada por **SQLSetPos**, seu status é alterado para o novo status.<br /><br /> Alguns drivers não podem detectar alterações aos dados e, portanto, não é possível retornar esse valor. Para determinar se um driver pode detectar as atualizações para linhas refetched, um aplicativo chama **SQLGetInfo** com a opção SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|A linha foi excluída desde que foi buscada pela última vez.|  
|SQL_ROW_ADDED|A linha foi inserida pela **SQLBulkOperations**. Se a linha será buscada novamente ou é atualizada pelo **SQLSetPos**, seu status é SQL_ROW_SUCCESS.<br /><br /> Esse valor não é definido **SQLFetch** ou **SQLFetchScroll**.|  
|SQL_ROW_NOROW|O conjunto de linhas sobrepostas final do conjunto de resultados e nenhuma linha foi retornada que correspondeu a esse elemento da matriz de status de linha.|
