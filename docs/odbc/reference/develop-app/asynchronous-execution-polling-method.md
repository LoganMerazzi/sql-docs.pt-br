---
title: Execução assíncrona (método de sondagem) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ca0a5094e40f13aef4b4f87d5642e51e7a9b765
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306297"
---
# <a name="asynchronous-execution-polling-method"></a>Execução assíncrona (Método de Sondagem)
Antes do ODBC 3.8 e o SDK do Windows 7, operações assíncronas eram permitidas apenas em funções de instrução. Para obter mais informações, consulte o **execução de operações de instrução assincronamente**, mais adiante neste tópico.  
  
 No Windows 7 SDK o ODBC 3.8 introduziu a execução assíncrona em operações relacionadas à conexão. Para obter mais informações, consulte o **execução de operações de Conexão assíncrona** seção, mais adiante neste tópico.  
  
 No SDK do Windows 7, para as operações de conexão, ou instrução assíncrona um aplicativo determinado que a operação assíncrona foi concluída usando o método de sondagem. A partir do SDK do Windows 8, você pode determinar que uma operação assíncrona foi concluída usando o método de notificação. Para obter mais informações, consulte [execução assíncrona (método de notificação)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
 Por padrão, drivers executam funções ODBC de forma síncrona; ou seja, o aplicativo chama uma função e o driver retorna o controle para o aplicativo até que termine a execução da função. No entanto, algumas funções podem ser executadas de forma assíncrona; ou seja, o aplicativo chama a função e o driver, após o processamento mínimo, retorna o controle para o aplicativo. O aplicativo pode chamar outras funções enquanto a primeira função ainda está em execução.  
  
 Execução assíncrona tem suporte para a maioria das funções que são executadas em grande parte na fonte de dados, como as funções para estabelecer conexões, preparar e executar instruções SQL, recuperar metadados, buscar dados e confirmar as transações. Ele é mais útil quando a tarefa que está sendo executada na fonte de dados leva muito tempo, como um processo de logon ou uma consulta complexa em relação a um banco de dados grande.  
  
 Quando o aplicativo executa uma função com uma instrução ou a conexão que está habilitado para processamento assíncrono, o driver executa uma quantidade mínima de processamento (como argumentos para erros de verificação), entrega o processamento para a fonte de dados e retorna o controle para o aplicativo com o código de retorno de SQL_STILL_EXECUTING. O aplicativo, em seguida, executa outras tarefas. Para determinar quando a função assíncrona for concluída, o aplicativo sonda o driver em intervalos regulares, chamando a função com os mesmos argumentos que ele usado originalmente. Se a função ainda está em execução, ele retornará SQL_STILL_EXECUTING; Se a execução foi concluída, ela retornará o código que poderia ter retornado tivesse ela executada de forma síncrona, como SQL_SUCCESS, SQL_ERROR ou SQL_NEED_DATA.  
  
 Se uma função é executada de forma síncrona ou assíncrona é um driver específico. Por exemplo, suponha que os metadados do conjunto de resultados é armazenado em cache no driver. Nesse caso, ele usa muito pouco tempo para executar **SQLDescribeCol** e o driver deve simplesmente executar a função em vez de artificialmente atrasar a execução. Por outro lado, se o driver precisa recuperar os metadados da fonte de dados, ele deve retornar o controle ao aplicativo enquanto ele está fazendo isso. Portanto, o aplicativo deve ser capaz de lidar com um código de retorno diferente de SQL_STILL_EXECUTING quando ele primeiro executa uma função de forma assíncrona.  
  
## <a name="executing-statement-operations-asynchronously"></a>Executar operações de instrução de forma assíncrona  
 As seguintes funções de declaração operam em uma fonte de dados e podem executar de forma assíncrona:  
  
||||  
|-|-|-|  
|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 Execução de instrução assíncrono é controlada por instrução ou uma base por conexão, dependendo da fonte de dados. Ou seja, o aplicativo não especifica que uma função específica deve ser executado de forma assíncrona, mas que qualquer função executada em uma determinada instrução é executado de forma assíncrona. Para localizar out há suporte para a qual deles, um aplicativo chama [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) com uma opção de SQL_ASYNC_MODE. SQL_AM_CONNECTION será retornado se houver suporte para a execução assíncrona de nível de conexão (para um identificador de instrução); SQL_AM_STATEMENT se há suporte para a execução assíncrona de nível de instrução.  
  
 Para especificar que as funções executadas com uma instrução específica devem ser executadas de forma assíncrona, o aplicativo chama **SQLSetStmtAttr** o SQL_ATTR_ASYNC_ENABLE de atributo e o define como SQL_ASYNC_ENABLE_ON. Se há suporte para processamento assíncrono de nível de conexão, o atributo da instrução SQL_ATTR_ASYNC_ENABLE é somente leitura e seu valor é o mesmo que o atributo de conexão da conexão no qual a instrução foi alocada. Ele é específica do driver, se o valor do atributo de instrução é definido durante o tempo de alocação de instrução ou posterior. Tentar defini-la retornará SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado).  
  
 Para especificar que as funções executadas com uma conexão específica devem ser executadas de forma assíncrona, o aplicativo chama **SQLSetConnectAttr** o SQL_ATTR_ASYNC_ENABLE de atributo e o define como SQL_ASYNC_ENABLE_ON. Todos os identificadores de instrução futuras alocados na conexão serão habilitados para a execução assíncrona; ele é definido pelo driver se os identificadores de instrução existente serão habilitados por esta ação. Se SQL_ATTR_ASYNC_ENABLE for definido como SQL_ASYNC_ENABLE_OFF, todas as instruções sobre a conexão estiver no modo síncrono. Um erro será retornado se a execução assíncrona estiver habilitada, enquanto houver uma instrução ativa sobre a conexão.  
  
 Para determinar o número máximo de instruções simultâneas ativas no modo assíncrono e o driver pode dar suporte a uma determinada conexão, o aplicativo chama **SQLGetInfo** com a opção SQL_MAX_ASYNC_CONCURRENT_STATEMENTS.  
  
 O código a seguir demonstra como funciona o modelo de sondagem:  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 Enquanto uma função está em execução de forma assíncrona, o aplicativo pode chamar funções em quaisquer outras instruções. O aplicativo também pode chamar funções em qualquer conexão, exceto aquele associado à instrução assíncrona. Mas o aplicativo só pode chamar a função original e as funções a seguir (com o identificador de instrução ou sua conexão associada, o identificador de ambiente), após uma operação de instrução retornará SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (no identificador de instrução)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 Se o aplicativo chamar qualquer outra função com a instrução assíncrona ou com a conexão associada a essa instrução, a função retornará SQLSTATE HY010 (função de erro de sequência), por exemplo.  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 Quando um aplicativo chama uma função para determinar se ele ainda está em execução assincronamente, ele deve usar o identificador de instrução original. Isso ocorre porque a execução assíncrona é rastreada em uma base por instrução. O aplicativo também deve fornecer valores válidos para os outros argumentos - os argumentos originais serão fazer - para cancelar a verificação no Gerenciador de Driver de erro. No entanto, depois que o driver verifica o identificador de instrução e determina que a instrução está em execução assíncrona, ele ignora todos os outros argumentos.  
  
 Enquanto uma função está em execução assíncrona - ou seja, depois que ele tiver retornado SQL_STILL_EXECUTING e antes de retornar um código diferente – o aplicativo poderá cancelá-lo chamando **SQLCancel** ou **SQLCancelHandle** com o mesmo identificador de instrução. Isso não é garantido para cancelar a execução da função. Por exemplo, a função talvez já terminou. Além disso, o código retornado pelo **SQLCancel** ou **SQLCancelHandle** indica somente se a tentativa de cancelar a função foi bem-sucedida, não se ele realmente cancelados a função. Para determinar se a função foi cancelada, o aplicativo chama a função novamente. Se a função foi cancelada, ela retornará SQL_ERROR e SQLSTATE HY008 (operação cancelada). Se a função não tiver sido cancelada, ele retorna outro código, como SQL_SUCCESS, SQL_STILL_EXECUTING ou SQL_ERROR com SQLSTATE um diferente.  
  
 Para desabilitar a execução assíncrona de uma instrução específica quando o driver dá suporte ao processamento assíncrono de nível de instrução, o aplicativo chama **SQLSetStmtAttr** o SQL_ATTR_ASYNC_ENABLE de atributo e o configura para SQL _ ASYNC_ENABLE_OFF. Se o driver dá suporte ao processamento assíncrono de nível de conexão, o aplicativo chama **SQLSetConnectAttr** para definir SQL_ATTR_ASYNC_ENABLE como SQL_ASYNC_ENABLE_OFF, que desabilita a execução assíncrona de todas as instruções sobre o conexão.  
  
 O aplicativo deve processar os registros de diagnóstico no loop de repetição da função original. Se **SQLGetDiagField** ou **SQLGetDiagRec** é chamado quando uma função assíncrona está em execução, ele retornará a lista atual de registros de diagnóstico. Cada vez que a chamada de função original é repetida, ele limpa registros de diagnóstico anteriores.  
  
## <a name="executing-connection-operations-asynchronously"></a>Executando operações de Conexão de forma assíncrona  
 Antes do ODBC 3.8, execução assíncrona foi permitida para operações relacionadas à instrução, como preparar, executar e buscar, bem como para operações de metadados de catálogo. A partir do ODBC 3.8, execução assíncrona também é possível que operações relacionadas à conexão, tal como se conectar, desconectar, commit e rollback.  
  
 Para obter mais informações sobre o ODBC 3.8, consulte [o que há de novo no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
 Executar operações de conexão de forma assíncrona é útil nos seguintes cenários:  
  
-   Quando um pequeno número de segmentos gerencia um grande número de dispositivos com as taxas de dados muito alta. Para maximizar a escalabilidade e capacidade de resposta é desejável para todas as operações ser assíncrona.  
  
-   Quando você quiser se sobrepor a operações de banco de dados em várias conexões para reduzir o tempo de transferência decorrido.  
  
-   Chamadas ODBC assíncronas eficientes e a capacidade de cancelar operações de conexão habilita um aplicativo permitir que o usuário cancele qualquer operação lenta sem ter de esperar tempos limites.  
  
 As funções a seguir, que operam em identificadores de conexão, agora podem ser executadas de forma assíncrona:  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 Para determinar se um driver dá suporte a operações assíncronas dessas funções, um aplicativo chama **SQLGetInfo** com SQL_ASYNC_DBC_FUNCTIONS. SQL_ASYNC_DBC_CAPABLE será retornado se há suporte para operações assíncronas. SQL_ASYNC_DBC_NOT_CAPABLE será retornado se não há suporte para operações assíncronas.  
  
 Para especificar que as funções executadas com uma conexão específica devem ser executadas de forma assíncrona, o aplicativo chama **SQLSetConnectAttr** e define o atributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE como SQL_ASYNC_DBC_ENABLE ON. Definir um atributo de conexão antes de estabelecer uma conexão sempre executa de forma síncrona. Além disso, a operação de definir a conexão atributo SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE com **SQLSetConnectAttr** sempre executa de forma síncrona.  
  
 Um aplicativo pode permitir que a operação assíncrona antes de fazer uma conexão. Porque o Gerenciador de Driver não pode determinar qual driver a ser usado antes de fazer uma conexão, o Gerenciador de Driver sempre retornará com êxito no **SQLSetConnectAttr**. No entanto, ele poderá falhar ao se conectar se o driver ODBC não dá suporte a operações assíncronas.  
  
 Em geral, pode haver no máximo um função de execução de forma assíncrona associado com um identificador de conexão específica ou identificador de instrução. No entanto, um identificador de conexão pode ter mais de um identificador de instrução associado. Se não houver nenhuma operação assíncrona em execução no identificador de conexão, um identificador de instrução associado pode executar uma operação assíncrona. Da mesma forma, você pode ter uma operação assíncrona em um identificador de conexão se não houver nenhuma operação assíncrona em andamento em qualquer identificador de instrução associado. Uma tentativa de executar uma operação assíncrona usando um identificador que está executando uma operação assíncrona retornará HY010, "Erro de sequência de função".  
  
 Se uma operação de conexão retornará SQL_STILL_EXECUTING, um aplicativo só pode chamar a função original e as funções a seguir para esse identificador de conexão:  
  
-   **SQLCancelHandle** (no identificador de conexão)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **Falha de SQLAllocHandle** (alocando ENV/DBC)  
  
-   **SQLAllocHandleStd** (alocando ENV/DBC)  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 O aplicativo deve processar os registros de diagnóstico no loop de repetição da função original. Se SQLGetDiagField ou SQLGetDiagRec é chamado quando uma função assíncrona está em execução, ele retornará a lista atual de registros de diagnóstico. Cada vez que a chamada de função original é repetida, ele limpa registros de diagnóstico anteriores.  
  
 Se uma conexão está sendo aberto ou fechado de forma assíncrona, a operação é concluída quando o aplicativo recebe SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO na chamada de função original.  
  
 Uma nova função foi adicionada ao ODBC 3.8 **SQLCancelHandle**. Essa função cancela as funções de seis conexão (**SQLBrowseConnect**, **SQLConnect**, **SQLDisconnect**, **SQLDriverConnect**, **SQLEndTran**, e **SQLSetConnectAttr**). Um aplicativo deve chamar **SQLGetFunctions** para determinar se o driver suporta **SQLCancelHandle**. Assim como acontece com **SQLCancel**, se **SQLCancelHandle** retornar com sucesso, isso não significa que a operação foi cancelada. Um aplicativo deve chamar a função original novamente para determinar se a operação foi cancelada. **SQLCancelHandle** lhe permite cancelar operações assíncronas em identificadores de instrução ou identificadores de conexão. Usando o **SQLCancelHandle** para cancelar uma operação em uma instrução de identificador é o mesmo que chamar **SQLCancel**.  
  
 Não é necessário dar suporte a ambos **SQLCancelHandle** e operações de conexão assíncrona ao mesmo tempo. Um driver pode dar suporte a operações assíncronas de conexão, mas não **SQLCancelHandle**, ou vice-versa.  
  
 Operações de conexão assíncrona e **SQLCancelHandle** também pode ser usado por ODBC 3. x e os aplicativos ODBC 2. x com um driver ODBC 3.8 e o Gerenciador de Driver do ODBC 3.8. Para obter informações sobre como habilitar um aplicativo mais antigo usar novos recursos na versão mais recente do ODBC, consulte [matriz de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
### <a name="connection-pooling"></a>Pool de conexões  
 Sempre que o pool de conexão estiver habilitado, somente minimamente há suporte para operações assíncronas para estabelecer uma conexão (com **SQLConnect** e **SQLDriverConnect**) e fechando uma conexão com **SQLDisconnect**. Mas um aplicativo ainda deve ser capaz de lidar com o valor de retorno SQL_STILL_EXECUTING **SQLConnect**, **SQLDriverConnect**, e **SQLDisconnect**.  
  
 Quando o pooling de conexão está habilitado, **SQLEndTran** e **SQLSetConnectAttr** têm suporte para operações assíncronas.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra como usar **SQLSetConnectAttr** para habilitar a execução assíncrona para funções relacionadas à conexão.  
  
### <a name="code"></a>Código  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 Este exemplo mostra operações de confirmação assíncrona. Operações de reversão também podem ser feitas dessa maneira.  
  
### <a name="code"></a>Código  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Executando instruções ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
