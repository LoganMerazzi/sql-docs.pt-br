---
title: Método getXopenStates (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de6fdf6b-8345-4490-b35e-7115b61e782e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c0a3859c3195d14243ff570493d3ae04c72d0780
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66768812"
---
# <a name="getxopenstates-method-sqlserverdatasource"></a>Método getXopenStates (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um valor **boolean** que indica se a conversão de estados SQL em estados compatíveis com XOPEN está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getXopenStates()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **True** se a conversão de estados SQL em estados compatíveis com XOPEN está habilitada. Caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade xopenStates for definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] converterá estados de SQL em estados em conformidade com o XOPEN. O padrão é **false**, que faz o driver JDBC gerar os códigos de estado SQL 99. Se xopenStates não for definido, o método getXopenStates retornará o valor padrão **false**.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
