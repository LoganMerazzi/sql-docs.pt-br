---
title: Suporte de conjunto de caracteres nacionais | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f143d37911a1375a1eebe9de04c8b509817575ec
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="national-character-set-support"></a>Suporte ao conjunto de caracteres nacionais
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O driver JDBC oferece suporte à API do JDBC 4.0, que inclui novos métodos da API de conversão do conjunto de caracteres nacional. Esse suporte inclui novos métodos setter, getter e updater para **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, e **NCLOB** tipos JDBC.  
  
 A seguir encontra-se uma lista de novos métodos de getter, setter e updater para dar suporte à conversão do conjunto de caracteres nacionais:  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md).  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md), [setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md), [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md), [setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md).  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md), [getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md), [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md), [updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md), [updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md), [updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md).  
  
> [!NOTE]  
>  É preciso definir o classpath para incluir o arquivo sqljdbc4.jar a fim de usar esses métodos em um aplicativo.  
  
 Para enviar parâmetros String ao servidor no formato Unicode, os aplicativos devem usar os novos métodos de caractere nacional JDBC 4.0 ou defina o **sendStringParametersAsUnicode** propriedade de conexão como "**true**" ao usar os métodos de caractere não nacional. O modo recomendado é usar os novos métodos de caracteres nacionais do JDBC 4.0 onde possível. Para obter mais informações sobre o **sendStringParametersAsUnicode** propriedade de conexão, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  