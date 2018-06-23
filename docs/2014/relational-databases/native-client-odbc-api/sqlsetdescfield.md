---
title: SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bf61530ccfd142b473da8a5443cc63b16a435d32
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007697"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
  SQLSetDescField pode ser usado para definir campos de descritor para parâmetros com valor de tabela e colunas de parâmetro com valor de tabela. Para obter informações sobre os campos disponíveis, consulte [campos de descritor de parâmetro com valor de tabela](../native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) e [campos de descritor para colunas de constituinte de parâmetro com valor de tabela](../native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md).  
  
## <a name="remarks"></a>Remarks  
 As colunas do parâmetro com valor de tabela ficam disponíveis somente quando o campo do cabeçalho do descritor SQL_SOPT_SS_PARAM_FOCUS é definido como o ordinal de um registro que tenha SQL_DESC_TYPE definido como SQL_SS_TABLE. Para obter mais informações sobre SQL_SOPT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Se for feita uma tentativa de definir SQL_SOPT_SS_PARAM_FOCUS como o ordinal de um parâmetro que não é um parâmetro com valor de tabela, SQLSetStmtAttr retornará SQL_ERROR e é criado um registro de diagnóstico com SQLSTATE = HY024 e a mensagem "valor de atributo inválido". SQL_SOPT_SS_PARAM_FOCUS não é alterado quando SQL_ERROR é retornado.  
  
 A definição de SQL_SOPT_SS_PARAM_FOCUS como 0 restaura o acesso a registros de descritor para parâmetros.  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>Suporte do SQLSetDescField a recursos aprimorados de data e hora  
 Os recursos de data/hora foram aprimorados no ODBC. Para obter informações sobre o campo de descritor fornecido para os tipos de data/hora novo, consulte [parâmetro e metadados de resultado](../native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obter mais informações, consulte [data e hora melhorias &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>Suporte de SQLSetDescField a UDTs grandes do CLR  
 SQLSetDescField oferece suporte a grandes CLR definido pelo usuário (UDTs tipos). Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>Suporte de SQLSetDescField a colunas esparsas  
 SQLSetDecField pode ser usado para definir SQL_SOPT_SS_NAME_SCOPE no descritor de parâmetro de aplicativo (APD) com os valores SQL_SS_NAME_SCOPE_EXTENDED e SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET.  
  
 Para obter mais informações, consulte [suporte a colunas esparsas &#40;ODBC&#41;](../native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQLSetDescField](http://go.microsoft.com/fwlink/?LinkId=80705)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  