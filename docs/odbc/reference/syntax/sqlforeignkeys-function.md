---
title: Função SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1aeaef9b120a0bd4be008adafe8e9a24724279a0
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537251"
---
# <a name="sqlforeignkeys-function"></a>Função SQLForeignKeys
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLForeignKeys** pode retornar:  
  
-   Uma lista de chaves estrangeiras na tabela especificada (colunas na tabela especificada que referenciam as chaves primárias em outras tabelas).  
  
-   Uma lista de chaves estrangeiras em outras tabelas que fazem referência à chave primária na tabela especificada.  
  
 O driver retornará cada lista como um conjunto de resultados na declaração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *PKCatalogName*  
 [Entrada] Nome de catálogo da tabela de chave primária. Se um driver compatível com catálogos para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não têm catálogos. *PKCatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *PKCatalogName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *PKCatalogName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento de **PKCatalogName*, em caracteres.  
  
 *PKSchemaName*  
 [Entrada] Nome do esquema de tabela de chave primária. Se um driver compatível com esquemas para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não tem esquemas. *PKSchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *PKSchemaName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *PKSchemaName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento de **PKSchemaName*, em caracteres.  
  
 *PKTableName*  
 [Entrada] Nome da tabela de chave primária. *PKTableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *PKTableName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *PKTableName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento de **PKTableName*, em caracteres.  
  
 *FKCatalogName*  
 [Entrada] Nome de catálogo da tabela de chave estrangeira. Se um driver compatível com catálogos para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não têm catálogos. *FKCatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *FKCatalogName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *FKCatalogName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength4*  
 [Entrada] Comprimento de **FKCatalogName*, em caracteres.  
  
 *FKSchemaName*  
 [Entrada] Nome do esquema de tabela de chave estrangeira. Se um driver compatível com esquemas para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não tem esquemas. *FKSchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *FKSchemaName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *FKSchemaName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength5*  
 [Entrada] Comprimento de **FKSchemaName*, em caracteres.  
  
 *FKTableName*  
 [Entrada] Nome da tabela de chave estrangeira. *FKTableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *FKTableName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *FKTableName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength6*  
 [Entrada] Comprimento de **FKTableName*, em caracteres.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLForeignKeys** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* do SQL _HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLForeignKeys** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto sobre o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver, se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tem retornar SQL_NO_DATA.<br /><br /> Um cursor foi aberto sobre o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*, e, em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) os argumentos *PKTableName* e *FKTableName* foram ambos ponteiros nulos.<br /><br /> O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *FKCatalogName* ou *PKCatalogName* argumento era um ponteiro nulo e o SQL_CATALOG_NAME *o tipo de informação*retorna nomes de catálogo têm suporte.<br /><br /> (DM) o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *FKSchemaName*, *PKSchemaName*, *FKTableName*, ou *PKTableName*  argumento é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando a função SQLForeignKeys foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento do nome da era menor que 0 mas não iguais a SQL_NTS.|  
|||O valor de um dos argumentos de comprimento de nome excedeu o valor de comprimento máximo para o nome correspondente. (Consulte "Comentários".)|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Foi especificado um nome de catálogo, e o driver ou fonte de dados não oferece suporte a catálogos.<br /><br /> Foi especificado um nome de esquema e o driver ou fonte de dados não oferece suporte a esquemas.|  
|||A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo SQL_ATTR_CURSOR_TYPE de instrução foi definido como um tipo de cursor para o qual o driver não oferece suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre como as informações retornadas por essa função podem ser usadas, consulte [usa do catálogo de dados](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Se \* *PKTableName* contém um nome de tabela **SQLForeignKeys** retorna um conjunto de resultados que contém a chave primária da tabela especificada e todas as chaves estrangeiras que fazem referência a ele. A lista de chaves estrangeiras em outras tabelas não tem chaves estrangeiras que apontam para restrições unique na tabela especificada.  
  
 Se \* *FKTableName* contém um nome de tabela **SQLForeignKeys** retorna um conjunto de resultados que contém todas as chaves estrangeiras na tabela especificada que apontam para as chaves primárias em outras tabelas e o chaves primárias em outras tabelas para que eles se referem. A lista de chaves estrangeiras na tabela especificada não contém chaves estrangeiras que fazem referência a restrições exclusivas em outras tabelas.  
  
 Se os dois \* *PKTableName* e \* *FKTableName* contêm nomes de tabela **SQLForeignKeys** retorna as chaves estrangeiras na tabela especificada na \* *FKTableName* que se referem a chave primária da tabela especificada na **PKTableName*. Isso deve ser uma chave no máximo.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLForeignKeys** retorna resultados como um conjunto de resultados padrão. Se as chaves estrangeiras associadas com uma chave primária forem solicitadas, o conjunto de resultados é ordenado por FKTABLE_CAT, FKTABLE_SCHEM, FKTABLE_NAME e KEY_SEQ. Se as chaves primárias associadas com uma chave estrangeira forem solicitadas, o conjunto de resultados é ordenado por PKTABLE_CAT, PKTABLE_SCHEM, PKTABLE_NAME e KEY_SEQ. A tabela a seguir lista as colunas no conjunto de resultados.  
  
 Os comprimentos das colunas VARCHAR não são mostrados na tabela; os comprimentos reais dependem da fonte de dados. Para determinar os comprimentos reais do PKTABLE_CAT ou FKTABLE_CAT, PKTABLE_SCHEM ou FKTABLE_SCHEM, PKTABLE_NAME ou FKTABLE_NAME e PKCOLUMN_NAME ou FKCOLUMN_NAME colunas, um aplicativo pode chamar **SQLGetInfo** com o SQL_MAX_ Opções de CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN e SQL_MAX_COLUMN_NAME_LEN.  
  
 As seguintes colunas foram renomeadas para ODBC 3 *. x.* As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar por número de coluna.  
  
|Coluna de ODBC 2.0|3 de ODBC *. x* coluna|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 14 (Observações) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contagem regressiva do final do conjunto em vez de especificar uma posição ordinal explícita de resultados. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|Nome de catálogo da tabela de chave primária; NULL se não for aplicável à fonte de dados. Se um driver compatível com catálogos para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema de tabela de chave primária; NULL se não for aplicável à fonte de dados. Se um driver compatível com esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não tem esquemas.|  
|PKTABLE_NAME (ODBC 1.0)|3|Varchar não nulo|Nome da tabela de chave primária.|  
|PKCOLUMN_NAME (ODBC 1.0)|4|Varchar não nulo|Nome da coluna de chave primária. O driver retornará uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|Nome de catálogo da tabela de chave estrangeira; NULL se não for aplicável à fonte de dados. Se um driver compatível com catálogos para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|Nome do esquema de tabela de chave estrangeira; NULL se não for aplicável à fonte de dados. Se um driver compatível com esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não tem esquemas.|  
|FKTABLE_NAME (ODBC 1.0)|7|Varchar não nulo|Nome da tabela de chave estrangeira.|  
|FKCOLUMN_NAME (ODBC 1.0)|8|Varchar não nulo|Nome da coluna de chave estrangeira. O driver retornará uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|KEY_SEQ (ODBC 1.0)|9|Smallint não NULL|Número de sequência de coluna na chave (começando com 1).|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|Ação a ser aplicada à chave estrangeira quando a operação SQL é **atualização**. Pode ter um dos valores a seguir. (A tabela referenciada é a tabela que tem a chave primária; a tabela de referência é a tabela que tem a chave estrangeira).<br /><br /> SQL_CASCADE: Quando a chave primária da tabela referenciada for atualizada, a chave estrangeira da tabela de referência também é atualizada.<br /><br /> SQL_NO_ACTION: Se uma atualização da chave primária da tabela referenciada causaria uma "referência pendentes" na tabela de referência (ou seja, linhas na tabela de referência não teria nenhum correspondentes na tabela de referência), a atualização será rejeitada. Se uma atualização da chave estrangeira da tabela de referência introduziria um valor que não existe como um valor da chave primária da tabela referenciada, a atualização será rejeitada. (Essa ação é o mesmo que a ação de SQL_RESTRICT em 2 de ODBC *. x*.)<br /><br /> SQL_SET_NULL: Quando uma ou mais linhas na tabela de referência são atualizadas de forma que um ou mais componentes da chave primária são alterados, os componentes da chave estrangeira na tabela de referência que correspondem aos componentes alterados da chave primária são definidos como NULL em todas as linhas de tabela de referência correspondentes.<br /><br /> SQL_SET_DEFAULT: Quando uma ou mais linhas na tabela de referência são atualizadas de forma que um ou mais componentes da chave primária são alterados, os componentes da chave estrangeira na tabela de referência que correspondem aos componentes alterados da chave primária são definidos como o applicab Le valores de padrão em todas as linhas correspondentes da tabela de referência.<br /><br /> NULL se não for aplicável à fonte de dados.|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|Ação a ser aplicada à chave estrangeira quando a operação SQL é **excluir**. Pode ter um dos valores a seguir. (A tabela referenciada é a tabela que tem a chave primária; a tabela de referência é a tabela que tem a chave estrangeira).<br /><br /> SQL_CASCADE: Quando uma linha na tabela referenciada for excluída, todas as linhas correspondentes nas tabelas de referência também são excluídas.<br /><br /> SQL_NO_ACTION: Se uma exclusão de uma linha na tabela de referência causaria uma "referência pendentes" na tabela de referência (ou seja, linhas na tabela de referência não teria nenhum correspondentes na tabela de referência), a atualização será rejeitada. (Essa ação é o mesmo que a ação de SQL_RESTRICT em 2 de ODBC *. x*.)<br /><br /> SQL_SET_NULL: Quando uma ou mais linhas na tabela de referência são excluídas, cada componente da chave estrangeira da tabela de referência é definida como NULL em todas as linhas correspondentes da tabela de referência.<br /><br /> SQL_SET_DEFAULT: Quando uma ou mais linhas na tabela de referência são excluídas, cada componente da chave estrangeira da tabela de referência é definida para o padrão aplicável em todas as linhas correspondentes da tabela de referência.<br /><br /> NULL se não for aplicável à fonte de dados.|  
|COLUNAS FK_NAME (ODBC 2.0)|12|Varchar|Nome da chave estrangeira. NULL se não for aplicável à fonte de dados.|  
|PK_NAME (ODBC 2.0)|13|Varchar|Nome da chave primária. NULL se não for aplicável à fonte de dados.|  
|CAPACIDADE DE ADIAMENTO (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED, SQL_INITIALLY_IMMEDIATE, SQL_NOT_DEFERRABLE.|  
  
## <a name="code-example"></a>Exemplo de código  
 Conforme ilustrado na tabela a seguir, este exemplo usa três tabelas, chamadas ORDERS, linhas e os clientes.  
  
|PEDIDOS|LINHAS|CLIENTES|  
|------------|-----------|---------------|  
|ORDERID|ORDERID|CUSTID|  
|CUSTID|LINHAS|NAME|  
|OPENDATE|PARTID|ENDEREÇO|  
|SALESPERSON|QUANTIDADE|TELEFONE|  
|STATUS|||  
  
 Na tabela de pedidos, CUSTID identifica o cliente a quem a venda foi feita. É uma chave estrangeira que se refere ao CUSTID na tabela CUSTOMERS.  
  
 Na tabela de linhas, ORDERID identifica a ordem de venda ao qual o item de linha está associado. É uma chave estrangeira que se refere ao ORDERID da tabela ORDERS.  
  
 Este exemplo chama **SQLPrimaryKeys** para obter a chave primária da tabela ORDERS. O conjunto de resultados terá uma linha; as colunas significativas são mostradas na tabela a seguir.  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|PEDIDOS|ORDERID|1|  
  
 Em seguida, o exemplo chama **SQLForeignKeys** para obter as chaves estrangeiras em outras tabelas que fazem referência a chave primária da tabela ORDERS. O conjunto de resultados terá uma linha; as colunas significativas são mostradas na tabela a seguir.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|PEDIDOS|CUSTID|LINHAS|CUSTID|1|  
  
 Por fim, o exemplo chama **SQLForeignKeys** para obter as chaves estrangeiras na tabela de pedidos que se referem às chaves primárias de outras tabelas. O conjunto de resultados terá uma linha; as colunas significativas são mostradas na tabela a seguir.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|CLIENTES|CUSTID|PEDIDOS|CUSTID|1|  
  
```cpp  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando as colunas de uma chave primária|[Função SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|Retornando estatísticas de tabela e índices|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
