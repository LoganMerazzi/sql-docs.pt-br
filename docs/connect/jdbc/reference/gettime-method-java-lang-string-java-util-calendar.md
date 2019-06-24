---
title: Método getTime (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d4c67c2-a3c8-4a26-a159-89c5d63fda0b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6b9d74778d3ff1fc62b5549fbea7e0f97bf1e477
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778878"
---
# <a name="gettime-method-javalangstring-javautilcalendar"></a>Método getTime (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto java.sql.Time na linguagem de programação Java, considerando o nome do parâmetro, usando o objeto Calendar fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Time getTime(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *cal*  
  
 Um objeto de calendário.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto de tempo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getTime é especificado pelo método getTime na interface java.sql.CallableStatement.  
  
 Consulte o gráfico intitulado "Conversões de método Getter" em [Noções básicas sobre conversões de tipo de dados](../../../connect/jdbc/understanding-data-type-conversions.md) para ver quais [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados podem ser recuperados com esse método.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getTime &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
