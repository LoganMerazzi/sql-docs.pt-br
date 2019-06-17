---
title: Tela 4 (Driver ODBC para SQL Server) do Assistente de fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 93145892c96d2b255dca758e7028d2884cec359b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797773"
---
# <a name="data-source-wizard-screen-4"></a>Tela 4 do Assistente de Fonte de Dados

Especifique o idioma a ser usado para mensagens do SQL Server, a tradução do conjunto de caracteres e se o driver ODBC do SQL Server deverá usar configurações regionais. Você também pode controlar o log de consultas demoradas e as configurações de estatísticas de driver.

## <a name="options"></a>Opções

### <a name="change-the-language-of-sql-server-system-messages-to"></a>Alterar o idioma das mensagens de sistema do SQL Server para

Cada instância do SQL Server pode ter vários conjuntos de mensagens de sistema, cada um deles em um idioma diferente (por exemplo, inglês, espanhol, francês etc.). Se uma fonte de dados for definida em relação a um servidor com vários conjuntos de mensagens do sistema, você poderá especificar o idioma a ser utilizado para essas mensagens. Clique no idioma na lista. Esta opção não estará disponível se só um idioma for instalado no SQL Server.

### <a name="use-strong-encryption-for-data"></a>Usar criptografia forte para dados

Quando essa opção está selecionada, os dados passados por conexões estabelecidas com o uso de DSN serão criptografados. Os logons são criptografados por padrão, até mesmo quando a caixa de seleção está desmarcada.

### <a name="trust-server-certificate"></a>Confiar em certificado do servidor

Essa opção é aplicável somente quando **usar criptografia forte para dados** está habilitado. Quando selecionada, o certificado do servidor não será validado para que o nome de host correto do servidor e ser emitido por uma autoridade de certificação confiável. 

### <a name="perform-translation-for-character-data"></a>Executar tradução de dados de caracteres

Quando essa caixa de seleção está marcada, o driver ODBC do SQL Server converte cadeias de caracteres ANSI enviadas entre o computador cliente e o SQL Server com o uso de Unicode. O driver ODBC às vezes converte entre a página de código do SQL Server e o Unicode no computador cliente. Isso requer que a página de código usada pelo SQL Server seja uma das páginas de código disponíveis no computador cliente.

Quando essa caixa de seleção está desmarcada, nenhuma tradução dos caracteres estendidos em cadeias de caracteres ANSI é feita quando eles são enviados entre o aplicativo cliente e o servidor. Se o computador cliente estiver usando uma página de código ANSI (ACP) diferente da página de código do SQL Server, os caracteres estendidos em cadeias de caracteres ANSI talvez sejam interpretados incorretamente. Se o computador cliente usando a mesma página de código desse ACP que o SQL Server está utilizando, os caracteres estendidos serão interpretados corretamente.

### <a name="use-regional-settings-when-outputting-currency-numbers-dates-and-times"></a>Usar configurações regionais na saída de moedas, números, datas e horas

Especifica que o driver usa as configurações regionais do computador cliente para formatação de moedas, números, datas e horas nas cadeias de saída de caracteres. O driver usa a configuração regional padrão da conta de logon do Windows do usuário conectado por meio da fonte de dados. Selecione esta opção para aplicativos que só exibem dados, não para aplicativos que processam dados.

### <a name="save-long-running-queries-to-the-log-file"></a>Salvar consultas demoradas no arquivo de log

Especifica que o log registra qualquer consulta que demore mais do que o valor de **tempo de consulta Demorada**. As consultas demoradas são registradas no arquivo especificado. Para especificar um arquivo de log, digite o caminho completo e o nome de arquivo na caixa ou clique em **Procurar** para selecionar um arquivo de log navegando pelos diretórios de arquivo existentes.

### <a name="long-query-time-milliseconds"></a>Tempo da consulta demorada (milissegundos)

Especifica um valor de limite, em milissegundos, para registrar uma consulta demorada. Qualquer consulta cuja execução demore mais que esse número de milissegundos será registrada.

### <a name="log-odbc-driver-statistics-to-the-log-file"></a>Registrar estatísticas de driver ODBC no arquivo de log

Especifica que as estatísticas sejam registradas. As estatísticas são registradas no arquivo especificado. Para especificar um arquivo de log, digite o caminho completo e o nome de arquivo na caixa ou clique em **Procurar** para selecionar um arquivo de log navegando pelos diretórios de arquivo existentes.

O log de estatísticas é um arquivo delimitado por tabulações que pode ser analisado no Microsoft Excel ou em qualquer aplicativo com suporte para arquivos delimitados por tabulações.

### <a name="connect-retry-count"></a>Contagem de repetições de conexão

Especifica o número de vezes para repetir uma tentativa de conexão malsucedida.

### <a name="connect-retry-interval-seconds"></a>Intervalo de repetições de conexão (segundos)

Especifica o número de segundos entre cada tentativa de repetição de conexão. Para obter mais informações sobre a operação e o **contagem de repetição do Connect** opções, consulte [resiliência de Conexão no Driver ODBC do Windows](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).

### <a name="back"></a>Voltar

Clique neste botão para voltar à página anterior do assistente.

### <a name="finish"></a>Concluir

Se as informações especificadas nesta tela forem concluídas, você poderá clicar **concluir**. O DSN é criado usando todos os atributos especificados sobre esta e outras telas do assistente e você terá a oportunidade de testar o DSN criado recentemente.

## <a name="next-steps"></a>Próximas etapas

[Tela 3 do Assistente de Fonte de Dados](../../../connect/odbc/windows/dsn-wizard-3.md)
