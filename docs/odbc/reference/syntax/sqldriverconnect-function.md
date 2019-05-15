---
title: Função SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 225b882a6c48900e9a15a23e4073910315848985
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537650"
---
# <a name="sqldriverconnect-function"></a>Função SQLDriverConnect
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLDriverConnect** é uma alternativa ao **SQLConnect**. Ele dá suporte a fontes de dados que exigem mais informações de conexão que três argumentos no **SQLConnect**, caixas de diálogo para solicitar ao usuário para todas as informações de conexão e as fontes de dados que não estão definidos no sistema informações.  
  
 **SQLDriverConnect** fornece os seguintes atributos de conexão:  
  
-   Estabelece uma conexão usando uma cadeia de caracteres de conexão que contém o nome da fonte de dados, uma ou mais IDs de usuário, um ou mais senhas e outras informações necessárias pela fonte de dados.  
  
-   Estabelecer uma conexão usando uma cadeia de caracteres de conexão parcial ou nenhuma informação adicional; Nesse caso, o Gerenciador de Driver e o driver podem cada avisar o usuário para obter informações de conexão.  
  
-   Estabelece uma conexão a uma fonte de dados que não está definida nas informações do sistema. Se o aplicativo fornecer uma cadeia de caracteres de conexão parcial, o driver pode avisar o usuário para obter informações de conexão.  
  
-   Estabelece uma conexão com uma fonte de dados usando uma cadeia de caracteres de conexão construída a partir de informações em um arquivo. DSN.  
  
 Depois que uma conexão é estabelecida, **SQLDriverConnect** retorna a cadeia de caracteres de conexão concluído. O aplicativo pode usar essa cadeia de caracteres para solicitações de conexão subsequentes. Para obter mais informações, consulte [conectar-se com o SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de Conexão.  
  
 *WindowHandle*  
 [Entrada] Identificador de janela. O aplicativo pode passar o identificador da janela pai, se aplicável, ou um ponteiro nulo se o identificador de janela não é aplicável ou **SQLDriverConnect** não apresentará as caixas de diálogo.  
  
 *InConnectionString*  
 [Entrada] Uma cadeia de caracteres de conexão completa (consulte a sintaxe em "Comentários"), uma cadeia de caracteres de conexão parcial ou uma cadeia de caracteres vazia.  
  
 *StringLength1*  
 [Entrada] Comprimento de **InConnectionString*, em caracteres, se a cadeia de caracteres for Unicode ou bytes se a cadeia de caracteres é o ANSI ou DBCS.  
  
 *OutConnectionString*  
 [Saída] Ponteiro para um buffer para a cadeia de caracteres de conexão concluído. Após a conexão bem-sucedida à fonte de dados de destino, esse buffer contém a cadeia de conexão concluído. Aplicativos devem alocar pelo menos 1.024 caracteres para esse buffer.  
  
 Se *OutConnectionString* for NULL, *StringLength2Ptr* ainda retornará o número total de caracteres (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontada por *OutConnectionString*.  
  
 *BufferLength*  
 [Entrada] Comprimento do **OutConnectionString* buffer em caracteres.  
  
 *StringLength2Ptr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (exceto o caractere nulo de terminação) disponíveis para retornar na \* *OutConnectionString*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *BufferLength*, a concluir a cadeia de caracteres de conexão no \* *OutConnectionString* será truncado para  *BufferLength* menos o comprimento de um caractere nulo de terminação.  
  
 *DriverCompletion*  
 [Entrada] Sinalizador que indica se o Gerenciador de Driver ou o driver deve solicitar para obter mais informações de conexão:  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED ou SQL_DRIVER_NOPROMPT.  
  
 (Para obter mais informações, consulte "Comentários".)  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE ou SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLDriverConnect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *fHandleType*SQL_HANDLE_DBC e uma *hHandle* dos *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDriverConnect** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *OutConnectionString* não era grande o suficiente para retornar a cadeia de conexão inteira, portanto, a cadeia de caracteres de conexão foi truncada. O comprimento da cadeia de caracteres de conexão completo será retornado no **StringLength2Ptr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S00|Atributo de cadeia de caracteres de conexão inválido|Uma palavra-chave de atributo inválido foi especificada na cadeia de conexão (*InConnectionString*), mas o driver não conseguiu se conectar à fonte de dados, mesmo assim. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|O driver não oferecia suporte para o valor especificado apontado para o *ValuePtr* argumento na **SQLSetConnectAttr** e substituído, um valor semelhante. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S08|Erro ao salvar DSN de arquivo|A cadeia de caracteres em  *\*InConnectionString* continha um **FILEDSN** palavra-chave, mas o arquivo. DSN não foi salvo. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S09|Palavra-chave inválida|(DM) a cadeia de caracteres em  *\*InConnectionString* continha um **SAVEFILE** palavra-chave, mas não uma **DRIVER** ou uma **FILEDSN** palavra-chave. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08001|Não é possível estabelecer conexão de cliente|O driver não pôde estabelecer uma conexão com a fonte de dados.|  
|08002|Nome da Conexão em uso|(DM) especificado *ConnectionHandle* já foi usado para estabelecer uma conexão com uma fonte de dados e a conexão foi aberta.|  
|08004|O servidor recusou a conexão|A fonte de dados rejeitados o estabelecimento da conexão por motivos de implementação definida.|  
|08S01|Falha de link de comunicação|Falha de link de comunicação entre o driver e a fonte de dados ao qual o driver estava tentando conectar-se antes do **SQLDriverConnect** processamento da função foi concluída.|  
|28000|Especificação de autorização inválida|O identificador de usuário ou a cadeia de caracteres de autorização ou ambos, conforme especificado na cadeia de conexão (*InConnectionString*), violou as restrições definidas pela fonte de dados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*szMessageText* buffer descreve o erro e sua causa.|  
|HY000|Erro geral: Dsn de arquivo inválido|(DM) a cadeia de caracteres no **InConnectionString* continha uma palavra-chave FILEDSN, mas o nome do arquivo. DSN não foi encontrado.|  
|HY000|Erro geral: Não é possível criar o buffer de arquivo|(DM) a cadeia de caracteres no **InConnectionString* continha uma palavra-chave FILEDSN, mas o arquivo. DSN esteja ilegível.|  
|HY001|Erro de alocação de memória|O Gerenciador de Driver não pôde alocar a memória necessária para dar suporte à execução ou conclusão do **SQLDriverConnect** função.<br /><br /> O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *ConnectionHandle*. A função foi chamada e antes ele concluiu a execução, o [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) foi chamado na *ConnectionHandle*e, em seguida, o **SQLDriverConnect** função foi chamada novamente sobre o *ConnectionHandle*.<br /><br /> Ou, o **SQLDriverConnect** função foi chamada e antes ele concluiu a execução, **SQLCancelHandle** foi chamado no *ConnectionHandle* de um thread diferente em um aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) outra função de execução assíncrona (não **SQLDriverConnect**) foi chamado para o *ConnectionHandle* e ainda estava em execução quando o **SQLDriverConnect** a função foi chamada.|  
|HY013|Erro de gerenciamento de memória|O **SQLDriverConnect** chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *StringLength1* era menor que 0 e não era igual a SQL_NTS.<br /><br /> (DM) o valor especificado para o argumento *BufferLength* foi menor que 0.|  
|HY092|Identificador de atributo/opção inválido|(DM) a *DriverCompletion* argumento era SQL_DRIVER_PROMPT e o *WindowHandle* argumento é um ponteiro nulo.|  
|HY110|Conclusão de driver inválida|(DM) o valor especificado para o argumento *DriverCompletion* não era igual a SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED ou SQL_DRIVER_NOPROMPT.<br /><br /> (DM) pool de Conexão foi habilitado e o valor especificado para o argumento *DriverCompletion* não era igual como SQL_DRIVER_NOPROMPT.|  
|HYC00|Recurso opcional não implementado|O driver não dá suporte à versão de comportamento do ODBC que o aplicativo solicitou.|  
|HYT00|Tempo limite esgotado|O período de tempo limite de logon expirou antes da conexão à fonte de dados concluída. O período de tempo limite é definido por meio **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|(DM) o driver correspondente ao nome de fonte de dados especificado não oferece suporte para a função.|  
|IM002|Fonte de dados não encontrado e nenhum driver padrão especificado|Nome especificado na cadeia de conexão da fonte de dados (DM) (*InConnectionString*) não foi encontrada nas informações do sistema e não havia nenhuma especificação de driver padrão.<br /><br /> (DM) não foi possível encontrar informações de driver ODBC dados origem e padrão nas informações do sistema.|  
|IM003|Não foi possível carregar o driver especificado|(DM), o driver listado na especificação de fonte de dados nas informações do sistema ou especificado pelo **DRIVER** palavra-chave não foi encontrado ou não pôde ser carregado por algum outro motivo.|  
|IM004|Motorista **SQLAllocHandle** em SQL_HANDLE_ENV falhou|(DM) durante **SQLDriverConnect**, o Gerenciador de Driver chamado do driver **SQLAllocHandle** funcionar com um *fHandleType* de SQL_HANDLE_ENV e o driver retornou um erro.|  
|IM005|Motorista **SQLAllocHandle** em SQL_HANDLE_DBC falhou.|(DM) durante **SQLDriverConnect**, o Gerenciador de Driver chamado do driver **SQLAllocHandle** funcionar com um *fHandleType* de SQL_HANDLE_DBC e o driver retornou um erro.|  
|IM006|Motorista **SQLSetConnectAttr** falhou|(DM) durante **SQLDriverConnect**, o Gerenciador de Driver chamado do driver **SQLSetConnectAttr** função e o driver retornaram um erro.|  
|IM007|Nenhuma fonte de dados ou driver especificado. caixa de diálogo proibida|Nenhum nome de fonte de dados ou o driver foi especificado na cadeia de conexão, e *DriverCompletion* foi SQL_DRIVER_NOPROMPT.|  
|IM008|Caixa de diálogo falhada|O driver tentou exibir sua caixa de diálogo de logon e falha.<br /><br /> *WindowHandle* é um ponteiro nulo, e *DriverCompletion* não era SQL_DRIVER_NO_PROMPT.|  
|IM009|Não é possível carregar a DLL de conversão|O driver não pôde carregar a DLL que foi especificado para a fonte de dados ou para a conexão de tradução.|  
|IM010|Nome de fonte de dados muito longo|(DM) o valor do atributo para a palavra-chave DSN era maior do que SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nome do driver muito longo|Valor de atributo (DM) para o **DRIVER** palavra-chave foi maior que 255 caracteres.|  
|IM012|Erro de sintaxe de palavra-chave DRIVER|Emparelhar de palavra-chave-valor (DM) para o **DRIVER** palavra-chave continha um erro de sintaxe.<br /><br /> (DM) a cadeia de caracteres em  *\*InConnectionString* continha um **FILEDSN** palavra-chave, mas o arquivo. DSN não continha um **DRIVER** palavra-chave ou um  **DSN** palavra-chave.|  
|IM014|O DSN especificado contém uma incompatibilidade de arquitetura entre o Driver e o aplicativo|Aplicativo de 32 bits (DM) usa um DSN que se conectar a um driver de 64 bits. ou vice-versa.|  
|IM015|Falha SQLDriverConnect do driver em SQL_HANDLE_DBC_INFO_HANDLE|Se um driver retornará SQL_ERROR, o Gerenciador de Driver retornará SQL_ERROR ao aplicativo e a conexão falhará.<br /><br /> Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento de Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
|S1118|Driver não oferece suporte a notificação assíncrona|Quando o driver não oferece suporte a notificação assíncrona, é possível definir SQL_ATTR_ASYNC_DBC_EVENT ou SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentários  
 Uma cadeia de caracteres de conexão tem a seguinte sintaxe:  
  
 *connection-string* ::= *empty-string*[;] &#124; *attribute*[;] &#124; *attribute*; *connection-string*  
  
 *empty-string* ::=*attribute* ::= *attribute-keyword*=*attribute-value* &#124; DRIVER=[{]*attribute-value*[}]  
  
 *attribute-keyword* ::= DSN &#124; UID &#124; PWD &#124; *driver-defined-attribute-keyword*  
  
 *attribute-value* ::= *character-string*  
  
 *driver-defined-attribute-keyword* ::= *identifier*  
  
 em que *cadeia de caracteres* tem zero ou mais caracteres; *identificador* tem um ou mais caracteres; *palavra-chave de atributo* não diferencia maiusculas de minúsculas; *valor de atributo* podem diferenciar maiusculas de minúsculas; e o valor da **DSN** palavra-chave não ser formado apenas por espaços em branco.  
  
 Devido à conexão cadeia de caracteres e inicialização de gramática, palavras-chave e atributo de valores do arquivo que contenha os caracteres **[]{}(),? \*=! @** não incluídos com as chaves devem ser evitadas. O valor de **DSN** palavra-chave não pode consistir apenas de espaços em branco e não deve conter espaços em branco à esquerda. Devido a gramática de informações do sistema, nomes de fonte de dados e palavras-chave não podem conter uma barra invertida (\\) caracteres.  
  
 Aplicativos não é necessário adicionar chaves ao redor do valor do atributo após o **DRIVER** palavra-chave, a menos que o atributo contém um ponto e vírgula (;), caso em que as chaves são necessárias. Se o valor do atributo que o driver recebe inclui chaves, o driver não deverá removê-los, mas eles devem ser parte da cadeia de conexão retornado.  
  
 Um valor de cadeia de caracteres DSN ou conexão colocado entre chaves ({}) que contém os caracteres **[]{}(),? \*=! @** é passado intactas para o driver. No entanto, ao usar esses caracteres em uma palavra-chave, o Gerenciador de Driver retornará um erro ao trabalhar com DSNs de arquivos, mas passa a cadeia de caracteres de conexão para o driver para cadeias de caracteres de conexão regulares. Evite usar chaves inseridas em um valor de palavra-chave.  
  
 A cadeia de caracteres de conexão pode incluir qualquer número de palavras-chave definidos pelo driver. Porque o **DRIVER** palavra-chave não usa as informações das informações do sistema, o driver deve definir palavras-chave suficientes para que um driver pode se conectar a uma fonte de dados usando apenas as informações na cadeia de conexão. (Para obter mais informações, consulte "Diretrizes de Driver", posteriormente nesta seção.) O driver define quais palavras-chave é necessárias para se conectar à fonte de dados.  
  
 A tabela a seguir descreve os valores de atributo de **DSN**, **FILEDSN**, **DRIVER**, **UID**, **PWD**, e **SAVEFILE** palavras-chave.  
  
|Palavra-chave|Descrição do valor de atributo|  
|-------------|---------------------------------|  
|**DSN**|Nome de uma fonte de dados, conforme retornado por **SQLDataSources** ou a caixa de diálogo de fontes de dados de **SQLDriverConnect**.|  
|**FILEDSN**|Nome de um arquivo. DSN do qual uma cadeia de caracteres de conexão será criada para a fonte de dados. Essas fontes de dados são chamadas de fontes de dados de arquivo.|  
|**DRIVER**|Descrição do driver como retornado pela **SQLDrivers** função. Por exemplo, Rdb ou SQL Server.|  
|**UID**|Uma ID de usuário.|  
|**PWD**|A senha correspondente para a ID de usuário ou uma cadeia de caracteres vazia se não houver nenhuma senha para a ID de usuário (PWD =;).|  
|**SAVEFILE**|O nome do arquivo de um arquivo. DSN no qual os valores de atributo de palavras-chave usadas para fazer a conexão bem-sucedida, presente devem ser salvo.|  
  
 Para obter informações sobre como um aplicativo escolhe uma fonte de dados ou driver, consulte [escolhendo uma fonte de dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se quaisquer palavras-chave é repetidos na cadeia de conexão, o driver usa o valor associado com a primeira ocorrência da palavra-chave. Se o **DSN** e **DRIVER** palavras-chave são incluídas na mesma cadeia de conexão, o Gerenciador de Driver e o driver usam qualquer palavra-chave aparece primeiro.  
  
 O **FILEDSN** e **DSN** palavras-chave são mutuamente exclusivas: qualquer palavra-chave aparece primeiro é usado e que é exibida a segunda é ignorado. O **FILEDSN** e **DRIVER** palavras-chave, por outro lado, não são mutuamente exclusivas. Se qualquer palavra-chave aparece em uma cadeia de caracteres de conexão com **FILEDSN**, em seguida, o valor do atributo a palavra-chave na cadeia de conexão é usado em vez do valor de atributo da mesma palavra-chave no arquivo. DSN.  
  
 Se o **FILEDSN** palavra-chave é usada, as palavras-chave especificadas em um arquivo. DSN são usadas para criar uma cadeia de caracteres de conexão. (Para obter mais informações, consulte "Arquivo de fontes de dados," nesta seção.) O **UID** palavra-chave é opcional; um arquivo. DSN pode ser criado apenas com o **DRIVER** palavra-chave. O **PWD** palavra-chave não é armazenado em um arquivo. DSN. O diretório padrão para salvar e carregar um arquivo. DSN será uma combinação do caminho especificado por **CommonFileDir** hkey_local_machine\software\microsoft\. Windows\CurrentVersion e "ODBC\DataSources". (Se CommonFileDir "C:\Program Files\Common Files", o diretório padrão seria "C:\Program programas\Arquivos Comuns\odbc\fontes".)  
  
> [!NOTE]  
>  Um arquivo. DSN pode ser manipulado diretamente, chamando o [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) e [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) funções na DLL do instalador.  
  
 Se o **SAVEFILE** palavra-chave é usada, os valores de atributo de palavras-chave usadas para fazer a conexão bem-sucedida, presente serão salvo como um arquivo. DSN com o nome do valor do atributo a **SAVEFILE** palavra-chave. O **SAVEFILE** palavra-chave deve ser usada em conjunto com o **DRIVER** palavra-chave, o **FILEDSN** palavra-chave, ou ambos, ou a função retornará SQL_SUCCESS_WITH_INFO com SQLSTATE 01S09 (palavra-chave inválida). O **SAVEFILE** palavra-chave deve aparecer antes de **DRIVER** palavra-chave na cadeia de conexão, ou os resultados serão indefinido.  
  
## <a name="driver-manager-guidelines"></a>Diretrizes do Gerenciador de driver  
 O Gerenciador de Driver constrói uma cadeia de caracteres de conexão para passar para o driver na *InConnectionString* argumento do driver **SQLDriverConnect** função. O Gerenciador de Driver não modifica o *InConnectionString* argumento passado para ele pelo aplicativo.  
  
 A ação do Gerenciador de Driver é com base no valor da *DriverCompletion* argumento:  
  
-   SQL_DRIVER_PROMPT: Se a cadeia de caracteres de conexão não contém o **DRIVER**, **DSN**, ou **FILEDSN** palavra-chave, o Gerenciador de Driver exibe a caixa de diálogo de fontes de dados. Ele constrói uma cadeia de caracteres de conexão de nome de fonte de dados retornado pela caixa de diálogo e quaisquer outras palavras-chave passado para ele pelo aplicativo. Se o nome da fonte de dados retornado pela caixa de diálogo estiver vazio, o Gerenciador de Driver Especifica o par de valor de palavra-chave DSN = padrão. (Essa caixa de diálogo não exibirá a uma fonte de dados com o nome "Padrão".)  
  
-   SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED: Se a cadeia de caracteres de conexão especificada pelo aplicativo inclui o **DSN** palavra-chave, o Gerenciador de Driver copia a cadeia de caracteres de conexão especificada pelo aplicativo. Caso contrário, ele usa as mesmas ações como faz quando *DriverCompletion* é SQL_DRIVER_PROMPT.  
  
-   SQL_DRIVER_NOPROMPT: O Gerenciador de Driver copia a cadeia de caracteres de conexão especificada pelo aplicativo.  
  
 Se a cadeia de conexão especificada pelo aplicativo contiver a **DRIVER** palavra-chave, o Gerenciador de Driver copia a cadeia de caracteres de conexão especificada pelo aplicativo.  
  
 Usando a cadeia de caracteres de conexão que ele foi construído, o Gerenciador de Driver determina qual driver a ser usado, se conecta a esse driver e passa a cadeia de caracteres de conexão que ele foi criado para o driver; Para obter mais informações sobre a interação do Gerenciador de Driver e o driver, consulte a seção "Comentários" em [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Se a cadeia de caracteres de conexão não contém o **DRIVER** palavra-chave, o Gerenciador de Driver determina qual driver a ser usado da seguinte maneira:  
  
1.  Se a cadeia de conexão contém o **DSN** palavra-chave, o Gerenciador de Driver recupera o driver associado à fonte de dados de informações do sistema.  
  
2.  Se a cadeia de caracteres de conexão não contém o **DSN** palavra-chave ou a fonte de dados não for encontrada, o Gerenciador de Driver recupera o driver associado com a fonte de dados padrão de informações do sistema. (Para obter mais informações, consulte [subchave padrão](../../../odbc/reference/install/default-subkey.md).) O Gerenciador de Driver altera o valor da **DSN** palavra-chave na cadeia de conexão como "DEFAULT".  
  
3.  Se o **DSN** palavra-chave na cadeia de conexão é definido como "DEFAULT", o Gerenciador de Driver recupera o driver associado com a fonte de dados padrão de informações do sistema.  
  
4.  Se a fonte de dados não for encontrada e a fonte de dados padrão não for encontrada, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE IM002 (fonte de dados não encontrado e nenhum driver padrão especificado).  
  
## <a name="file-data-sources"></a>Fontes de dados do arquivo  
 Se a cadeia de caracteres de conexão especificado pelo aplicativo na chamada para **SQLDriverConnect** contém o **FILEDSN** palavra-chave e essa palavra-chave não é substituída por qualquer um de **DSN**ou **DRIVER** palavra-chave e, em seguida, o Gerenciador de Driver cria uma cadeia de caracteres de conexão usando as informações no arquivo. DSN e o *InConnectionString* argumento. O Gerenciador de Driver procede da seguinte maneira:  
  
1.  Verifica se o nome do arquivo do arquivo. DSN é válido. Se não, ele retornará SQL_ERROR com SQLSTATE IM014 (nome inválido do DSN de arquivo). Se o nome do arquivo é uma cadeia de caracteres vazia ("") e SQL_DRIVER_NOPROMPT não for especificado, o **abertura de arquivo** caixa de diálogo é exibida. Se o nome do arquivo contém um caminho válido, mas nenhum nome de arquivo ou um nome de arquivo inválido e SQL_DRIVER_NOPROMPT não for especificado, o **abertura de arquivo** caixa de diálogo é exibida com o diretório atual definido para aquele especificado no nome do arquivo. Se o nome do arquivo é uma cadeia de caracteres vazia ("") ou o nome do arquivo contém um caminho válido, mas nenhum nome de arquivo ou um nome de arquivo inválido e SQL_DRIVER_NOPROMPT é especificado, e SQL_ERROR será retornado com SQLSTATE IM014 (nome inválido do DSN de arquivo).  
  
2.  Lê todas as palavras-chave na seção [ODBC] do arquivo. DSN. Se o **DRIVER** palavra-chave não estiver presente, ela retornará SQL_ERROR com SQLSTATE IM012 (erro de sintaxe de palavra-chave do Driver), exceto onde o arquivo. DSN é não compartilhável e, portanto, contém somente os **DSN** palavra-chave.  
  
     Se a fonte de dados de arquivos for não compartilhável, o Gerenciador de Driver lê o valor da **DSN** palavra-chave e conecta-se conforme o necessário para a fonte de dados de usuário ou sistema apontada pela fonte de dados de arquivo não compartilhável. As etapas 3 a 5 não são executadas.  
  
3.  Constrói uma cadeia de caracteres de conexão para o driver. A cadeia de caracteres de conexão do driver é a união entre as palavras-chave especificadas no arquivo. DSN e aquelas especificadas na cadeia de conexão do aplicativo original. Regras para a construção da cadeia de caracteres de conexão de driver em que as palavras-chave se sobrepõem são da seguinte maneira:  
  
    -   Se o **DRIVER** palavra-chave existe na cadeia de conexão do aplicativo e os drivers especificados pelo **DRIVER** palavras-chave não são os mesmos no arquivo. DSN e a cadeia de caracteres de conexão do aplicativo, em seguida, a informações sobre o driver no arquivo. DSN é ignorada e as informações do driver na cadeia de conexão do aplicativo são usadas. Se os drivers especificados pela **DRIVER** palavra-chave são as mesmas no arquivo. DSN e cadeia de caracteres de conexão do aplicativo e, em seguida, onde todas as palavras-chave se sobrepõem, aquelas especificadas na cadeia de conexão do aplicativo têm precedência sobre aquelas especificado no arquivo. DSN.  
  
    -   Na nova cadeia de conexão, o **FILEDSN** palavra-chave é eliminado.  
  
4.  Carrega o driver examinando a entrada do registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\\< nome do Driver\>\Driver onde \<nome do Driver > for especificado o **DRIVER** palavra-chave.  
  
5.  Passa o driver a cadeia de caracteres de conexões novo.  
  
 Para obter exemplos de arquivos. DSN, consulte [conectar fontes de dados de arquivo usando](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md).  
  
## <a name="savefile-keyword"></a>Palavra-chave SAVEFILE  
 Se a cadeia de conexão especificada pelo aplicativo contiver a **SAVEFILE** palavra-chave e, em seguida, o Gerenciador de Driver salva a cadeia de caracteres de conexão em um arquivo. DSN. O Gerenciador de Driver procede da seguinte maneira:  
  
1.  Verifica se o nome do arquivo do arquivo. DSN incluído como o valor do atributo de **SAVEFILE** palavra-chave é válida. Se não, ele retornará SQL_ERROR com SQLSTATE IM014 (nome inválido do DSN de arquivo). A validade do nome do arquivo é determinada pelas regras de nomenclatura padrão do sistema. Se o nome do arquivo é uma cadeia de caracteres vazia ("") e o *DriverCompletion* argumento não for SQL_DRIVER_NOPROMPT e, em seguida, o nome do arquivo é válido. Se o nome do arquivo já existir, em seguida, se *DriverCompletion* for SQL_DRIVER_NOPROMPT, o arquivo será substituído. Se *DriverCompletion* é SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED, uma caixa de diálogo solicita que o usuário especifique se o arquivo deve ser substituído. Se não for inserido, o **salvar arquivo** caixa de diálogo é exibida.  
  
2.  Se o driver retornará SQL_SUCCESS e o nome do arquivo não era uma cadeia de caracteres vazia, o Gerenciador de Driver grava as informações de conexão retornadas na *OutConnectionString* argumento para o arquivo especificado com o formato especificado em a seção "Cadeias de Conexão" no início desta seção.  
  
3.  Se o driver retornará SQL_SUCCESS e o nome do arquivo foi uma cadeia de caracteres vazia (""), em seguida, chama o Gerenciador de Driver a **salvar arquivo** caixa de diálogo comum com o *hwnd* especificado e grava as informações de conexão retornado no *OutConnectionString* para o arquivo especificado na caixa de diálogo comum salvar arquivo com o formato especificado na seção "Cadeias de Conexão", anteriormente nesta seção.  
  
4.  Se o driver retornará SQL_SUCCESS, ele retorna o *OutConnectionString* argumento que contém a cadeia de caracteres de conexão para o aplicativo.  
  
5.  Se o driver retorna SQL_SUCCESS_WITH_INFO ou SQL_ERROR for retornado, o Gerenciador de Driver retorna o SQLSTATE para o aplicativo.  
  
## <a name="driver-guidelines"></a>Diretrizes de driver  
 O driver verificará se a cadeia de caracteres de conexão passada para ele pelo Gerenciador de Driver contém o **DSN** ou **DRIVER** palavra-chave. Se a cadeia de conexão contém o **DRIVER** palavra-chave, o driver não é possível recuperar informações sobre a fonte de dados das informações do sistema. Se a cadeia de conexão contém o **DSN** palavra-chave ou não contém o **DSN** ou o **DRIVER** palavra-chave, o driver pode recuperar informações sobre a fonte de dados a partir das informações do sistema da seguinte maneira:  
  
1.  Se a cadeia de conexão contém o **DSN** palavra-chave, o driver recupera as informações da fonte de dados especificado.  
  
2.  Se a cadeia de caracteres de conexão não contém o **DSN** palavra-chave, a fonte de dados especificado não for encontrada, ou o **DSN** palavra-chave for definido como "DEFAULT", o driver recupera as informações para a fonte de dados padrão .  
  
 O driver usa quaisquer informações que ele recupera a partir das informações do sistema para aumentar as informações passadas a ele na cadeia de conexão. Se as informações nas informações do sistema duplicarem as informações na cadeia de conexão, o driver usa as informações na cadeia de conexão.  
  
 Com base no valor de *DriverCompletion*, o driver solicita ao usuário para informações de conexão, como a ID de usuário e senha e conecta-se à fonte de dados:  
  
-   SQL_DRIVER_PROMPT: O driver exibe uma caixa de diálogo, usando os valores das informações de sistema e de cadeia de caracteres de conexão (se houver) como valores iniciais. Quando o usuário sai da caixa de diálogo, o driver se conecta à fonte de dados. Ele também constrói uma cadeia de caracteres de conexão do valor da **DSN** ou **DRIVER** palavra-chave na \* *InConnectionString* e as informações retornadas a caixa de diálogo. Ele coloca essa cadeia de conexão no **OutConnectionString* buffer.  
  
-   SQL_DRIVER_COMPLETE ou SQL_DRIVER_COMPLETE_REQUIRED: Se a cadeia de caracteres de conexão contém informações suficientes e essa informação está correta, o driver conecta-se para a fonte de dados e cópias \* *InConnectionString* à \* *OutConnectionString* . Se nenhuma informação está ausente ou incorreto, o driver usa as mesmas ações, como faz quando *DriverCompletion* é SQL_DRIVER_PROMPT, exceto que, se *DriverCompletion* é SQL_DRIVER_COMPLETE_ O driver necessário, desabilita os controles para todas as informações não são necessárias para se conectar à fonte de dados.  
  
-   SQL_DRIVER_NOPROMPT: Se a cadeia de caracteres de conexão contém informações suficientes, o driver conecta-se para a fonte de dados e cópias \* *InConnectionString* à \* *OutConnectionString*. Caso contrário, o driver retornará SQL_ERROR para **SQLDriverConnect**.  
  
 Na conexão bem-sucedida à fonte de dados, o driver também define \* *StringLength2Ptr* até o comprimento da cadeia de conexão de saída que está disponível para retornar em **OutConnectionString*.  
  
 Se o usuário cancela uma caixa de diálogo apresentada pelo Gerenciador de Driver ou o driver **SQLDriverConnect** retorne SQL_NO_DATA.  
  
 Para obter informações sobre como o Gerenciador de Driver e o driver interagem durante o processo de conexão, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Se um driver compatível com **SQLDriverConnect**, a seção de palavra-chave driver as informações do sistema para o driver deve conter o **ConnectFunctions** com o segundo caractere de palavra-chave definida para "Y".  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>Conectar-se quando o Pooling de Conexão está habilitado  
 Pooling de Conexão permite que um aplicativo para reutilizar uma conexão que já foi criado. Quando **SQLDriverConnect** é chamado, o Gerenciador de Driver tenta fazer a conexão usando uma conexão que faz parte de um pool de conexões em um ambiente que foi designado para o pool de conexão. Para obter mais informações sobre o pooling de conexão, consulte [função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Um aplicativo pode definir SQL_ATTR_RESET_CONNECTION antes de chamar SQLDisconnect uma conexão em que o pool está habilitado. Para obter mais informações, consulte [função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 As seguintes restrições se aplicam quando um aplicativo chama **SQLDriverConnect** para se conectar a uma conexão em pool:  
  
-   Nenhum pool de processamento de conexão é executada quando o **SAVEFILE** palavra-chave é especificado na cadeia de conexão.  
  
-   Se o pool de conexão é habilitado, **SQLDriverConnect** pode ser chamado apenas com um *DriverCompletion* argumento de SQL_DRIVER_NOPROMPT; se **SQLDriverConnect** é chamado com qualquer outro *DriverCompletion*, SQLSTATE HY110 (conclusão de driver inválida) será retornado.  
  
## <a name="connection-attributes"></a>Atributos de conexão  
 O atributo de conexão SQL_ATTR_LOGIN_TIMEOUT, definido usando **SQLSetConnectAttr**, define o número de segundos a aguardar uma solicitação de logon ser concluído com uma conexão bem-sucedida pelo driver antes de retornar ao aplicativo. Se o usuário é solicitado a concluir a cadeia de caracteres de conexão, um período de espera para cada solicitação de logon começa quando o driver iniciará o processo de conexão.  
  
 O driver abre a conexão no modo de acesso SQL_MODE_READ_WRITE por padrão. Para definir o modo de acesso para SQL_MODE_READ_ONLY, o aplicativo deve chamar **SQLSetConnectAttr** com o atributo SQL_ATTR_ACCESS_MODE antes de chamar **SQLDriverConnect**.  
  
 Se uma biblioteca de conversão padrão for especificada nas informações do sistema da fonte de dados, o driver carrega. Uma biblioteca de conversão diferentes pode ser carregada chamando **SQLSetConnectAttr** com o atributo SQL_ATTR_TRANSLATE_LIB. Uma opção de conversão pode ser especificada chamando **SQLSetConnectAttr** com a opção SQL_ATTR_TRANSLATE_OPTION.  
  
 Para obter mais informações, consulte [conectar-se com o SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
```cpp  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {                 
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 Consulte também [programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Descobrir e enumerar os valores necessários para se conectar a uma fonte de dados|[Função SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectando-se a uma fonte de dados|[Função SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Desconectando de uma fonte de dados|[Função SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Retornando atributos e descrições de driver|[Função SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberando um identificador|[Função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Definir um atributo de conexão|[Função SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
