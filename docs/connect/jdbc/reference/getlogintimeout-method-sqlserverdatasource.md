---
title: Método getLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ec8d033bc6d9bc451eaa606a00881bd4e533aa97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66793167"
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>Método getLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o número de segundos que o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) em questão aguardará ao tentar fazer uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **int** que representa o número de segundos de espera.  
  
## <a name="remarks"></a>Remarks  
 Se o aplicativo não especificar um valor de tempo limite explicitamente, este método retornará um valor padrão de 15 segundos.  
  
 Esse método getLoginTimeout é especificado pelo método getLoginTimeout na interface javax.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
