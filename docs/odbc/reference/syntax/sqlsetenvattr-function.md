---
title: Função SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09e5483bd5d1a1e2cb7398ee73d456c46439893f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536295"
---
# <a name="sqlsetenvattr-function"></a>Função SQLSetEnvAttr
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLSetEnvAttr** define os atributos que controlam aspectos de ambientes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] Identificador de ambiente.  
  
 *Atributo*  
 [Entrada] Atributo a ser definido, listados em "Comentários".  
  
 *ValuePtr*  
 [Entrada] Ponteiro para o valor a ser associado aos *atributo*. Dependendo do valor de *atributo*, *ValuePtr* será um valor inteiro de 32 bits ou apontar para uma cadeia de caracteres terminada em nulo.  
  
 *StringLength*  
 [Entrada] Se *ValuePtr* aponta para uma cadeia de caracteres ou um buffer de binário, este argumento deve ser o comprimento de **ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se *ValuePtr* é um inteiro *StringLength* será ignorado.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLSetEnvAttr** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_ENV e uma *manipular* dos *EnvironmentHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetEnvAttr** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário. Se um driver não oferece suporte a um atributo de ambiente, o erro pode ser retornado somente durante o tempo de conexão.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|O driver não oferecia suporte para o valor especificado na *ValuePtr* e substituído, um valor semelhante. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY009|Uso inválido de ponteiro nulo|O argumento de atributo identificado um atributo de ambiente que é necessário um valor de cadeia de caracteres, e o *ValuePtr* argumento é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) foi alocado em um identificador de conexão *EnvironmentHandle*.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** não tiver sido definida com **SQLSetEnvAttr** e *atributo* não é igual a **SQL_ATTR_ODBC_VERSION**. Não é necessário definir **SQL_ATTR_ODBC_VERSION** explicitamente se você estiver usando **SQLAllocHandleStd**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY024|Valor de atributo inválido|Dado especificado *atributo* valor, um valor inválido foi especificado na *ValuePtr*.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|O *StringLength* argumento era menor que 0 mas não estavam SQL_NTS.|  
|HY092|Identificador de atributo/opção inválido|(DM) o valor especificado para o argumento *atributo* não era válido para a versão do ODBC com suporte pelo driver.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O valor especificado para o argumento *atributo* foi um atributo de ambiente ODBC válido para a versão do ODBC com suporte pelo driver, mas não tinha suporte pelo driver.<br /><br /> (DM) a *atributo* argumento era SQL_ATTR_OUTPUT_NTS, e *ValuePtr* foi SQL_FALSE.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLSetEnvAttr** somente se nenhum identificador de conexão é alocado no ambiente. Todos os atributos de ambiente definidos com êxito pelo aplicativo para o ambiente persistem até **SQLFreeHandle** é chamado no ambiente. Mais de um identificador de ambiente pode ser alocado simultaneamente em ODBC 3 *. x*.  
  
 O formato das informações definida por meio *ValuePtr* depende especificado *atributo*. **SQLSetEnvAttr** aceitará as informações de atributo em um dos dois formatos diferentes: uma cadeia de caracteres terminada em nulo ou um valor inteiro de 32 bits. O formato de cada um é indicado na descrição do atributo.  
  
 Não há nenhum atributo de ambiente específicas do driver.  
  
 Atributos de Conexão não podem ser definidos por uma chamada para **SQLSetEnvAttr**. Tentar fazer isso retornará SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
|*Atributo*|*ValuePtr* conteúdo|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|Um valor SQLUINTEGER de 32 bits que habilita ou desabilita o pooling de conexão no nível do ambiente. Os seguintes valores são usados:<br /><br /> SQL_CP_OFF = Conexão do pool está desativado. Esse é o padrão.<br /><br /> SQL_CP_ONE_PER_DRIVER = um único pool de conexão tem suporte para cada driver. Cada conexão em um pool é associado um driver.<br /><br /> SQL_CP_ONE_PER_HENV = um único pool de conexão tem suporte para cada ambiente. Cada conexão em um pool é associado um ambiente.<br /><br /> SQL_CP_DRIVER_AWARE = usar o recurso de reconhecimento de pool de conexão do driver, se ele estiver disponível. Se o driver não oferece suporte a reconhecimento de pool de conexão, SQL_CP_DRIVER_AWARE será ignorado e SQL_CP_ONE_PER_HENV é usado. Para obter mais informações, consulte [Pooling de Conexão de reconhecimento de Driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md). Em um ambiente em que alguns drivers de suportam e alguns drivers não dão suporte a reconhecimento de pool de conexão, SQL_CP_DRIVER_AWARE pode habilitar o recurso de reconhecimento de pool de conexão naqueles que dão suporte a drivers, mas é equivalente à configuração para SQL_CP_ONE_PER_HENV em os drivers que não dão suporte a recurso de reconhecimento de pool de conexão.<br /><br /> Pooling de Conexão está habilitado por meio da chamada **SQLSetEnvAttr** para definir o atributo SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_HENV. Essa chamada deve ser feita antes que o aplicativo aloca o ambiente de compartilhado para o qual conexão o pool deve ser habilitado. O identificador de ambiente na chamada para **SQLSetEnvAttr** é definido como null, o que torna SQL_ATTR_CONNECTION_POOLING um atributo de nível de processo. Depois que o pool de conexão estiver habilitado, o aplicativo, em seguida, aloca um ambiente compartilhado implícito chamando **SQLAllocHandle** com o *InputHandle* argumento definido como SQL_HANDLE_ENV.<br /><br /> Depois de pooling de conexão tiver sido habilitado e um ambiente compartilhado foi selecionado para um aplicativo, SQL_ATTR_CONNECTION_POOLING não pode ser redefinido para esse ambiente, pois **SQLSetEnvAttr** é chamado com um ambiente de nulo identificador ao definir este atributo. Se esse atributo for definido, enquanto o pooling de conexão já está habilitado em um ambiente compartilhado, o atributo afeta somente os ambientes compartilhados que são alocados subsequentemente.<br /><br /> Também é possível habilitar o pool de conexão em um ambiente. Observe o seguinte sobre o pooling de conexão do ambiente:<br /><br /> -Habilitar conexão do pool em um identificador de NULL é um atributo de nível de processo. Ambientes subsequentemente alocados serão um ambiente compartilhado e herdarão a conexão de nível de processo pooling de configuração.<br />-Depois de um ambiente é alocado, um aplicativo ainda pode alterar sua configuração de pool de conexão.<br />– Se o pool de conexão do ambiente é habilitado e usa o driver a conexão pool de driver, ambiente de pool leva a preferência.<br /><br /> SQL_ATTR_CONNECTION_POOLING é implementada dentro do Gerenciador de Driver. Um driver não precisa implementar SQL_ATTR_CONNECTION_POOLING. ODBC 2.0 e 3.0 aplicativos podem definir esse atributo de ambiente.<br /><br /> Para obter mais informações, consulte [ODBC Connection Pooling](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|Um valor SQLUINTEGER de 32 bits que determina como uma conexão é escolhido de um pool de conexão. Quando **SQLConnect** ou **SQLDriverConnect** é chamado, o Gerenciador de Driver determina qual conexão for reutilizada do pool. O Gerenciador de Driver tenta corresponder as opções de conexão na chamada e os atributos de conexão definidos pelo aplicativo para as palavras-chave e os atributos de conexão das conexões no pool. O valor desse atributo determina o nível de precisão de critérios de correspondência.<br /><br /> Os seguintes valores são usados para definir o valor desse atributo:<br /><br /> SQL_CP_STRICT_MATCH = somente as conexões que correspondam exatamente às opções de conexão na chamada e a conexão atributos definidos pelo aplicativo são reutilizados. Esse é o padrão.<br /><br /> SQL_CP_RELAXED_MATCH = conexões com correspondência de cadeia de caracteres de conexão que palavras-chave podem ser usadas. Devem corresponder a palavras-chave, mas nem todos os atributos de conexão devem corresponder.<br /><br /> Para obter mais informações sobre como o Gerenciador de Driver executa a correspondência com a conexão com uma conexão em pool, consulte [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Para obter mais informações sobre o pooling de conexão, consulte [Pooling de Conexão ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|Um inteiro de 32 bits que determina se a determinada funcionalidade exibe ODBC 2 *. x* comportamento ou o ODBC 3 *. x* comportamento. Os seguintes valores são usados para definir o valor desse atributo:<br /><br /> SQL_OV_ODBC3_80 = o Gerenciador de Driver e o comportamento de anexo a seguir ODBC 3.8 do driver:<br /><br /> -O driver retorna e espera que o ODBC 3. *x* códigos de data, hora e carimbo de hora.<br />-O driver retornará ODBC 3. *x* códigos de SQLSTATE quando **SQLError**, **SQLGetDiagField**, ou **SQLGetDiagRec** é chamado.<br />-A *CatalogName* argumento em uma chamada para **SQLTables** aceita um padrão de pesquisa.<br />-O Gerenciador de Driver dá suporte à extensibilidade do tipo de dados C. Para obter mais informações sobre as extensões de tipo de dados C, consulte [tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).<br /><br /> Para obter mais informações, consulte [o que há de novo no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).<br /><br /> SQL_OV_ODBC3 = o Gerenciador de Driver e anexo do driver de ODBC de 3 a seguir *. x* comportamento:<br /><br /> -O driver retorna e espera que o ODBC 3 *. x* códigos de data, hora e carimbo de hora.<br />-O driver retorna ODBC 3 *. x* códigos de SQLSTATE quando **SQLError**, **SQLGetDiagField**, ou **SQLGetDiagRec** é chamado.<br />-A *CatalogName* argumento em uma chamada para **SQLTables** aceita um padrão de pesquisa.<br />-O Gerenciador de Driver não oferece suporte a extensibilidade do tipo de dados C.<br /><br /> SQL_OV_ODBC2 = o Gerenciador de Driver e o anexo do driver ODBC 2 seguintes *. x* comportamento. Isso é especialmente útil para um ODBC 2 *. x* aplicativo trabalhar com um ODBC 3 *. x* driver.<br /><br /> -O driver retorna e espera que o ODBC 2 *. x* códigos de data, hora e carimbo de hora.<br />-O driver retorna 2 de ODBC *. x* códigos de SQLSTATE quando **SQLError**, **SQLGetDiagField**, ou **SQLGetDiagRec** é chamado.<br />-A *CatalogName* argumento em uma chamada para **SQLTables** não aceita um padrão de pesquisa.<br />-O Gerenciador de Driver não oferece suporte a extensibilidade do tipo de dados C.<br /><br /> Um aplicativo deve definir esse atributo de ambiente antes de chamar qualquer função que tem um argumento SQLHENV ou a chamada retornará SQLSTATE HY010 (erro de sequência de função). Ela é específica do driver existência de um comportamento adicional para esses sinalizadores ambientais.<br /><br /> -Para obter mais informações, consulte [declarando a versão do aplicativo ODBC](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [alterações comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md).|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|Um inteiro de 32 bits que determina como o driver retorna dados de cadeia de caracteres. Se SQL_TRUE, o driver retorna dados de cadeia de caracteres terminada em nulo. Se SQL_FALSE, o driver não retorna dados de cadeia de caracteres terminada em nulo.<br /><br /> Esse atributo padrão será SQL_TRUE. Uma chamada para **SQLSetEnvAttr** defini-lo como SQL_TRUE retorna SQL_SUCCESS. Uma chamada para **SQLSetEnvAttr** defini-lo como retornará SQL_FALSE SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado).|  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Retornando a configuração de um atributo de ambiente|[Função SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
