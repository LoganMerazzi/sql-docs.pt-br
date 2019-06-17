---
title: Subchave do núcleo ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c95c4e28a5f32131307daeaa61e214af887b577
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63069691"
---
# <a name="odbc-core-subkey"></a>Subchave do núcleo ODBC
O valor sob a subchave do núcleo de ODBC fornece a contagem de uso para os componentes principais (Gerenciador de Driver, biblioteca de cursores, DLL do instalador e assim por diante). O formato desse valor é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*contagem*|  
  
 Por exemplo, suponha que os componentes de núcleo de ODBC foram instalados pelos programas de instalação para três aplicativos diferentes e dois drivers diferentes. O valor sob a subchave do núcleo de ODBC seria:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
