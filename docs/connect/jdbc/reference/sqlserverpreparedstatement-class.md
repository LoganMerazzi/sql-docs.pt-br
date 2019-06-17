---
title: Classe SQLServerPreparedStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7112a20f7811a0796396045c50b1b243ed0c3802
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796946"
---
# <a name="sqlserverpreparedstatement-class"></a>Classe SQLServerPreparedStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa a implementação básica da funcionalidade de instrução preparada JDBC.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** SQLServerStatement  
  
 **Implementa:** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerPreparedStatement fornece métodos que permitem que você forneça parâmetros como qualquer tipo nativo do Java e vários tipos de objetos Java. SQLServerPreparedStatement prepara uma instrução usando o procedimento armazenado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sp_prepare** e, em seguida, reutiliza a barra de instrução retornada para cada execução subsequente da instrução, normalmente usando diferentes parâmetros fornecidos pelo usuário.  
  
 SQLServerPreparedStatement é compatível com o processamento em lotes, em que um conjunto de instruções preparadas é executado em uma viagem de ida e volta do banco de dados individual, para melhorar o desempenho do tempo de execução.  
  
 Esta classe dá suporte ao desencapsulamento para a classe SQLServerPreparedStatement, interface ISQLServerPreparedStatement, PreparedStatement interface, as classes e interfaces suportadas por SQLServerStatement para desencapsulamento. Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
