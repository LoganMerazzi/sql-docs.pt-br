---
title: Verificações de transição de estado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcfefffb167b97ace09bfa358296d886265a987f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149058"
---
# <a name="state-transition-checks"></a>Verificações de transição de estado
O Gerenciador de Driver verifica se o estado do ambiente, conexão ou instrução é apropriado para a função que está sendo chamada. Por exemplo, uma conexão deve estar em um alocado estado quando **SQLConnect** é chamado; uma instrução deve estar em um preparada estado quando **SQLExecute** é chamado. O Gerenciador de Driver retornará SQL_ERROR para erros de transição de estado.
