---
title: Dados de coluna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4bc57a5a0b500dc8828d5b0e35c2d6023165ac5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019255"
---
# <a name="column-data"></a>Dados de coluna
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores cria um buffer em cache para cada buffer de dados associado ao conjunto de resultados com **SQLBindCol**. Ele usa os valores nesses buffers para construir uma **onde** cláusula quando ela emula um posicionadas instrução update ou delete. Ele atualiza esses buffers dos buffers de conjunto de linhas quando ele busca dados da fonte de dados e quando ele executa instruções update posicionadas.  
  
 Quando a biblioteca de cursores atualiza seu cache dos buffers de conjunto de linhas, ele transfere os dados de acordo com o tipo de dados C especificado na **SQLBindCol**. Por exemplo, se o tipo de dados C de um buffer de conjunto de linhas for SQL_C_SLONG, a biblioteca de cursores transferências de quatro bytes de dados; Se for SQL_C_CHAR e *BufferLength* for 10, a biblioteca de cursores transfere 10 bytes de dados. A biblioteca de cursores não executa nenhuma verificação de tipo ou conversões de nos dados que ele transfere.  
  
> [!NOTE]  
>  A biblioteca de cursores não atualiza seu cache para uma coluna se **StrLen_or_IndPtr* no conjunto de linhas correspondente buffer é o resultado da macro SQL_LEN_DATA_AT_EXEC ou SQL_DATA_AT_EXEC.  
  
 Quando ele atualiza uma coluna, dados de caracteres de comprimento fixo de painéis de espaço em branco de origem de dados e dados binários de comprimento fixo de zero pads conforme necessário. Por exemplo, uma fonte de dados armazena "Smith" em uma coluna CHAR(10) como "Smith". A biblioteca de cursores não dados não o painel de espaço em branco ou o painel de zero nos buffers de conjunto de linhas quando ele copia esses dados para seu cache depois de executar uma instrução de atualização posicionada. Portanto, se um aplicativo exigir que os valores no cache da biblioteca de cursor são preenchidos de espaço em branco ou sem preenchimento, ele deve ser painel de espaço em branco ou preencheriam de zeros os valores nos buffers de conjunto de linhas antes de executar uma instrução update posicionadas.
