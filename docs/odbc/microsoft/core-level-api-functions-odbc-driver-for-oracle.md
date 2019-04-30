---
title: Principais funções de nível de API (Driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2ada1011096eb8275f9059e531cfc0fcc1af58c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232645"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Funções de API de nível do núcleo (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Funções nesse nível compõem o nível mínimo de conformidade de interface para drivers ODBC.  
  
|Função de API|Observações|  
|------------------|-----------|  
|**SQLAllocConnect**|Aloca memória para um identificador de conexão *hdbc*, dentro do ambiente identificado pelo *henv*. O Gerenciador de Driver processa esta chamada e chama o driver **SQLAllocConnect** funcionar sempre que **SQLConnect**, **SQLBrowseConnect**, ou  **SQLDriverConnect** é chamado.|  
|**SQLAllocEnv**|Exibe uma caixa de diálogo especificando o requisito para o software cliente Oracle e, em seguida, retorna SQL_NULL_HANDLE. Se o software cliente Oracle não estiver instalado, essa função aloca memória para um identificador de ambiente *henv*e inicializa a interface de nível de chamada ODBC para uso por um aplicativo.|  
|**SQLAllocStmt**|Aloca memória para um identificador de instrução e associa o identificador de instrução com a conexão especificada pelo hdbc. O Gerenciador de Driver passa essa chamada para o driver, que aloca a memória para a estrutura hstmt.|  
|**SQLBindCol**|Atribui o espaço de armazenamento para uma coluna de resultados e especifica o tipo do resultado.|  
|**SQLCancel**|Cancela o processamento em um identificador de instrução, hstmt. Em alguns casos, o Oracle não permite o cancelamento de uma instrução em execução. Isso significa que uma instrução em execução continuará até que Oracle conclui o processo, momento em que os resultados das instruções são cancelados pelo Driver ODBC para Oracle.|  
|**SQLColAttributes**|Retorna informações de descritor para uma coluna em um conjunto de resultados. Informações do descritor são retornadas como uma cadeia de caracteres, um valor de descritor dependente de 32 bits ou um valor inteiro.|  
|**SQLConnect**|Conecta-se a fonte de dados. Para usar a autenticação do sistema operacional Oracle, especifique "/" como o *szUID* parâmetro e "" como o *szAuthStr* parâmetro.|  
|**SQLDescribeCol**|Retorna o nome, tipo, precisão, escala e nulidade da coluna de resultados fornecido. **Observação:  SQLDescribeCol** relata colunas calculadas como SQL_VARCHAR.|  
|**SQLDisconnect**|Fecha uma conexão. Se o pool de conexão está habilitado para um ambiente compartilhado e um aplicativo chama **SQLDisconnect** em uma conexão nesse ambiente, a conexão é retornada ao pool de conexão e ainda está disponível para outros componentes usando o mesmo ambiente compartilhado.|  
|**SQLError**|Retorna informações de erro ou de status sobre o último erro. O driver mantém uma pilha ou a lista de erros que podem ser retornadas para o *hstmt*, *hdbc*, e *henv* argumentos, dependendo de como a chamada para **SQLError**  é feita. A fila de erros é liberada após cada instrução. Normalmente, recupera uma mensagem de erro do Oracle e, caso contrário, está vazia.|  
|**SQLExecDirect**|Executa uma instrução SQL nova e não preparada. O driver usa os valores atuais das variáveis de marcador de parâmetro se há quaisquer parâmetros na instrução. Se sua tabela, exibição ou nomes de campo contiverem espaços, coloque os nomes de aspas em volta marcas. Por exemplo, se seu banco de dados contém uma tabela chamada *My Table* e o campo *Meu campo*, coloque cada elemento do identificador da seguinte forma:<br /><br /> Selecione \`minha tabela\`. \`Meu campo1\`, \`Minha tabela\`.\` Meu Field2\` FROM \`minha tabela '|  
|**SQLExecute**|Executa uma instrução SQL preparada (uma instrução já foi preparada pela **SQLPrepare**). O driver usa os valores atuais das variáveis de marcador de parâmetro se há quaisquer parâmetros na instrução.|  
|**SQLFetch**|Recupera uma linha de um conjunto de resultados em locais especificados pelas chamadas anteriores ao **SQLBindCol**. Prepara o driver para uma chamada para **SQLGetData** para as colunas não associadas.|  
|**SQLFreeConnect**|Libera um identificador de conexão e libera toda a memória alocada para o identificador.|  
|**SQLFreeEnv**|Fecha o Driver ODBC para Oracle e libera toda memória associada com o driver.|  
|**SQLFreeStmt**|Interrompe o processamento associado a um hstmt específico, fechará quaisquer cursores abertos associados a hstmt, descartará resultados pendentes e, opcionalmente, libera todos os recursos associados com o identificador de instrução.|  
|**SQLGetCursorName**|Retorna o nome do cursor associado a determinado hstmt.|  
|**SQLNumResultCols**|Retorna o número de colunas em um cursor de conjunto de resultados.|  
|**SQLPrepare**|Prepara uma instrução SQL, como planejar a otimizar e execute a instrução. A instrução SQL é compilada para execução pelo **SQLExecDirect**.<br /><br /> Se sua tabela, exibição ou nomes de campo contiverem espaços, coloque os nomes de aspas em volta marcas. Por exemplo, se seu banco de dados contém uma tabela chamada *My Table* e o campo *Meu campo*, coloque cada elemento do identificador da seguinte maneira:<br /><br /> Selecione \`minha tabela\`.\` Meu campo\` FROM \`minha tabela '<br /><br /> Para obter informações sobre como usar conjuntos de resultados que contêm matrizes como parâmetros formais, consulte [retornando parâmetros da matriz de procedimentos armazenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle não fornece uma maneira de determinar o número de linhas em um resultado definido até depois de você busca a última linha, portanto, ele retornará -1.|  
|**SQLSetCursorName**|Associa um nome de cursor com um identificador de instrução ativa *hstmt*.|  
|**SQLSetParam**|Substituído por SQLBindParameter no ODBC 2. *x*.|  
|**SQLTransact**|Solicita uma operação de confirmação ou reversão para todas as operações ativas em todos os identificadores de instrução (hstmts) associados a uma conexão ou para todas as conexões associadas com o identificador de ambiente *henv*. Se uma confirmação falhar no modo manual, a transação permanecerá ativa; Você pode escolher reverter a transação ou repita a operação de confirmação. Se uma operação de confirmação falhar no modo de transação automática, a transação é revertida automaticamente. a transação não pode ficar inativa.|
