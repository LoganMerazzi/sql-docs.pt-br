---
title: Aprimoramentos de data e hora (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 65a083b1aac2661ac013bf005d1d442d73a86f99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030502"
---
# <a name="date-and-time-improvements-odbc"></a>Aprimoramentos de data e hora (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduziu novos tipos de dados de data e hora. Esta seção descreve como esses novos tipos são expostos como extensões no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para obter uma visão geral [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suporte ao cliente nativo para a nova data e tipos de dados de hora, consulte [aprimoramentos de data e hora](../../relational-databases/native-client/features/date-and-time-improvements.md). Para obter um exemplo que demonstra o suporte de data/hora ODBC, consulte [Use tipos de data e hora](../../relational-databases/native-client-odbc-how-to/use-date-and-time-types.md).  
  
 Para obter mais informações sobre tipos de dados de data e hora, consulte [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Suporte a tipos de dados para aprimoramentos de data e hora do ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 Fornece informações sobre tipos ODBC que oferecem suporte a tipos de dados de data e hora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Metadados &#40;ODBC&#41;](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
 Descreve informações retornadas no descritor de parâmetro de implementação (IPD) e campos de IRD (descritor) de linha de implementação, bem como metadados de coluna retornados por **SQLColumns** e **SQLProcedureColumns**. Também descreve metadados de tipo de dados retornados por **SQLGetTypeInfo**.  
  
 [Conversões de tipo de dados datetime &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-odbc.md)  
 Descreve como converter entre valores datetime e datetimeoffset.  
  
 [Suporte a Sql_variant para tipos de data e hora](../../relational-databases/native-client-odbc-date-time/sql-variant-support-for-date-and-time-types.md)  
 Descreve o suporte da função SQL_VARIANT para uma funcionalidade de data e hora aprimorada.  
  
 [Em massa copia alterações para tipos aprimorados de data e hora &#40;OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Descreve aprimoramentos de data/hora para dar suporte a operações de cópia em massa.  
  
 [Comportamento com versões anteriores do SQL Server um tipo aprimorados de data e hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 Descreve o comportamento esperado quando um aplicativo cliente usando recursos de data e hora aprimorados se comunica com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quando um cliente compilado com uma versão mais antiga do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envia comandos para um servidor que dê suporte os recursos de data e hora aprimorados.  
  
 [Suporte à API ODBC para recursos avançados de data e hora](../../relational-databases/native-client-odbc-date-time/odbc-api-support-for-enhanced-date-and-time-features.md)  
 Lista as ODBC funções que dão suporte a funcionalidade de data e hora aprimorada.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
