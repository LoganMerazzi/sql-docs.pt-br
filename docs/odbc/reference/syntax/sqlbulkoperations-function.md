---
title: Função SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06a1997b482c45ea4b529c1230ef1cb2c61dc873
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63237855"
---
# <a name="sqlbulkoperations-function"></a>Função SQLBulkOperations
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLBulkOperations** executa inserções em massa e indicador em massa operações, incluindo a atualização, excluir e buscar por indicador.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *Operação*  
 [Entrada] Operação a ser executada:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 Para obter mais informações, consulte "Comentários".  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLBulkOperations** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLBulkOperations** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver . O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
 Para todos esses SQLSTATEs que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx SQLSTATEs), SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em um ou mais, mas nem todas as linhas de uma operação de várias linhas, e SQL_ERROR será retornado se ocorrer um erro em um operação de uma única linha.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Truncamento à direita de dados de cadeia de caracteres|O *operação* argumento era SQL_FETCH_BY_BOOKMARK e cadeia de caracteres ou dados binários retornados para uma coluna ou colunas com um tipo de dados de SQL_C_CHAR ou SQL_C_BINARY resultaram em truncamento de caractere não vazios ou nulos de dados binários.|  
|01S01|Erro na linha|O *operação* argumento era SQL_ADD e ocorreu um erro em uma ou mais linhas ao executar a operação, mas pelo menos uma linha foi adicionada com êxito. (A função retornará SQL_SUCCESS_WITH_INFO.)<br /><br /> (Esse erro é gerado somente quando um aplicativo está funcionando com um ODBC 2. *x* driver.)|  
|01S07|Truncamento fracionário|O *operação* argumento era SQL_FETCH_BY_BOOKMARK, o tipo de dados do buffer de aplicativo não era SQL_C_CHAR ou SQL_C_BINARY e os dados retornados aos buffers de aplicativo para uma ou mais colunas foi truncados. (Para tipos de dados numéricos do C, a parte fracionária do número foi truncada. Para o tempo, carimbo de hora e tipos de dados de intervalo de C que contêm um componente de tempo, a parte fracionária do tempo foi truncada.)<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O *operação* argumento era SQL_FETCH_BY_BOOKMARK, e o valor de dados de uma coluna no conjunto de resultados não pôde ser convertido para o tipo de dados especificado pela *TargetType* argumento na chamada para **SQLBindCol**.<br /><br /> O *operação* argumento era SQL_UPDATE_BY_BOOKMARK ou SQL_ADD, e o valor dos dados nos buffers de aplicativo não pôde ser convertido para o tipo de dados de uma coluna no conjunto de resultados.|  
|07009|Índice de descritor inválido|O argumento *operação* era SQL_ADD, e uma coluna foi associada com um número de coluna maior que o número de colunas no conjunto de resultados.|  
|21S02|Grau da tabela derivada não corresponde à lista de colunas|O argumento *operação* era SQL_UPDATE_BY_BOOKMARK; e não há colunas foram atualizáveis porque todas as colunas foram não associadas ou somente leitura ou o valor no buffer de comprimento/indicador associado foi SQL_COLUMN_IGNORE.|  
|22001|Truncamento à direita de dados de cadeia de caracteres|A atribuição de um caractere ou valor binário para uma coluna no conjunto de resultados resultou em truncamento de não vazio (para caracteres) ou caracteres nulos (para binário) ou bytes.|  
|22003|Valor numérico fora do intervalo|O *operação* argumento era SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e a atribuição de um valor numérico para uma coluna no conjunto de resultados causou a parte inteira (em vez de fracionários) o número a ser truncado.<br /><br /> O argumento *operação* era SQL_FETCH_BY_BOOKMARK e retornar o valor numérico de uma ou mais colunas associadas causaria uma perda de dígitos significativos.|  
|22007|Formato de data/hora inválido|O *operação* argumento estava SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e a atribuição de um valor de data ou carimbo de hora a uma coluna no conjunto de resultados causou o ano, mês, dia campo ou para estar fora do intervalo.<br /><br /> O argumento *operação* era SQL_FETCH_BY_BOOKMARK e retornando o valor de data ou carimbo de data para um ou mais colunas associadas teria causado o ano, mês, dia campo ou para estar fora do intervalo.|  
|22008|Estouro no campo de data/hora|O *operação* argumento era SQL_ADD ou SQL_UPDATE_BY_BOOKMARK, e o desempenho das operações aritméticas com dados que estão sendo enviados a uma coluna no conjunto de resultados de datetime resultou em um campo de data e hora (o ano, mês, dia, hora, minuto ou segundo campo) do resultado que fica fora do intervalo permitido de valores para o campo ou sendo inválido com base nas regras de natural do calendário gregoriano para datetimes.<br /><br /> O *operação* argumento era SQL_FETCH_BY_BOOKMARK, e o desempenho das operações aritméticas com dados que estão sendo recuperados do conjunto de resultados de datetime resultou em um campo de data e hora (o ano, mês, dia, hora, minuto ou segundo campo) das resulta que fica fora do intervalo permitido de valores para o campo ou sendo inválido com base nas regras de natural do calendário gregoriano para datetimes.|  
|22015|Estouro no campo de intervalo|O *operação* argumento era SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e a atribuição de um valor numérico exato ou o tipo de intervalo de C para um intervalo de tipo de dados SQL causou uma perda de dígitos significativos.<br /><br /> O *operação* argumento era SQL_ADD ou SQL_UPDATE_BY_BOOKMARK; ao atribuir a um intervalo de tipo SQL, não havia nenhuma representação do valor do tipo C no intervalo de tipo SQL.<br /><br /> O *operação* argumento era SQL_FETCH_BY_BOOKMARK e atribuição de um numérico exato ou o intervalo de tipo SQL para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> O *operação* argumento era SQL_FETCH_BY_BOOKMARK; ao atribuir a um tipo de intervalo de C, não havia nenhuma representação do valor do tipo SQL no tipo de intervalo de C.|  
|22018|Valor de caractere inválido para especificação de conversão|O *operação* argumento era SQL_FETCH_BY_BOOKMARK; o tipo C era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era válido literal do tipo C associado.<br /><br /> O argumento *operação* era SQL_ADD ou SQL_UPDATE_BY_BOOKMARK; o tipo SQL era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna não era um literal válido das tipo SQL associado.|  
|23000|Violação de restrição de integridade|O *operação* argumento era SQL_ADD, SQL_DELETE_BY_BOOKMARK ou SQL_UPDATE_BY_BOOKMARK e uma restrição de integridade foi violada.<br /><br /> O *operação* argumento era SQL_ADD e uma coluna que não estava associada é definida como NOT NULL e não tem nenhum padrão.<br /><br /> O *operação* argumento era SQL_ADD, o comprimento especificado em que o limite *StrLen_or_IndPtr* buffer era SQL_COLUMN_IGNORE e a coluna não tem um valor padrão.|  
|24000|Estado de cursor inválido|O *StatementHandle* estava em um estado de executado, mas nenhum conjunto de resultados foi associado a *StatementHandle*.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|42000|Sintaxe ou violação de acesso|O driver não foi possível bloquear a linha conforme necessário para executar a operação solicitada na *operação* argumento.|  
|44000|Violação COM OPÇÃO DE VERIFICAÇÃO|O *operação* argumento era SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e a inserção ou atualização foi executada em uma tabela visualizada (ou uma tabela derivada da tabela exibida) que foi criado com a especificação de **WITH CHECK OPTION**, de forma que uma ou mais linhas afetadas pela inserção ou atualização não estará presente na tabela exibida.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLBulkOperations** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) especificado *StatementHandle* não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute**, ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLSetPos** foi chamado para o *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) o driver foi um ODBC 2. *x* driver, e **SQLBulkOperations** foi chamado para um *StatementHandle* antes **SQLFetchScroll** ou **SQLFetch**  foi chamado.<br /><br /> (DM) **SQLBulkOperations** foi chamado após **SQLExtendedFetch** foi chamado no *StatementHandle*.|  
|HY011|Atributo não pode ser definido agora|(DM) o driver foi um ODBC 2. *x* driver e o atributo da instrução SQL_ATTR_ROW_STATUS_PTR foi definida entre as chamadas para **SQLFetch** ou **SQLFetchScroll** e **SQLBulkOperations** .|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|O *operação* argumento era SQL_ADD ou SQL_UPDATE_BY_BOOKMARK; um valor de dados não é um ponteiro nulo; o tipo de dados C foi SQL_C_BINARY ou SQL_C_CHAR; e o valor de comprimento de coluna era menor que 0, mas não iguais a SQL_DATA_AT_EXEC , SQL_COLUMN_IGNORE, SQL_NTS ou SQL_NULL_DATA, ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> O valor em um buffer de comprimento/indicador foi SQL_DATA_AT_EXEC; o tipo de SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específicos da fonte de dados long; e o tipo de informação no SQL_NEED_LONG_DATA_LEN **SQLGetInfo** foi "Y".<br /><br /> O *operação* argumento era SQL_ADD, o atributo da instrução SQL_ATTR_USE_BOOKMARK foi definido como SQL_UB_VARIABLE e a coluna 0 estava associada a um buffer cujo comprimento não era igual ao comprimento máximo para o indicador para esse conjunto de resultados. (Esse tamanho está disponível no campo do IRD SQL_DESC_OCTET_LENGTH e pode ser obtido chamando **SQLDescribeCol**, **SQLColAttribute**, ou **SQLGetDescField**.)|  
|HY092|Identificador de atributo inválido|(DM) o valor especificado para o *operação* argumento era inválido.<br /><br /> O *operação* argumento era SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK, e o atributo de instrução SQL_ATTR_CONCURRENCY foi definido como SQL_CONCUR_READ_ONLY.<br /><br /> O *operação* argumento era SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK ou SQL_UPDATE_BY_BOOKMARK e a coluna de indicador não foi associada ou o atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A driver ou fonte de dados não oferece suporte para a operação solicitada na *operação* argumento.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
  
> [!CAUTION]  
>  Para obter informações sobre estados de instrução **SQLBulkOperations** pode ser chamada e o que ele deve fazer para compatibilidade com o ODBC 2. *x* aplicativos, consulte a [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) seção no Apêndice g: Diretrizes de driver para compatibilidade com versões anteriores.  
  
 Um aplicativo usa **SQLBulkOperations** para executar as seguintes operações na tabela base ou exibição que corresponde à consulta atual:  
  
-   Adicione novas linhas.  
  
-   Atualize um conjunto de linhas em que cada linha é identificada por um indicador.  
  
-   Exclua um conjunto de linhas em que cada linha é identificada por um indicador.  
  
-   Busca um conjunto de linhas em que cada linha é identificada por um indicador.  
  
 Após uma chamada para **SQLBulkOperations**, a posição do cursor de bloco é indefinida. O aplicativo tem que chamar **SQLFetchScroll** para definir a posição do cursor. Um aplicativo deve chamar **SQLFetchScroll** somente com um *FetchOrientation* argumento de SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE ou SQL_FETCH_BOOKMARK. A posição do cursor é indefinida se o aplicativo chama **SQLFetch** ou **SQLFetchScroll** com um *FetchOrientation* argumento de SQL_FETCH_PRIOR, SQL_FETCH_NEXT, ou SQL_FETCH_RELATIVE.  
  
 Uma coluna pode ser ignorada em operações em massa executadas por uma chamada para **SQLBulkOperations** definindo o buffer de comprimento/indicador de coluna especificado na chamada para **SQLBindCol**, para SQL_COLUMN_IGNORE.  
  
 Não é necessário para o aplicativo para definir o atributo da instrução SQL_ATTR_ROW_OPERATION_PTR quando ele chama **SQLBulkOperations** porque as linhas não podem ser ignoradas ao executar operações em massa com essa função.  
  
 O buffer apontado pelo atributo SQL_ATTR_ROWS_FETCHED_PTR declaração contém o número de linhas afetadas por uma chamada para **SQLBulkOperations**.  
  
 Quando o *operação* argumento é SQL_ADD ou SQL_UPDATE_BY_BOOKMARK e lista de seleção da especificação de consulta associada com o cursor contém mais de uma referência para a mesma coluna, ele é definido pelo driver se um erro é gerado ou o driver ignora as referências duplicadas e executa as operações solicitadas.  
  
 Para obter mais informações sobre como usar **SQLBulkOperations**, consulte [atualizando dados com SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).  
  
## <a name="performing-bulk-inserts"></a>Executar inserções em massa  
 Para inserir dados com **SQLBulkOperations**, um aplicativo executa a seguinte sequência de etapas:  
  
1.  Executa uma consulta que retorna um conjunto de resultados.  
  
2.  Define o atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas que deseja inserir.  
  
3.  Chamadas **SQLBindCol** para associar os dados que deseja inserir. Os dados serão associados a uma matriz com um tamanho igual ao valor de SQL_ATTR_ROW_ARRAY_SIZE.  
  
    > [!NOTE]  
    >  O tamanho da matriz apontado pelo atributo SQL_ATTR_ROW_STATUS_PTR instrução deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
4.  Chamadas **SQLBulkOperations**(*StatementHandle,* SQL_ADD) para executar a inserção.  
  
5.  Se o aplicativo tiver definido o atributo da instrução SQL_ATTR_ROW_STATUS_PTR, ele pode inspecionar essa matriz para ver o resultado da operação.  
  
 Se um aplicativo associar a coluna 0 antes de chamar **SQLBulkOperations** com um *operação* argumento de SQL_ADD, o driver atualizará os buffers de coluna associada 0 com os valores de indicador para o recentemente linha inserida. Para isso ocorrer, o aplicativo deve ter definir o atributo da instrução SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE antes de executar a instrução. (Isso não funciona com um ODBC 2. *x* driver.)  
  
 Dados longos podem ser adicionados em partes por SQLBulkOperations, por meio de chamadas para SQLParamData e SQLPutData. Para obter mais informações, consulte "Fornecendo longo dados para Bulk Inserts e Updates" mais adiante, essa referência de função.  
  
 Não é necessário para o aplicativo chamar **SQLFetch** ou **SQLFetchScroll** antes de chamar **SQLBulkOperations** (exceto quando vai contra um ODBC 2. *x* driver; consulte [compatibilidade com versões anteriores e em conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)).  
  
 O comportamento é definido pelo driver se **SQLBulkOperations**, com um *operação* argumento de SQL_ADD, é chamado em um cursor que contém colunas duplicadas. O driver pode retornar um SQLSTATE definido pelo driver, adicione os dados para a primeira coluna que aparece no resultado definido, ou executam outro comportamento definido pelo driver.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>Executando atualizações em massa usando indicadores  
 Para executar atualizações em massa usando indicadores com **SQLBulkOperations**, um aplicativo executa as seguintes etapas na sequência:  
  
1.  Define o atributo da instrução SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE.  
  
2.  Executa uma consulta que retorna um conjunto de resultados.  
  
3.  Define o atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas que deseja atualizar.  
  
4.  Chamadas **SQLBindCol** para associar os dados que deseja atualizar. Os dados serão associados a uma matriz com um tamanho igual ao valor de SQL_ATTR_ROW_ARRAY_SIZE. Ele também chama **SQLBindCol** para associar a coluna 0 (a coluna de indicador).  
  
5.  Copia os indicadores para as linhas que ele está interessado em atualizar para a matriz associada à coluna 0.  
  
6.  Atualiza os dados nos buffers associados.  
  
    > [!NOTE]  
    >  O tamanho da matriz apontado pelo atributo SQL_ATTR_ROW_STATUS_PTR instrução deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
7.  Chamadas **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  Se o aplicativo tiver definido o atributo da instrução SQL_ATTR_ROW_STATUS_PTR, ele pode inspecionar essa matriz para ver o resultado da operação.  
  
8.  Opcionalmente, chama **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) para buscar dados nos buffers associadas de aplicativo para confirmar que a atualização foi executada.  
  
9. Se dados foram atualizados, o driver altera o valor na matriz de status de linha para as linhas apropriadas para SQL_ROW_UPDATED.  
  
 Em massa atualizações realizadas pelas **SQLBulkOperations** pode incluir dados long usando chamadas para **SQLParamData** e **SQLPutData**. Para obter mais informações, consulte "Fornecendo longo dados para Bulk Inserts e Updates" mais adiante, essa referência de função.  
  
 Se persistem os indicadores em cursores, o aplicativo não precisa chamar **SQLFetch** ou **SQLFetchScroll** antes de atualizar por indicadores. Ele pode usar indicadores armazenado de um cursor anterior. Se não persistem os indicadores em cursores, o aplicativo tem que chamar **SQLFetch** ou **SQLFetchScroll** para recuperar os indicadores.  
  
 O comportamento é definido pelo driver se **SQLBulkOperations**, com um *operação* argumento de SQL_UPDATE_BY_BOOKMARK, é chamado em um cursor que contém colunas duplicadas. O driver pode retornar um SQLSTATE definido pelo driver, atualizar a primeira coluna que aparece no conjunto de resultados ou realizar outro comportamento definido pelo driver.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>Executar em massa busca usando indicadores  
 Para executar buscas em massa usando indicadores com **SQLBulkOperations**, um aplicativo executa as seguintes etapas na sequência:  
  
1.  Define o atributo da instrução SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE.  
  
2.  Executa uma consulta que retorna um conjunto de resultados.  
  
3.  Define o atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas que deseja buscar.  
  
4.  Chamadas **SQLBindCol** para associar os dados que deseja buscar. Os dados serão associados a uma matriz com um tamanho igual ao valor de SQL_ATTR_ROW_ARRAY_SIZE. Ele também chama **SQLBindCol** para associar a coluna 0 (a coluna de indicador).  
  
5.  Copia os indicadores para as linhas que ele está interessado em busca na matriz associada à coluna 0. (Isso pressupõe que o aplicativo já tiver obtido indicadores separadamente).  
  
    > [!NOTE]  
    >  O tamanho da matriz apontado pelo atributo SQL_ATTR_ROW_STATUS_PTR instrução deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
6.  Chamadas **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  Se o aplicativo tiver definido o atributo da instrução SQL_ATTR_ROW_STATUS_PTR, ele pode inspecionar essa matriz para ver o resultado da operação.  
  
 Se persistem os indicadores em cursores, o aplicativo não precisa chamar **SQLFetch** ou **SQLFetchScroll** antes de buscar por indicadores. Ele pode usar indicadores armazenado de um cursor anterior. Se não persistem os indicadores em cursores, o aplicativo tem que chamar **SQLFetch** ou **SQLFetchScroll** uma vez para recuperar os indicadores.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>Executar em massa exclui usando indicadores  
 Para executar exclusões em massa usando indicadores com **SQLBulkOperations**, um aplicativo executa as seguintes etapas na sequência:  
  
1.  Define o atributo da instrução SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE.  
  
2.  Executa uma consulta que retorna um conjunto de resultados.  
  
3.  Define o atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas que deseja excluir.  
  
4.  Chamadas **SQLBindCol** para associar a coluna 0 (a coluna de indicador).  
  
5.  Copia os indicadores para as linhas se ele está interessado em Excluir para a matriz associada à coluna 0.  
  
    > [!NOTE]  
    >  O tamanho da matriz apontado pelo atributo SQL_ATTR_ROW_STATUS_PTR instrução deve ser igual a SQL_ATTR_ROW_ARRAY_SIZE ou SQL_ATTR_ROW_STATUS_PTR deve ser um ponteiro nulo.  
  
6.  Chamadas **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  Se o aplicativo tiver definido o atributo da instrução SQL_ATTR_ROW_STATUS_PTR, ele pode inspecionar essa matriz para ver o resultado da operação.  
  
 Se persistem os indicadores em cursores, o aplicativo não precisa chamar **SQLFetch** ou **SQLFetchScroll** antes da exclusão de indicadores. Ele pode usar indicadores armazenado de um cursor anterior. Se não persistem os indicadores em cursores, o aplicativo tem que chamar **SQLFetch** ou **SQLFetchScroll** uma vez para recuperar os indicadores.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>Fornecendo dados Long para atualizações e inserções em massa  
 Dados longos podem ser fornecidos para inserções em massa e atualizações executadas por chamadas para **SQLBulkOperations**. Para inserir ou atualizar dados longos, um aplicativo executa as seguintes etapas além das etapas descritas nas seções "Executar em massa insere" e "Executar em massa atualizações usando indicadores" neste tópico.  
  
1.  Quando associa os dados usando **SQLBindCol**, o aplicativo coloca um valor definido pelo aplicativo, como o número da coluna, na  *\*TargetValuePtr* buffer para dados em execução colunas. O valor pode ser usado posteriormente para identificar a coluna.  
  
     O aplicativo coloca o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro na  *\*StrLen_or_IndPtr* buffer. Se o tipo de dados SQL da coluna for SQL_LONGVARBINARY, SQL_LONGVARCHAR ou um tipo de dados específicos da fonte de dados longos e o driver retorna "Y" para o tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo**, *comprimento*  é o número de bytes de dados a serem enviados para o parâmetro; caso contrário, ele deve ser um valor não negativo e será ignorado.  
  
2.  Quando **SQLBulkOperations** é chamado, se não houver colunas de dados em execução, a função retornará SQL_NEED_DATA e prossegue para a etapa 3, que segue. (Se não houver nenhuma coluna de dados em execução, o processo é concluído.)  
  
3.  O aplicativo chama **SQLParamData** para recuperar o endereço da  *\*TargetValuePtr* buffer para a primeira coluna de dados em execução a ser processado. **SQLParamData** retornará SQL_NEED_DATA. O aplicativo recupera o valor definido pelo aplicativo do  *\*TargetValuePtr* buffer.  
  
    > [!NOTE]  
    >  Embora os parâmetros de dados em execução se parecer com colunas de dados em execução, o valor retornado por **SQLParamData** é diferente para cada um.  
  
     Colunas de dados em execução são colunas em um conjunto de linhas para o qual os dados serão enviados com **SQLPutData** quando uma linha é atualizada ou inserida com **SQLBulkOperations**. Eles são associados com **SQLBindCol**. O valor retornado por **SQLParamData** é o endereço da linha no **TargetValuePtr* buffer que está sendo processada.  
  
4.  O aplicativo chama **SQLPutData** uma ou mais vezes para enviar dados para a coluna. Mais de uma chamada é necessário se o valor de dados não pode ser retornado na  *\*TargetValuePtr* buffer especificado na **SQLPutData**; diversas chamadas para **SQLPutData** para a mesma coluna são permitidas somente quando o envio de dados de caractere C para uma coluna com um tipo específico de fonte de dados character, binary ou dados ou ao enviar dados binários de C para uma coluna com um caractere, binária, ou tipo de dados específico de fonte de dados.  
  
5.  O aplicativo chama **SQLParamData** novamente para sinalizar que todos os dados foram enviados para a coluna.  
  
    -   Se houver mais colunas de dados em execução, **SQLParamData** retorna SQL_NEED_DATA e o endereço do *TargetValuePtr* buffer para a próxima coluna de dados em execução a ser processado. O aplicativo se repete as etapas 4 e 5.  
  
    -   Se não houver nada mais colunas de dados em execução, o processo for concluído. Se a instrução foi executada com êxito, **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO; se a execução falhar, ele retornará SQL_ERROR. Neste ponto, **SQLParamData** pode retornar qualquer SQLSTATE que pode ser retornado por **SQLBulkOperations**.  
  
 Se a operação for cancelada ou ocorre um erro no **SQLParamData** ou **SQLPutData** após **SQLBulkOperations** retornará SQL_NEED_DATA e antes de dados são enviados para todos colunas de dados em execução, o aplicativo pode chamar apenas **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions** , **SQLParamData**, ou **SQLPutData** para a instrução ou a conexão associada com a instrução. Se ele chamar qualquer outra função para a instrução ou a conexão associada com a instrução, a função retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função).  
  
 Se o aplicativo chamar **SQLCancel** enquanto o driver ainda precisa de dados para colunas de dados em execução, o driver cancela a operação. O aplicativo pode, em seguida, chamar **SQLBulkOperations** novamente; o cancelamento não afeta o estado de cursor ou a posição atual do cursor.  
  
## <a name="row-status-array"></a>Matriz de status da linha  
 A matriz de status de linha contém valores de status para cada linha de dados no conjunto de linhas após uma chamada para **SQLBulkOperations**. O driver define os valores de status nessa matriz após uma chamada para **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, ou **SQLBulkOperations** . Inicialmente, essa matriz é preenchida por uma chamada para **SQLBulkOperations** se **SQLFetch** ou **SQLFetchScroll** não foi chamado antes de **SQLBulkOperations** . Essa matriz é apontada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR. O número de elementos nas matrizes de status de linha deve igual ao número de linhas no conjunto de linhas (conforme definido pelo atributo SQL_ATTR_ROW_ARRAY_SIZE instrução). Para obter informações sobre essa matriz de status de linha, consulte [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Exemplo de código  
 O exemplo a seguir busca 10 linhas de dados por vez da tabela Customers. Ele, em seguida, solicita que o usuário para uma ação tomar. Para reduzir o tráfego de rede, o buffer de exemplo atualizações, exclusões e inserções localmente as matrizes associadas, mas em deslocamentos após os dados do conjunto de linhas. Quando o usuário opta por enviar atualizações, exclusões e inserções para a fonte de dados, o código define a associação de deslocamento adequadamente e chama **SQLBulkOperations**. Para simplificar, o usuário não é possível armazenar em buffer mais de 10 atualizações, exclusões ou inserções.  
  
```  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obter um único campo de um descritor de|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Introdução a vários campos de um descritor de|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuração de um único campo de um descritor de|[Função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuração de vários campos de um descritor de|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Posicionando o cursor, a atualização de dados no conjunto de linhas, ou a atualização ou exclusão de dados no conjunto de linhas|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
