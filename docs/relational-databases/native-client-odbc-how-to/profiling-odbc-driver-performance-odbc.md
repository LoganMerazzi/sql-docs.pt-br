---
title: Tópicos explicativos de desempenho de Driver do ODBC (ODBC) de criação de perfil | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0e6d7aed-28d2-419e-be6a-f60d3729bfd0
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: af0d53b7eac7302dcf492eb72cf7f731434790d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069636"
---
# <a name="profiling-odbc-driver-performance-odbc"></a>Criar perfil de desempenho do driver ODBC (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem duas opções específicas do driver para a criação de perfil de desempenho do driver.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC pode registrar estatísticas de desempenho no arquivo. O arquivo de log é um arquivo delimitado por tabulação que pode ser analisado em qualquer planilha com suporte para arquivos delimitados por tabulação, como o Microsoft Excel.  
  
 O driver também pode registrar consultas de longa execução (consultas que não obtêm uma resposta do servidor em um intervalo especificado de tempo). Essas consultas podem ser analisadas depois pelos programadores e pelos administradores de banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criar o perfil de dados de desempenho de Driver &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data.md)  
  
-   [Registrar consultas de longa execução &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-data-log-long-running-queries.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de instruções sobre ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
  
