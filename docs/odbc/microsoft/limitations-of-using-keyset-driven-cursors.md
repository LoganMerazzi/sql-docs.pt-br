---
title: Limitações do uso de cursores controlados por | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c35f900faf1a30788b3642af3fdd65d672951d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054124"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitações de uso de cursores controlados por conjunto de chaves
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Você deve ser capaz de recuperar uma única coluna ROWID para a tabela consultada. Um cursor controlado por conjunto de chaves não pode ser usado em junções, consultas ou instruções que contêm DISTINCT, GROUP BY, UNION, INTERSECT ou menos cláusulas.  
  
 Além disso, se seu aplicativo usa aliases de tabela, os cursores controlados por conjunto de chaves não funcionará; tipos de cursor somente de avanço ou estáticos são necessários. O conjunto de chaves usando o tipo de cursor com aliases de tabela fará com que o seguinte erro: "[Microsoft] [driver ODBC para Oracle] não é possível usar um cursor controlado por junção, com union, intersect ou conjunto de resultados de menos ou em somente leitura."  
  
> [!NOTE]  
>  Por causa da maneira que o driver lida com a instrução SQL que é enviada para o servidor Oracle, Oracle internamente retorna a seguinte mensagem de erro: "ORA-00964: tabela de nome não na lista."
