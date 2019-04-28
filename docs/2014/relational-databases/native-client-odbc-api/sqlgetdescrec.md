---
title: SQLGetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41bd489752dc1b4084d9c012cad97413c6ff98b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657709"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
  Este tópico discute SQLGetDescRec funcionalidade específica para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec e parâmetros com valor de tabela  
 SQLGetDescRec pode ser usado para obter valores para atributos de parâmetros com valor de tabela e colunas de parâmetro com valor de tabela. O *RecNumber* parâmetro de SQLGetDescRec corresponde à *ParameterNumber* parâmetro do SQLBindParameter.  
  
 As colunas do parâmetro com valor de tabela ficam disponíveis somente quando o campo do cabeçalho do descritor SQL_SOPT_SS_PARAM_FOCUS é definido como o ordinal de um registro que tenha SQL_DESC_TYPE definido como SQL_SS_TABLE. Para obter mais informações sobre sql_spot_ss_param_focus sobre, consulte [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 SQLGetDescRec retorna os dados a seguir:  
  
|Parâmetro|Parâmetro com valor de tabela|Colunas de parâmetro com valor de tabela e outros parâmetros|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*Nome*|O nome de parâmetro formal para uma chamada de procedimento armazenado; caso contrário, uma cadeia de caracteres de comprimento 0.|O nome da coluna do parâmetro com valor de tabela.|  
|*TypePtr*|SQL_DESC_TYPE. Para parâmetros com valor de tabela, este é SQL_SS_TABLE.|SQL_DESC_TYPE|  
|*SubTypePtr*|Indefinido|SQL_DESC_DATETIME_INTERVAL_CODE (Para registros do tipo SQL_DATETIME ou SQL_INTERVAL.)|  
|*LengthPtr*|0|SQL_DESC_OCTET_LENGTH|  
|*PrecisionPtr*|0|SQL_DESC_PRECISION|  
|*ScalePtr*|0|SQL_DESC_SCALE|  
|*NullablePtr*|1|SQL_DESC_NULLABLE|  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>Suporte de SQLGetDescRec a recursos aprimorados de data e hora  
 Os valores retornados para tipos de data/hora são os seguintes:  
  
||*TypePtr*|*SubTypePtr*|*LengthPtr*|*PrecisionPtr*|*ScalePtr*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>Suporte de SQLGetDescRec para UDTs CLR grandes  
 `SQLGetDescRec` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQLGetDescRec](https://go.microsoft.com/fwlink/?LinkId=80707)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
