---
title: Método getUDTs (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getUDTs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4396453-dcb0-4132-8325-06b3c7896b3b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0e90f4d2ea8b98d2ecef237f04f5fe290a512c92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66765900"
---
# <a name="getudts-method-sqlserverdatabasemetadata"></a>Método getUDTs (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição de tipos definidos pelo usuário em um esquema específico.  
  
> [!NOTE]  
>  Esse método não é compatível no momento com [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Quando usado, este método sempre retornará um conjunto de resultados vazio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.ResultSet getUDTs(java.lang.String catalog,  
                                  java.lang.String schemaPattern,  
                                  java.lang.String typeNamePattern,  
                                  int[] types)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *catalog*  
  
 Uma **String** que contém o nome do catálogo.  
  
 *schemaPattern*  
  
 Uma **String** que contém o padrão de nome do esquema.  
  
 *typeNamePattern*  
  
 Uma **String** que contém o padrão de nome de tipo.  
  
 *types*  
  
 Uma matriz de inteiros que contém os tipos de dados a serem incluídos. Nulo indica que todos os tipos devem ser incluídos.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getUDTs é especificado pelo método getUDTs na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
