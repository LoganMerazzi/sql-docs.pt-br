---
title: Método getCharacterStream (long, long) (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5a8028bc-c877-4668-b662-0746d462040e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 96fbaf14a04203e08c620b5173bcc2df6d03cb7c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784944"
---
# <a name="getcharacterstream-method-long-long-sqlservernclob"></a>Método getCharacterStream (long, long) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera os dados de **NCLOB** como um objeto **Reader** ou como um fluxo de caracteres com uma posição e um comprimento especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                  long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 Um **long** que indica o deslocamento do primeiro caractere do valor parcial a ser recuperado.  
  
 *length*  
  
 Um **long** que indica o comprimento, em caracteres, do valor parcial a ser recuperado.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Reader que contém os dados **NCLOB**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getCharacterStream é especificado pelo método getCharacterStream na interface do NCLOB.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getCharacterStream &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)   
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
