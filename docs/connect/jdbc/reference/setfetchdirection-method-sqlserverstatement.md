---
title: Método setFetchDirection (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a23f058eea5512181bdbea277c4bccc6d1ff2616
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803392"
---
# <a name="setfetchdirection-method-sqlserverstatement"></a>Método setFetchDirection (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fornece ao [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] uma dica sobre a direção em que as linhas do conjunto de resultados devem ser processadas.  
  
> [!NOTE]  
>  Atualmente, o driver JDBC ignora a dica fornecida por este método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nDir*  
  
 Um **int** que indica a direção de processamento da linha, que pode ser um dos seguintes valores:  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setFetchDirection é especificado pelo método setFetchDirection na interface Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
