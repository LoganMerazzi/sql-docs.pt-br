---
title: Método getSubString (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getSubString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bf915590-a883-4403-befa-5b5bb42f34d8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3404d7e31cdc5ed82a4a2c57af1a05354104d4bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66787449"
---
# <a name="getsubstring-method-sqlserverclob"></a>Método getSubString (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna uma cópia da subcadeia de caracteres especificada no CLOB com base na posição inicial fornecida e no número de caracteres a serem copiados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getSubString(long pos,  
                                     int length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 O primeiro caractere da subcadeia a ser extraído. O primeiro caractere está na posição 1.  
  
 *length*  
  
 O número de caracteres consecutivos a serem copiados.  
  
## <a name="return-value"></a>Valor retornado  
 Uma **cadeia de caracteres** que é a subcadeia de caracteres especificada no CLOB.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getSubString é especificado pelo método getSubString na interface do CLOB.  
  
 A tentativa de obter zero caracteres de um CLOB nulo ou de comprimento zero retorna uma cadeia de caracteres vazia. A tentativa de obter qualquer comprimento de caracteres em qualquer posição que não seja a posição 1 em um CLOB de comprimento zero fará com que uma exceção de posição seja lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
