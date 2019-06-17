---
title: SQLGetInfo (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 015ea45d1383e6813973aeb1e4c86451a506a2aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213324"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível 1  
  
 Retorna informações gerais sobre o Driver ODBC do Visual FoxPro e associado com um identificador de conexão de fonte de dados *hdbc*. A lista a seguir mostra o valor retornado pelo Driver de ODBC do Visual FoxPro para cada *fInfoType* argumento e comentários sobre os valores retornados.  
  
 Para obter mais informações, consulte [SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md) na *referência do programador de ODBC*.  
  
## <a name="a"></a>Um  
 Retorna SQL_ACCESSIBLE_PROCEDURES ' n '.  
  
 SQL_ACCESSIBLE_TABLES retorna 'Y'.  
  
 SQL_ACTIVE_CONNECTIONS retornará 0.  
  
 SQL_ACTIVE_STATEMENTS retornará 0.  
  
 SQL_ALTER_TABLE retorna SQL_AT_ADD_COLUMN ou SQL_AT_DROP_COLUMN.  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE retorna SQL_BP_SCROLL.  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS retorna 'Y'.  
  
 SQL_CONCAT_NULL_BEHAVIOR retorna SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINT retornará 0. O Driver de ODBC do Visual FoxPro não suporta *BigInt*.  
  
 SQL_CONVERT_BINARY retornará 0.  
  
 SQL_CONVERT_BIT retornará 0.  
  
 SQL_CONVERT_CHAR retornará 0.  
  
 SQL_CONVERT_DATE retornará 0.  
  
 SQL_CONVERT_DECIMAL retornará 0.  
  
 SQL_CONVERT_DOUBLE retornará 0.  
  
 SQL_CONVERT_FLOAT retornará 0.  
  
 SQL_CONVERT_INTEGER retornará 0.  
  
 SQL_CONVERT_LONGVARBINARY retornará 0.  
  
 SQL_CONVERT_LONGVARCHAR retornará 0.  
  
 SQL_CONVERT_NUMERIC returns 0.  
  
 SQL_CONVERT_REAL retornará 0.  
  
 SQL_CONVERT_SMALLINT retornará 0.  
  
 SQL_CONVERT_TIME retornará 0.  
  
 SQL_CONVERT_TIMESTAMP retornará 0.  
  
 SQL_CONVERT_TINYINT retornará 0.  
  
 SQL_CONVERT_VARBINARY retornará 0.  
  
 SQL_CONVERT_VARCHAR retornará 0.  
  
 SQL_CONVERT_FUNCTIONS retornará 0.  
  
 SQL_CORRELATION_NAME retorna SQL_CN_ANY.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR retorna SQL_CB_PRESERVE.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR retorna SQL_CB_PRESERVE.  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME retorna o valor passado como DSN para [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md), ou [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md); retorna uma cadeia de caracteres vazia se nenhum DSN for especificado.  
  
 Retorna SQL_DATA_SOURCE_READ_ONLY ' n '.  
  
 SQL_DATABASE_NAME retorna um caminho UNC completo para o banco de dados atual se a fonte de dados for um [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md). Se a fonte de dados se conecta a um diretório da [tabelas](../../odbc/microsoft/visual-foxpro-terminology.md), a função retorna o caminho para o diretório.  
  
 SQL_DBMS_NAME retorna "Visual FoxPro".  
  
 SQL_DBMS_VER retorna "03.00.0000".  
  
 SQL_DEFAULT_TXN_ISOLATION returns SQL_TXN_READ_COMMITTED. Leituras sujas não são possíveis, mas leituras não repetíveis e fantasmas são possíveis.  
  
 SQL_DRIVER_HDBC é implementada pelo Gerenciador de Driver.  
  
 SQL_DRIVER_HENV é implementada pelo Gerenciador de Driver.  
  
 SQL_DRIVER_HLIB é implementada pelo Gerenciador de Driver.  
  
 SQL_DRIVER_HSTMT é implementada pelo Gerenciador de Driver.  
  
 SQL_DRIVER_NAME returns "vfpodbc.dll".  
  
 SQL_DRIVER_ODBC_VER retorna "02.50" (SQL_SPEC_MAJOR, SQL_SPEC_MINOR).  
  
 SQL_DRIVER_VER retorna "01.00.0000".  
  
## <a name="e"></a>E  
 Retorna SQL_EXPRESSIONS_IN_ORDERBY ' n '.  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION retorna:  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK.  
  
 SQL_FILE_USAGE retorna SQL_FILE_QUALIFIER ambas as para o banco de dados (arquivo. dbc) e fontes de dados (arquivo. dbf) de tabela gratuitamente.  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS returns:  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY retorna SQL_GB_NO_RELATION.  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE retorna SQL_IC_MIXED.  
  
 Retorna SQL_IDENTIFIER_QUOTE_CHAR '.  
  
## <a name="k"></a>K  
 SQL_KEYWORDS returns "".  
  
## <a name="l"></a>L  
 Retorna SQL_LIKE_ESCAPE_CLAUSE ' n '.  
  
 SQL_LOCK_TYPES retorna SQL_LCK_NO_CHANGE.  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN returns 0.  
  
 SQL_MAX_CHAR_LITERAL_LEN returns 254.  
  
 SQL_MAX_COLUMN_NAME_LEN retorna 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY returns 16.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY returns 16.  
  
 SQL_MAX_COLUMNS_IN_INDEX returns 0.  
  
 SQL_MAX_COLUMNS_IN_SELECT returns 254.  
  
 SQL_MAX_COLUMNS_IN_TABLE returns 254.  
  
 SQL_MAX_CURSOR_NAME_LEN returns 254.  
  
 SQL_MAX_INDEX_SIZE returns 0.  
  
 SQL_MAX_OWNER_NAME_LEN returns 0.  
  
 SQL_MAX_PROCEDURE_NAME_LEN retornará 0. O Driver de ODBC do Visual FoxPro não permite acesso direto aos procedimentos do Visual FoxPro armazenados.  
  
 SQL_MAX_QUALIFIER_NAME_LEN retorna o comprimento do caminho máximo do sistema operacional.  
  
 SQL_MAX_ROW_SIZE returns 254^2.  
  
 Retorna SQL_MAX_ROW_SIZE_INCLUDES_LONG ' n '.  
  
 SQL_MAX_STATEMENT_LEN returns 8192.  
  
 SQL_MAX_TABLE_NAME_LEN retorna 128.  
  
 SQL_MAX_TABLES_IN_SELECT returns 16.  
  
 SQL_MAX_USER_NAME_LEN returns 0.  
  
 SQL_MULT_RESULT_SETS retorna 'Y'.  
  
 SQL_MULTIPLE_ACTIVE_TXN retorna 'Y'. Várias conexões podem ter várias transações abertas ao mesmo tempo.  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN returns 'N'.  
  
 SQL_NON_NULLABLE_COLUMNS retorna SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION retorna SQL_NC_LOW.  
  
 SQL_NUMERIC_FUNCTIONS retorna todas as funções exceto SQL_FN_NUM_POWER, que não é compatível com o Driver de ODBC do Visual FoxPro. Há suporte para as funções a seguir:  
  
-   SQL_FN_NUM_ABS  
  
-   SQL_FN_NUM_ACOS  
  
-   SQL_FN_NUM_ASIN  
  
-   SQL_FN_NUM_ATAN  
  
-   SQL_FN_NUM_ATAN2  
  
-   SQL_FN_NUM_CELING  
  
-   SQL_FN_NUM_COS  
  
-   SQL_FN_NUM_COT  
  
-   SQL_FN_NUM_DEGREES  
  
-   SQL_FN_NUM_EXP  
  
-   SQL_FN_NUM_FLOOR  
  
-   SQL_FN_NUM_LOG  
  
-   SQL_FN_NUM_LOG10  
  
-   SQL_FN_NUM_MOD  
  
-   SQL_FN_NUM_PI  
  
-   SQL_FN_NUM_RADIANS  
  
-   SQL_FN_NUM_RAND  
  
-   SQL_FN_NUM_ROUND  
  
-   SQL_FN_NUM_SIGN  
  
-   SQL_FN_NUM_SIN  
  
-   SQL_FN_NUM_SQRT  
  
-   SQL_FN_NUM_TAN  
  
## <a name="o"></a>O  
 SQL_ODBC_API_CONFORMANCE retorna SQL_OAC_LEVEL1.  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE retorna SQL_OSCC_COMPLIANT.  
  
 SQL_ODBC_SQL_CONFORMANCE retorna SQL_OSC_MINIMUM. Há suporte para sintaxe SQL mínima.  
  
 Retorna um SQL_ODBC_SQL_OPT_IEF "N".  
  
 SQL_ODBC_VER é implementada pelo Gerenciador de Driver.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT returns "N".  
  
 Retorna um SQL_OUTER_JOINS "N".  
  
 SQL_OWNER_TERM retorna "". O Driver de ODBC do Visual FoxPro não suporta proprietários para seus objetos.  
  
 SQL_OWNER_USAGE retornará 0. O Driver de ODBC do Visual FoxPro não suporta proprietários para seus objetos.  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS retorna SQL_POS_POSITION.  
  
 SQL_POSITIONED_STATEMENTS retornará 0.  
  
 SQL_PROCEDURE_TERM retorna "".  
  
 Retorna SQL_PROCEDURES ' n '.  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION retorna SQL_QL_START.  
  
 Retorna SQL_QUALIFIER_NAME_SEPARATOR '!' ou '\\'. É o separador entre o banco de dados e tabela '!' para fontes de dados conectados ao [bancos de dados](../../odbc/microsoft/visual-foxpro-terminology.md), e '\\' para fontes de dados que são os diretórios de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 SQL_QUALIFIER_TERM retorna "database" ou "directory". O qualificador é "database" para fontes de dados conectado ao [bancos de dados](../../odbc/microsoft/visual-foxpro-terminology.md)e "diretório" para fontes de dados que são os diretórios de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Não oferece suporte a SQL_QUALIFIER_USAGE SQL_QU_PRIVILEGE_DEFINITION; ele retorna SQL_QU_DML_STATEMENT ou SQL_QU_TABLE_DEFINITION.  
  
 SQL_QUOTED_IDENTIFIER_CASE retorna SQL_IC_MIXED.  
  
## <a name="r"></a>R  
 Retorna um SQL_ROW_UPDATES "N". O Driver de ODBC do Visual FoxPro dá suporte a cursores somente estáticos e de avanço.  
  
## <a name="s"></a>P  
 SQL_SCROLL_CONCURRENCY retorna SQL_SCCO_READ_ONLY.  
  
 SQL_SCROLL_OPTIONS retorna SQL_SO_STATIC ou SQL_SO_READONLY.  
  
 SQL_SEARCH_PATTERN_ESCAPE retorna "\\".  
  
 SQL_SERVER_NAME returns "".  
  
 SQL_SPECIAL_CHARACTERS returns "~@#$%^".  
  
 SQL_STATIC_SENSITIVITY retornará 0. O Driver de ODBC do Visual FoxPro não oferece suporte a atualizações posicionais.  
  
 Não oferece suporte a SQL_STRING_FUNCTIONS SQL_FN_STR_INSERT, SQL_FN_STR_LOCATE, SQL_FN_STR_LOCATE_2 ou SQL_FN_STR_SOUNDEX.  
  
 Ele retorna:  
  
-   SQL_FN_STR_ASCII  
  
-   SQL_FN_STR_CHAR  
  
-   SQL_FN_STR_CONCAT  
  
-   SQL_FN_STR_DIFFERENCE  
  
-   SQL_FN_STR_LCASE  
  
-   SQL_FN_STR_LEFT  
  
-   SQL_FN_STR_LENGTH  
  
-   SQL_FN_STR_LTRIM  
  
-   SQL_FN_STR_REPEAT  
  
-   SQL_FN_STR_REPLACE  
  
-   SQL_FN_STR_RIGHT  
  
-   SQL_FN_STR_RTRIM  
  
-   SQL_FN_STR_SUBSTRING  
  
-   SQL_FN_STR_UCASE  
  
-   SQL_FN_STR_SPACE.  
  
 SQL_SUBQUERIES retorna:  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED.  
  
 SQL_SYSTEM_FUNCTIONS retorna:  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 mas não:  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM retorna "table".  
  
 SQL_TIMEDATE_ADD_INTERVALS retorna:  
  
-   SQL_FN_TSI_ SECOND  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 mas não:  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS retorna:  
  
-   SQL_FN_TSI_ SECOND  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 Não oferece suporte a SQL_TIMEDATE_FUNCTIONS SQL_FN_TD_QUARTER, SQL_FN_TD_TIMESTAMPADD, SQL_FN_TD_DAYOFYEAR ou SQL_FN_TD_WEEK.  
  
 Ele retorna:  
  
-   SQL_FN_TD_CURDATE  
  
-   SQL_FN_TD_CURTIME  
  
-   SQL_FN_TD_DAYNAME  
  
-   SQL_FN_TD_DAYOFMONTH  
  
-   SQL_FN_TD_DAYOFWEEK  
  
-   SQL_FN_TD_HOUR  
  
-   SQL_FN_TD_MINUTE  
  
-   SQL_FN_TD_MONTH  
  
-   SQL_FN_TD_MONTHNAME  
  
-   SQL_FN_TD_NOW  
  
-   SQL_FN_TD_SECOND  
  
-   SQL_FN_TD_TIMESTAMPDIFF  
  
-   SQL_FN_TD_YEAR .  
  
 SQL_TXN_CAPABLE retorna SQL_TC_DML.  
  
 SQL_TXN_ISOLATION_OPTION returns SQL_TXN_READ_COMMITTED.  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION retorna SQL_U_UNION ou SQL_U_UNION_ALL.  
  
 SQL_USER_NAME returns \<blank>.
