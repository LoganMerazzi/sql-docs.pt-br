---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 64224480bad8a7ffc3334b4fbc7670c19e77cb56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115243"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLCloseCursor** substitui [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com um *opção* valor SQL_CLOSE. Após a recepção de **SQLCloseCursor**, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client descarta linhas de conjunto de resultados pendentes. Observe que as associações de parâmetro e coluna da instrução (se houver) são mantidas inalteradas por **SQLCloseCursor**.  
  
## <a name="see-also"></a>Consulte também  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
