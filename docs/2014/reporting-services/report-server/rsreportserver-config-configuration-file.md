---
title: Arquivo de configuração RSReportServer | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 60e0a0b2-8a47-4eda-a5df-3e5e403dbdbc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1939e3b1f09e6afbc63ba0565e244e66a7cff26f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103226"
---
# <a name="rsreportserver-configuration-file"></a>RSReportServer Configuration File
  O arquivo **RsReportServer.config** armazena configurações que são usadas pelo Gerenciador de Relatórios, pelo serviço Web Servidor de Relatórios e pelo processamento em segundo plano. Todos os aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são executados dentro de um único processo que lê as configurações armazenadas no arquivo RSReportServer.config. Os servidores de relatório nos modos nativo e SharePoint usam o RSReportServer.config, porém os dois modos não usam todas as mesmas configurações do arquivo de configuração. A versão do modo do SharePoint do arquivo é menor, pois muitas das configurações do modo do SharePoint são armazenadas nos bancos de dados de configuração do SharePoint, em vez de no arquivo. Este tópico descreve o arquivo de configuração padrão instalado para o modo Nativo e o modo do SharePoint e algumas das configurações e comportamentos importantes controlados pelo arquivo de configuração.  
  
 No modo do SharePoint, o arquivo de configuração contém as configurações que se aplicam a todas as instâncias do aplicativo de serviço em execução nesse computador. O banco de dados de configuração do SharePoint contém definições de configuração que se aplicam a aplicativos de serviço específicos. As configurações armazenadas no banco de dados Configuração e gerenciadas por meio das páginas de gerenciamento do SharePoint podem ser diferentes para cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 As configurações são apresentadas no conteúdo a seguir, na ordem em que aparecem no arquivo de configuração instalado por padrão. Para obter instruções sobre como editar esse arquivo, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
 **Neste tópico:**  
  
-   [Local do arquivo](#bkmk_file_location)  
  
-   [Configurações gerais (rsreportserver. config)](#bkmk_generalconfiguration)  
  
-   [URLReservations (arquivo rsreportserver. config)](#bkmk_URLReservations)  
  
-   [Autenticação (arquivo rsreportserver. config)](#bkmk_Authentication)  
  
-   [Serviço (arquivo rsreportserver. config)](#bkmk_service)  
  
-   [Configuração geral de extensões de entrega de interface do usuário](#bkmk_ui)  
  
-   [Extensões (arquivo rsreportserver. config) no modo nativo](#bkmk_extensions)  
  
    -   [Configuração geral de extensões de entrega](#bkmk_extensionsgeneral)  
  
        -   [Configurações de configuração de extensão de entrega de compartilhamento de arquivo](#bkmk_fileshare_extension)  
  
        -   [Definições de configuração de extensão de email de servidor de relatório](#bkmk_email_extension)  
  
        -   [Configuração de extensão de biblioteca de documentos do SharePoint de servidor de relatório](#bkmk_documentlibrary_extension)  
  
        -   [Configuração da extensão de entrega NULL](#bkmk_null_extension)  
  
    -   [Configuração geral de extensões de entrega de interface do usuário](#bkmk_ui)  
  
    -   [Configuração geral de extensões de renderização](#bkmk_rendering)  
  
    -   [Configuração geral de extensões de dados](#bkmk_data)  
  
    -   [Configuração geral de extensões de consulta semântica](#bkmk_semantic)  
  
    -   [Configuração de geração de modelo](#bkmk_model)  
  
    -   [Configuração de extensão de segurança](#bkmk_security)  
  
    -   [Configuração de extensão de autenticação](#bkmk_authentication)  
  
    -   [Processamento de eventos](#bkmk_eventprocessing)  
  
    -   [Personalização de definição de relatório](#bkmk_reportdefinition)  
  
    -   [RDLSandboxing](#bkmk_rdlsandboxing)  
  
-   [MapTileServerConfiguration (arquivo rsreportserver. config)](#bkmk_MapTileServer)  
  
-   [Arquivo de configuração padrão para um servidor de relatório do modo nativo](#bkmk_nativedefaultfile)  
  
-   [Arquivo de configuração padrão para um servidor de relatório do modo do SharePoint](#bkmk_sharepointdefaultfile)  
  
##  <a name="bkmk_file_location"></a> Local do arquivo  
  
-   O RSReportServer.config está localizado nas seguintes pastas, dependendo do modo do servidor de relatório:  
  
     **Servidor de relatório do modo nativo:**  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
-   **Servidor de relatório do modo do SharePoint:**  
  
    ```  
    C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
    ```  
  
 Para obter mais informações sobre como editar o arquivo, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
##  <a name="bkmk_generalconfiguration"></a> Configurações gerais (rsreportserver.config)  
 A tabela a seguir fornece informações sobre as configurações gerais que aparecem na primeira parte do arquivo. As configurações são apresentadas na ordem em que aparecem no arquivo de configuração. A última coluna da tabela indica se a configuração se aplica a um servidor de relatório no modo nativo **(N)** , a um servidor de relatório no modo do PharePoint **(S)** ou a ambos.  
  
> [!NOTE]  
>  Neste tópico, "o número inteiro máximo" se refere ao valor INT_MAX de 2147483647.  Para saber mais, veja [Limites de inteiros](https://msdn.microsoft.com/library/296az74e\(v=vs.110\).aspx) (https://msdn.microsoft.com/library/296az74e(v=vs.110).aspx).  
  
|Configuração|Descrição|Modo|  
|-------------|-----------------|----------|  
|**Dsn**|Especifica a cadeia de conexão com o servidor de banco de dados que hospeda o banco de dados do servidor de relatório. Este valor é criptografado e adicionado ao arquivo de configuração quando você cria o banco de dados do servidor de relatório. Para o SharePoint, as informações de conexão de banco de dados são obtidas do banco de dados de configuração do SharePoint.|N,S|  
|**ConnectionType**|Especifica o tipo de credenciais que o servidor de relatório usa para se conectar ao banco de dados do servidor de relatório. Os valores válidos são `Default` e `Impersonate`. `Default` será especificado se o servidor de relatório for configurado para usar um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a conta de serviço para se conectar ao banco de dados do servidor de relatório. `Impersonate` será especificado se o servidor de relatório usar uma conta do Windows para se conectar ao banco de dados do servidor de relatório.|N|  
|**LogonUser, LogonDomain, LogonCred**|Armazena o domínio, o nome de usuário e a senha de uma conta de domínio usada por um servidor de relatório para se conectar a um banco de dados do servidor de relatório. Os valores para `LogonUser`, `LogonDomain` e `LogonCred` são criados quando a conexão do servidor de relatório é configurada para usar uma conta de domínio. Para obter mais informações sobre uma conexão de banco de dados do servidor de relatório, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).|N|  
|**InstanceID**|Um identificador para a instância do servidor de relatório. Os nomes das instâncias do servidor de relatório baseiam-se nos nomes das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este valor especifica um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por padrão, esse valor é `MSRS12`  *\<instancename >* . Não modifique esta configuração. A seguir é apresentado um exemplo do valor completo: `<InstanceId>MSRS12.MSSQLSERVER</InstanceId>`<br /><br /> A seguir é apresentado um exemplo do modo do SharePoint:<br /><br /> `<InstanceId>MSRS12.@Sharepoint</InstanceId>`|N,S|  
|**InstallationID**|Um identificador para a instalação do servidor de relatório criada pela Instalação. Este valor é definido como um GUID. Não modifique esta configuração.|N|  
|**SecureConnectionLevel**|Especifica o grau até o qual as chamadas de serviço Web devem usar o protocolo SSL. Esta configuração é usada para o serviço Web Servidor de Relatório e o Gerenciador de Relatórios. Este valor é definido quando você configura uma URL para usar HTTP ou HTTPS na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Os valores válidos variam de 0 a 3, sendo que 0 é o menos seguro. Para obter mais informações, veja [Usando métodos seguros de serviço Web](../report-server-web-service/net-framework/using-secure-web-service-methods.md) e [Configurar conexões SSL em um Servidor de Relatórios do Modo Nativo](../security/configure-ssl-connections-on-a-native-mode-report-server.md).|N,S|  
|**DisableSecureFormsAuthenticationCookie**|O valor padrão é False.<br /><br /> Especifica se deve ser desabilitada a ação de forçar o cookie usada para o formulário e a autenticação personalizada serem marcados como seguros. A partir do SQL Server 2012, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] automaticamente marcará cookies de autenticação de formulários usados com extensões de autenticação personalizadas, como um cookie seguro quando enviado ao cliente. Ao alterar esta propriedade, os administradores de servidor de relatório e os autores de extensão de segurança personalizada podem reverter para o comportamento anterior que permitiu que o autor de extensão de segurança personalizado determinasse se deve marcar o cookie como um cookie seguro. É recomendado usar cookies seguros para autenticação de formulários para ajudar a impedir a detecção de rede e os ataques de retomada.|N|  
|**CleanupCycleMinutes**|Especifica o número de minutos depois dos quais as sessões antigas e os instantâneos expirados são removidos dos bancos de dados do servidor de relatório. O intervalo de valores válidos é de 0 ao inteiro máximo. O padrão é 10. A configuração do valor como 0 desabilita o processo de limpeza do banco de dados.|N,S|  
|**MaxActiveReqForOneUser**|Especifica o número máximo de relatórios que um usuário pode processar ao mesmo tempo. Quando o limite é atingido, solicitações adicionais de processamento do relatório são negadas. Os valores válidos são de 1 a um inteiro máximo. O padrão é 20.<br /><br /> A maioria das solicitações é processada muito rapidamente, de modo que é improvável que um único usuário tenha mais de 20 conexões abertas a qualquer momento. Se os usuários abrirem mais de 15 relatórios com processamento intenso ao mesmo tempo, talvez seja necessário aumentar esse valor.<br /><br /> Esta configuração é ignorada para servidores de relatório executados no modo integrado do SharePoint.|N,S|  
|**DatabaseQueryTimeout**|Especifica o número de segundos depois dos quais uma conexão com o banco de dados do servidor de relatório atinge o tempo limite. Este valor é transmitido para a propriedade System.Data.SQLClient.SQLCommand.CommandTimeout. Os valores válidos variam de 0 a 2147483647. O padrão é 120. Um valor 0 especifica um tempo de espera ilimitado e, portanto, não é recomendado.|N|  
|**AlertingCleanupCycleMinutes**|O padrão é 20.<br /><br /> Determina com que frequência ocorre a limpeza de dados temporários armazenados no banco de dados de alertas.|P|  
|**AlertingDataCleanupMinutes**|O padrão é 360.<br /><br /> Determina quanto tempo os dados de sessão usados para criar ou editar uma definição de alerta são mantidos dentro do banco de dados de alertas. O padrão é 6 horas.|P|  
|**AlertingExecutionLogCleanup**Minutes|O padrão é 10.080.<br /><br /> Determina quanto tempo deve manter os valores do log de execução de Alertas. O padrão é 7 dias.|P|  
|**AlertingMaxDataRetentionDays**|O padrão é 180.<br /><br /> Determina quanto tempo deve manter dados alertas exigidos para impedir mensagens de alerta duplicadas quando os dados para o alerta não tiverem sido alterados.|P|  
|**RunningRequestsScavengerCycle**|Especifica com que frequência as solicitações órfãs e expiradas são canceladas. Este valor é especificado em segundos. O intervalo de valores válidos é de 0 ao inteiro máximo. O padrão é 60.|N,S|  
|**RunningRequestsDbCycle**|Especifica com que frequência o servidor de relatório avalia os trabalhos em execução para verificar se ultrapassaram o tempo limite de execução de relatório e quando as informações do trabalho em execução devem ser apresentadas na página Gerenciar Trabalhos do Gerenciador de Relatórios. Este valor é especificado em segundos. Os valores válidos variam de 0 a 2147483647. O padrão é 60.|N,S|  
|**RunningRequestsAge**|Especifica um intervalo em segundos depois do qual o status do trabalho em execução muda de novo para em execução. Os valores válidos variam de 0 a 2147483647. O padrão é 30.|N,S|  
|**MaxScheduleWait**|Especifica o número de segundos que o serviço Servidor de Relatório do Windows aguarda a atualização de uma agenda pelo serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent quando o **Próximo Tempo de Execução** é solicitado. Os valores válidos variam de 1 a 60.<br /><br /> No arquivo de configuração padrão, MaxScheduleWait é definido como **5**.<br /><br /> Se o servidor de relatório não pode localizar ou ler o arquivo de configuração, o servidor usa como padrão MaxScheduleWait como 1.|N,S|  
|**DisplayErrorLink**|Indica se um link para o site de Ajuda e Suporte de [!INCLUDE[msCoName](../../includes/msconame-md.md)] é exibido quando ocorrem erros. Este link aparece em mensagens de erro. Os usuários podem clicar no link para abrir o conteúdo atualizado da mensagem de erro no site. Os valores válidos incluem `True` (padrão) e `False`.|N,S|  
|**WebServiceuseFileShareStorage**|Especifica se os relatórios armazenados em cache e os instantâneos temporários (criados pelo serviço Web Servidor de Relatório para a duração de uma sessão de usuário) devem ser armazenados no sistema de arquivos. Os valores válidos são `True` e `False` (padrão). Se o valor for definido como falso, os dados temporários serão armazenados no banco de dados reportservertempdb.|N,S|  
|**WatsonFlags**|Especifica quantas informações são registradas para condições de erros relatadas para a [!INCLUDE[msCoName](../../includes/msconame-md.md)].<br /><br /> 0x0430 = um despejo completo<br /><br /> 0x0428 = um minidespejo<br /><br /> 0x0002 = nenhum despejo|N,S|  
|**WatsonDumpOnExZip Codetions**|Especifica uma lista de exceções que você deseja reportar em um log de erros. Isso é útil quando você tem um problema recorrente e deseja criar um despejo com informações a serem enviadas à [!INCLUDE[msCoName](../../includes/msconame-md.md)] para análise. A criação de despejos afeta o desempenho, portanto, altere esta configuração somente quando estiver diagnosticando um problema.|N,S|  
|**WatsonDumpExcludeIfContainsExZip Codetions**|Especifica uma lista de exceções que você não deseja reportar em um log de erros. Isso é útil quando você está diagnosticando um problema e não deseja que o servidor crie despejos para uma exceção específica.|N,S|  
  
##  <a name="bkmk_URLReservations"></a> URLReservations (arquivo RSReportServer.config)  
 `URLReservations` define o acesso HTTP ao serviço Web Servidor de Relatório e ao Gerenciador de Relatórios para a instância atual. Os URLs são reservados e armazenados em HTTP.SYS quando você configura o servidor de relatório.  
  
> [!WARNING]  
>  Para o modo do SharePoint, as reservas de URL são configuradas na Administração Central do SharePoint. Para saber mais, veja [Configurar o mapeamento de acesso alternativo (https://technet.microsoft.com/library/cc263208(office.12).aspx)](https://technet.microsoft.com/library/cc263208\(office.12\).aspx).  
  
 Não modifique as reservas de URL diretamente no arquivo de configuração. Sempre use a ferramenta [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager ou o provedor WMI do servidor de relatório para criar ou modificar reservas de URL para um servidor de relatório no modo nativo. Se os valores forem modificados no arquivo de configuração, você pode corromper a reserva, o que causa erros de servidor em tempo de execução ou deixa reservas órfãs em HTTP.SYS que não são removidas se o software é desinstalado. Para obter mais informações, consulte [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md) e [URLs em arquivos de configuração &#40;SSRS Configuration Manager&#41;](../install-windows/urls-in-configuration-files-ssrs-configuration-manager.md).  
  
 `URLReservations` é um elemento opcional. Se não estiver presente no arquivo RSReportServer.config, o servidor talvez não esteja configurado. Se for especificado, todos os elementos filho, com exceção de `AccountName`, serão obrigatórios.  
  
 A última coluna da tabela indica se a configuração se aplica a um servidor de relatório no modo nativo (N) ou um servidor de relatório no modo do SharePoint (S) ou ambos.  
  
|Configuração|Descrição|Modo|  
|-------------|-----------------|----------|  
|**Aplicativo**|Contém configurações para os aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|N|  
|**Nome**|Especifica os aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Os valores válidos são ReportServerWebService ou ReportManager.|N|  
|**VirtualDirectory**|Especifica o nome do diretório virtual do aplicativo.|N|  
|**URLs, URL**|Contém uma ou mais reservas de URL para o aplicativo.|N|  
|**UrlString**|Especifica a sintaxe de URL válida para HTTP.SYS. Para obter mais informações sobre a sintaxe, consulte [Sintaxe de reserva de URL &#40;SSRS Configuration Manager&#41;](../install-windows/url-reservation-syntax-ssrs-configuration-manager.md).|N|  
|`AccountSid`|Especifica o SID (identificador de segurança) da conta para a qual a reserva de URL foi criada. Essa deve ser a conta na qual o serviço do Servidor de Relatório é executado. Se o SID não corresponder à conta de serviço, talvez o servidor de relatório não possa ouvir as solicitações naquela URL.|N|  
|`AccountName`|Especifica um nome de conta legível que corresponde a `AccountSid`. Não é usado, mas aparece no arquivo para que você possa determinar facilmente a conta de serviço da conta usada para reserva de URL.|N|  
  
##  <a name="bkmk_Authentication"></a> Autenticação (arquivo RSReportServer.config)  
 `Authentication` especifica um ou mais tipos de autenticação aceitos pelo servidor de relatório. As configurações e os valores padrão são um subconjunto das configurações e dos possíveis valores para esta seção. Só as configurações padrão são adicionadas automaticamente. Para adicionar outras configurações, use um editor de texto para adicionar a estrutura do elemento ao arquivo RSReportServer.config e defina os valores.  
  
 Os valores padrão incluem `RSWindowsNegotiate` e `RSWindowsNTLM` com `EnableAuthPersistance` definido como `True`:  
  
```  
   <Authentication>  
      <AuthenticationTypes>  
         <RSWindowsNegotiate/>  
         <RSWindowsNTLM/>  
      </AuthenticationTypes>  
      <EnableAuthPersistence>true</EnableAuthPersistence>  
   </Authentication>  
```  
  
 Todos os outros valores devem ser adicionados manualmente. Para obter mais informações e exemplos, consulte [Autenticação no servidor de relatório](../security/authentication-with-the-report-server.md).  
  
 A última coluna da tabela a seguir indica se a configuração se aplica a um servidor de relatório de modo nativo (N) ou um servidor de relatório no modo do SharePoint (S) ou ambos.  
  
|Configuração|Descrição|Modo|  
|-------------|-----------------|----------|  
|**AuthenticationTypes**|Especifica um ou mais tipos de autenticação. Os valores válidos são: `RSWindowsNegotiate`, `RSWindowsKerberos`, `RSWindowsNTLM`, `RSWindowsBasic` e `Custom`.<br /><br /> Os tipos `RSWindows` e `Custom` são mutuamente exclusivos.<br /><br /> `RSWindowsNegotiate`, `RSWindowsKerberos`, `RSWindowsNTLM` e `RSWindowsBasic` são cumulativos e podem ser usados juntos, como ilustrado no exemplo de valor padrão anteriormente nesta seção.<br /><br /> A especificação de vários tipos de autenticação é necessária se as solicitações vierem de diversos aplicativos cliente ou navegadores que usam diferentes tipos de autenticação.<br /><br /> Não remova `RSWindowsNTLM`; caso contrário, você limitará o suporte ao navegador a uma parte dos tipos de navegador compatíveis. Para obter mais informações, consulte [Planning for Reporting Services e o suporte a navegador Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).|N|  
|`RSWindowsNegotiate`|O servidor de relatório aceita tokens de segurança Kerberos ou NTLM. Essa é a configuração padrão quando o servidor de relatório está executando em modo nativo e a conta de serviço é Serviço de Rede. Essa configuração é omitida quando o servidor de relatório está executando em modo nativo e a conta de serviço está configurada como uma conta de usuário de domínio.<br /><br /> Se uma conta de domínio estiver configurada para a conta de Serviço do Servidor de Relatório e um SPN (nome da entidade de serviço) não estiver configurado para o servidor de relatório, essa configuração poderá impedir que os usuários façam logon no servidor.|N|  
|`RSWindowsNTLM`|O servidor aceita tokens de segurança NTLM.<br /><br /> Se você remover essa configuração, o suporte ao navegador será limitado para alguns dos tipos de navegador suportados. Para obter mais informações, consulte [Planning for Reporting Services e o suporte a navegador Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).|N, S|  
|`RSWindowsKerberos`|O servidor aceita tokens de segurança Kerberos.<br /><br /> Use essa configuração ou RSWindowsNegotiate ao usar autenticação Kerberos em um esquema de autenticação de delegação restrita.|N|  
|`RSWindowsBasic`|O servidor aceita credenciais Básicas e emite um desafio/resposta quando uma conexão é feita sem credenciais.<br /><br /> A autenticação Básica transmite credenciais nas solicitações HTTP em texto não criptografado. Se você usar autenticação Básica, use o SSL para criptografar tráfego de rede para o servidor de relatório e vice-versa. Para exibir a sintaxe de configuração de exemplo para a autenticação básica do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Autenticação com o servidor de relatório](../security/authentication-with-the-report-server.md).|N|  
|`Custom`|Especifique este valor se você tiver implantado uma extensão de segurança personalizada no computador do servidor de relatório. Para obter mais informações, consulte [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md).|N|  
|**LogonMethod**|Esse valor Especifica o tipo de logon para `RSWindowsBasic`. Se você especificar `RSWindowsBasic`, esse valor é obrigatório. Os valores válidos são 2 ou 3, onde cada valor representa o seguinte:<br /><br /> `2` = Logon de rede de servidores de alto desempenho para autenticar senhas de texto não criptografado<br /><br /> `3` = Logon de texto não criptografado, que preserva as credenciais de logon no pacote de autenticação enviado com cada solicitação HTTP, permitindo que o servidor represente o usuário durante a conexão com outros servidores da rede.<br /><br /> Observação: Os valores 0 (para logon interativo) e 1 (para logon em lotes) não têm suporte no [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|N|  
|**Realm**|Esse valor é usado para `RSWindowsBasic`. Especifica uma partição de recurso que inclui recursos de autorização e autenticação usados para controlar o acesso a recursos protegidos em sua organização.|N|  
|**DefaultDomain**|Esse valor é usado para `RSWindowsBasic`. É usado para determinar o domínio usado pelo servidor para autenticar o usuário. Este valor é opcional, mas, caso seja omitido, o servidor de relatório usará o nome do computador como domínio. Se você instalou o servidor de relatório em um controlador de domínio, o domínio usado será o que é controlado pelo computador.|N|  
|**RSWindowsExtendedProtectionLevel**|O valor padrão é **off**. Para obter mais informações, consulte [Extended Protection for Authentication with Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md).|N|  
|**RSWindowsExtendedProtectionScenario**|O valor padrão é **Proxy**|N|  
|**EnableAuthPersistence**|Determina se a autenticação é executada na conexão ou para cada solicitação.<br /><br /> Os valores válidos são `True` (padrão) ou `False`. Se for definido como `True`, as solicitações subsequentes da mesma conexão assumirão o contexto de representação da primeira solicitação.<br /><br /> Este valor deve ser definido como `False` se você estiver usando o servidor proxy (como ISA Server) para acessar o servidor de relatório. O uso de um servidor proxy permite que uma única conexão do servidor proxy seja usada por vários usuários. Para este cenário, você deve desabilitar a persistência de autenticação de forma que cada solicitação de usuário possa ser autenticada separadamente. Se você não definir **EnableAuthPersistence** para `False`, todos os usuários se conectarão usando o contexto de representação da primeira solicitação.|N,S|  
  
##  <a name="bkmk_service"></a> Serviço (arquivo RSReportServer.config)  
 `Service` especifica as configurações do aplicativo que se aplicam ao serviço como um todo.  
  
 A última coluna da tabela a seguir indica se a configuração se aplica a um servidor de relatório de modo nativo (N) ou um servidor de relatório no modo do SharePoint (S) ou ambos.  
  
|Configuração|Descrição|Modo|  
|-------------|-----------------|----------|  
|**IsSchedulingService**|Especifica se o servidor de relatório mantém um conjunto de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que correspondem a agendas e assinaturas criadas por usuários do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Os valores válidos incluem `True` (padrão) e `False`.<br /><br /> Essa configuração é afetada quando você habilita ou desabilita recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando a faceta Configuração da Área da Superfície do Reporting Services do Gerenciamento Baseado em Políticas. Para obter mais informações, consulte [Iniciar e parar o serviço Servidor de Relatório](start-and-stop-the-report-server-service.md).|N,S|  
|**IsNotificationService**|Especifica se o servidor de relatório está processando notificações e entregas. Os valores válidos incluem `True` (padrão) e `False`. Quando o valor é `False`, as assinaturas não são entregues.<br /><br /> Essa configuração é afetada quando você habilita ou desabilita recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando a faceta Configuração da Área da Superfície do Reporting Services do Gerenciamento Baseado em Políticas. Para obter mais informações, consulte [Iniciar e parar o serviço Servidor de Relatório](start-and-stop-the-report-server-service.md).|N,S|  
|**IsEventService**|Especifica se o serviço processa eventos na fila de evento. Os valores válidos incluem `True` (padrão) e `False`. Quando o valor é `False`, o servidor de relatório não executa operações para agendas ou assinaturas.<br /><br /> Essa configuração é afetada quando você habilita ou desabilita recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando a faceta Configuração da Área da Superfície do Reporting Services do Gerenciamento Baseado em Políticas. Para obter mais informações, consulte [Iniciar e parar o serviço Servidor de Relatório](start-and-stop-the-report-server-service.md).|N,S|  
|**IsAlertingService**|O valor padrão é `True`|P|  
|**PollingInterval**|Especifica o intervalo, em segundos, entre as sondagens da tabela de evento pelo servidor de relatório. O intervalo de valores válidos é de 0 ao inteiro máximo. O padrão é 10.|N,S|  
|**WindowsServiceUseFileShareStorage**|Especifica se os relatórios armazenados em cache e os instantâneos temporários (criados pelo serviço Servidor de Relatório para a duração de uma sessão de usuário) devem ser armazenados no sistema de arquivos. Os valores válidos são `True` e `False` (padrão).|N,S|  
|`MemorySafetyMargin`|Especifica uma porcentagem de `WorkingSetMaximum` que define o limite entre cenários de pressão média e baixa. O valor padrão é 80. Para obter mais informações sobre `WorkingSetMaximum` e configurar a memória disponível, consulte [configurar memória disponível para aplicativos de servidor de relatório](../report-server/configure-available-memory-for-report-server-applications.md).|N,S|  
|**MemoryThreshold**|Especifica uma porcentagem de `WorkingSetMaximum` que define o limite entre cenários de pressão média e alta. O valor padrão é **90**. Esse valor deve ser maior do que o valor definido para `MemorySafetyMargin`. Para obter mais informações, consulte [Configurar memória disponível para aplicativos do Servidor de Relatório](../report-server/configure-available-memory-for-report-server-applications.md).|N,S|  
|**RecycleTime**|Especifica um momento de reciclagem para o domínio de aplicativo, medido em minutos. O intervalo de valores válidos é de 0 ao inteiro máximo. O padrão é 720.|N,S|  
|**MaxAppDomainUnloadTime**|Especifica um intervalo durante o qual o domínio de aplicativo pode ser carregado durante uma operação de reciclagem. Se a reciclagem não for concluída durante esse período de tempo, todo o processamento no domínio do aplicativo será interrompido. Para obter mais informações, consulte [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md).<br /><br /> Este valor é especificado em minutos. O intervalo de valores válidos é de 0 ao inteiro máximo. O padrão é **30**.|N,S|  
|**MaxQueueThreads**|Especifica o número de threads usados pelo serviço Servidor de Relatório do Windows para processamento simultâneo de assinaturas e notificações. O intervalo de valores válidos é de 0 ao inteiro máximo. O padrão é 0. Se você escolher 0, o servidor de relatório determinará o número de máximo de threads. Se um inteiro for especificado, o valor que você especificar definirá o limite máximo de threads que podem ser criados de uma vez. Para obter mais informações sobre como o serviço Windows Servidor de Relatório gerencia a memória para executar processos, consulte [Configurar memória disponível para aplicativos do Servidor de Relatórios](../report-server/configure-available-memory-for-report-server-applications.md).|N,S|  
|**UrlRoot**|Usado pelas extensões de entrega de servidor de relatório para compor URLs usadas por relatórios entregues por email e assinaturas de compartilhamento de arquivos. O valor deve ser um endereço de URL válido para o servidor de relatório a partir do qual o relatório publicado é acessado. Usado pelo servidor de relatório para gerar URLs para acesso offline ou autônomo. Essas URLs são usadas em relatórios exportados, e por extensões de entrega para compor uma URL que é incluída em mensagens de entrega, como links em emails. O servidor de relatório determina as URLs em relatórios baseados no comportamento a seguir:<br /><br /> Quando **UrlRoot** está em branco (o valor padrão) e existem reservas de URL, o servidor de relatório determina automaticamente as URLs, da mesma maneira como as URLs são geradas para o método ListReportServerUrls. A primeira URL retornada pelo método ListReportServerUrls é usada. Ou, se SecureConnectionLevel for maior que zero (0), a primeira URL do SSL será usada.<br /><br /> Quando **UrlRoot** está definido como um valor específico, o valor explícito é usado.<br /><br /> Quando **UrlRoot** está em branco e não existe nenhuma reserva de URL configurada, as URLs em relatórios renderizados e em links de email estão incorretas.|N,S|  
|**UnattendedExecutionAccount**|Especifica um nome de usuário, uma senha e o domínio usados pelo servidor de relatório para executar um relatório. Esses valores são criptografados. Use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou o utilitário **rsconfig** para definir esses valores. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;Configuration Manager do SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).<br /><br /> No modo do SharePoint, você define a conta de execução para um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando a Administração Central do SharePoint. Para obter mais informações, veja [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../manage-a-reporting-services-sharepoint-service-application.md)|N|  
|**PolicyLevel**|Especifica o arquivo de configuração de política de segurança. O valor válido é Rssrvrpolicy.config. Para obter mais informações, consulte [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|N,S|  
|**IsWebServiceEnabled**|Especifica se o serviço Web Servidor de Relatório responde a solicitações de acesso SOAP e URL. Esse valor é definido quando você habilita ou desabilita o serviço usando a faceta Configuração da Área da Superfície do Reporting Services do Gerenciamento Baseado em Políticas.|N,S|  
|**IsReportManagerEnabled**|Especifica se o aplicativo Gerenciador de Relatórios está disponível no servidor de relatório. Os valores válidos são `True` (padrão) e `False`. Se o valor for definido como `True`, o Gerenciador de Relatórios estará disponível. Observe que você ainda deve configurar uma reserva de URL para o Gerenciador de Relatório antes de usá-lo.|N|  
|**FileShareStorageLocation**|Especifica uma única pasta no sistema de arquivos para armazenar instantâneos temporários. Embora seja possível especificar o caminho da pasta como um caminho UNC, isso não é recomendado. O valor padrão é vazio.<br /><br /> `<FileShareStorageLocation>`<br /><br /> `<Path>`<br /><br /> `</Path>`<br /><br /> `</FileShareStorageLocation>`|N,S|  
|**IsRdceEnabled**|Especifica se a RDCE (Extensão de Personalização de Definição de Relatório) está habilitada. Os valores válidos são `True` e `False`.|N,S|  
  
##  <a name="bkmk_UI"></a> UI (arquivo RSReportServer.config)  
 `UI` especifica as configurações que se aplicam ao aplicativo Gerenciador de Relatórios.  
  
 A última coluna da tabela a seguir indica se a configuração se aplica a um servidor de relatório de modo nativo (N) ou um servidor de relatório no modo do SharePoint (S) ou ambos.  
  
|Configuração|Descrição|Modo|  
|-------------|-----------------|----------|  
|**ReportServerUrl**|Especifica o URL do servidor de relatório ao qual o Gerenciador de Relatórios se conecta. Modifique este valor somente se estiver configurando o Gerenciador de Relatórios para se conectar a um servidor de relatório em outra instância ou em um computador remoto. Para obter mais informações, consulte [Configurar o Gerenciador de Relatórios &#40;Modo Nativo&#41;](configure-web-portal.md).|N,S|  
|**ReportBuilderTrustLevel**|Não modifique este valor; ele não é configurável. Na [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e em versões posteriores, construtor de relatórios somente é executado em `FullTrust`. Para obter mais informações, consulte [Configurar o acesso do Construtor de Relatórios](configure-report-builder-access.md) . Para obter mais informações sobre como descontinuar o modo de confiança parcial, consulte [descontinuada no SQL Server Reporting Services no SQL Server 2014](../discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md).|N,S|  
|`PageCountMode`|Somente para o Gerenciador de Relatórios, esta configuração especifica se o servidor de relatório calcula um valor de contagem de página antes de o relatório ser processado ou enquanto o relatório é exibido. Os valores válidos são `Estimate` (padrão) e `Actual`. Use `Estimate` para calcular informações de contagem de página enquanto o usuário exibe o relatório. Inicialmente, a contagem de página é definida como 2 (para a página atual mais uma página adicional), mas aumenta conforme o usuário navega pelo relatório. Use `Actual` se quiser calcular a contagem de página com antecedência, antes que o relatório seja exibido. `Actual` é fornecida para compatibilidade com versões anteriores. Se `PageCountMode` for definido como `Actual`, o relatório inteiro deverá ser processado para obter uma contagem de páginas válida, aumentando o tempo de espera antes de o relatório ser exibido.|N,S|  
  
##  <a name="bkmk_extensions"></a> Extensões (arquivo RSReportServer.config) no modo nativo  
 A seção Extensões aparece no arquivo rsreportserver.config **somente para servidores de relatório no modo nativo** . As informações de extensão para servidores de relatório no modo do SharePoint são armazenadas no banco de dados de configuração do SharePoint e são configuradas de acordo com o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 `Extensions` especifica as configurações para os seguintes módulos extensíveis de uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
-   Extensões de entrega  
  
-   Extensões DeliveryUI  
  
-   Extensões de renderização  
  
-   Extensões de processamento de dados  
  
-   Extensões de consulta semântica (somente interno)  
  
-   Extensões de geração de modelo (somente interno)  
  
-   Extensões de segurança  
  
-   Extensões de autenticação  
  
-   Extensões de processamento de eventos (somente interno)  
  
-   Extensões de personalização para definição de relatórios  
  
 Algumas destas extensões são estritamente para uso interno do servidor de relatório. As configurações para extensões somente de uso interno não são documentadas. As seções a seguir descrevem as definições de configuração para as extensões padrão. Se estiver usando o servidor de relatório com extensões personalizadas, os arquivos de configuração podem conter alguma outra configuração não descrita aqui. Esta seção lista as extensões na ordem em que aparecem. São descritas as configurações que acontecem repetidamente para várias instâncias do mesmo tipo de extensão.  
  
###  <a name="bkmk_extensionsgeneral"></a> Configuração geral de extensões de entrega  
 Especifica extensões de entrega padrão (e possivelmente personalizadas) usadas para entregar relatórios por meio de assinaturas. O arquivo RSReportServer.config contém configurações do aplicativo para quatro extensões de entrega:  
  
1.  Email do servidor de relatório  
  
2.  Entrega de compartilhamento de arquivos.  
  
3.  Biblioteca de documentos de servidor de relatório usada para um servidor de relatório executado no modo integrado do SharePoint.  
  
4.  Provedor de entrega nulo usado para pré-carregar o cache de relatório.  
  
 Para obter mais informações sobre extensões de entrega, consulte [Assinaturas e entrega &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
 Todas as extensões de entrega têm **Nome da Extensão**, **MaxRetries**, **SecondsBeforeRetry**e **Configuração**. Estas configurações compartilhadas são documentadas primeiro. As descrições de configurações específicas da extensão encontram-se em uma segunda tabela.  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**Nome da Extensão**|Especifica um nome amigável e o assembly da extensão de entrega. Não modifique esse valor.|  
|**MaxRetries**|Especifica o número de vezes que um servidor de relatório tentará repetir uma entrega se a primeira tentativa não for bem-sucedida. O valor padrão é 3.|  
|**SecondsBeforeRetry**|Especifica o intervalo de tempo (em segundos) entre cada nova tentativa. O valor padrão é 900.|  
|**Configuração**|Contém as configurações específicas de cada extensão de entrega.|  
  
####  <a name="bkmk_fileshare_extension"></a> Configurações de extensão da entrega de compartilhamento de arquivos  
 A entrega de compartilhamento de arquivos envia um relatório que foi exportado em um formato de arquivo de aplicativo para uma pasta compartilhada na rede. Para obter mais informações, consulte [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md).  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**ExcludedRenderFormats**, **RenderingExtension**|Estas configurações são usadas para excluir intencionalmente formatos de exportação que não funcionam bem com a entrega de compartilhamento de arquivos. Estes formatos normalmente são usados para relatórios interativos, visualização ou para pré-carregar o cache de relatório. Eles não produzem arquivos de aplicativo que podem ser exibidos facilmente a partir de um aplicativo de desktop. Os valores válidos são:<br /><br /> **HTMLOWC**<br /><br /> **RGDI**<br /><br /> **Nulo**|  
  
####  <a name="bkmk_email_extension"></a> Configurações de extensão de email do servidor de relatório  
 O email do servidor de relatório usa um dispositivo de rede SMTP para enviar relatórios a endereços de email. Esta extensão de entrega deve ser configurada antes de ser usada. Para obter mais informações, consulte [configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41; ](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) e [entrega de email no Reporting Services](../subscriptions/e-mail-delivery-in-reporting-services.md).  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**SMTPServer**|Especifica um valor da cadeia de caracteres que indica o endereço de um encaminhador ou servidor SMTP remoto. Este valor é necessário para o serviço SMTP remoto. Esse valor pode ser um endereço IP, um nome UNC de um computador em sua intranet corporativa ou um nome de domínio totalmente qualificado.|  
|**SMTPServerPort**|Especifica um valor inteiro que indica a porta que o serviço SMTP usa para enviar mensagens. A porta 25 normalmente é usada para enviar emails.|  
|**SMTPAccountName**|Contém um valor da cadeia de caracteres que atribui um nome de conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook Express. Você pode definir este valor se o servidor SMTP for configurado para usar o Outlook de algum modo; caso contrário, deixe-o em branco. Use **De** para especificar uma conta de email usada para enviar relatórios.|  
|**SMTPConnectionTimeout**|Especifica um valor inteiro que indica o número de segundos que deve-se aguardar por uma conexão de soquete válida com o serviço SMTP antes do tempo limite. O padrão é 30 segundos, mas este valor será ignorado se **SendUsing** for definido como 2.|  
|**SMTPServerPickupDirectory**|Especifica um valor da cadeia de caracteres que indica o diretório de retirada para o serviço SMTP local. Este valor deve ser um caminho de pasta local (por exemplo, d:\rs-emails) completamente qualificado.|  
|**SMTPUseSSL**|Especifica um valor booliano que pode ser definido para usar o protocolo SSL ao enviar uma mensagem SMTP na rede. O valor padrão é 0 (ou falso). Esta configuração pode ser usada quando o elemento **SendUsing** é definido como 2.|  
|**SendUsing**|Especifica qual método deve ser usado para enviar mensagens. Os valores válidos são:<br /><br /> 1 = Envia uma mensagem do diretório de retirada do serviço SMTP local.<br /><br /> 2 = Envia a mensagem do serviço SMTP de rede.|  
|**SMTPAuthenticate**|Especifica um valor inteiro que indica o tipo de autenticação a ser usado ao enviar mensagens para um serviço SMTP em uma conexão TCP/IP. Os valores válidos são:<br /><br /> 0 = Sem autenticação.<br /><br /> 1 = (sem suporte).<br /><br /> 2 = Autenticação NTLM (NT LanMan). O contexto de segurança do serviço Servidor de Relatório do Windows é usado para se conectar ao servidor SMTP de rede.|  
|**De**|Especifica um endereço de email do qual são enviados relatórios no formato *abc@host.xyz* . O endereço aparece na linha **De** de uma mensagem de email de saída. Este valor é necessário se você estiver usando um servidor SMTP remoto. Deve ser uma conta de email válida que tenha permissão para enviar email.|  
|**EmbeddedRenderFormats, RenderingExtension**|Especifica o formato de renderização usado para encapsular um relatório dentro do corpo de uma mensagem de email. As imagens do relatório são inseridas subsequentemente no relatório. Os valores válidos são MHTML e HTML4.0.|  
|**PrivilegedUserRenderFormats**|Especifica formatos de renderização que um usuário pode selecionar para uma assinatura de relatório quando a assinatura está habilitada por meio da tarefa “Gerenciar todas as assinaturas”. Se este valor não for definido, todos os formatos de processamento que não são excluídos intencionalmente estarão disponíveis para uso.|  
|**ExcludedRenderFormats, RenderingExtension**|Exclui propositadamente os formatos que não funcionam bem com uma determinada extensão de entrega. Não é possível excluir várias instâncias da mesma extensão de renderização. A exclusão de várias instâncias resultará em um erro quando o servidor de relatório ler o arquivo de configuração. Por padrão, as seguintes extensões são excluídas para entrega de email:<br /><br /> **HTMLOWC**<br /><br /> **Nulo**<br /><br /> **RGDI**|  
|**SendEmailToUserAlias**|Esse valor funciona com **DefaultHostName**.<br /><br /> Quando **SendEmailToUserAlias** é definido como `True`, os usuários que definirem assinaturas individuais serão especificados automaticamente como destinatários do relatório. O campo **Para** fica oculto. Se esse valor for `False`, o **para** campo está visível. Defina este valor como `True` se desejar ter controle máximo na distribuição de relatórios. Os valores válidos incluem os seguintes:<br /><br /> `True`= O endereço de email do usuário que cria a assinatura é usado. Este é o valor padrão.<br /><br /> `False` = Qualquer endereço de email pode ser especificado.|  
|**DefaultHostName**|Este valor funciona com **SendEmailToUserAlias**.<br /><br /> Especifica um valor de cadeia de caracteres que indica o nome do host a ser anexado ao alias de usuário quando **SendEmailToUserAlias** for verdadeiro. Este valor pode ser um nome DNS (Sistema de Nome de Domínio) ou endereço IP.|  
|**PermittedHosts**|Limita a distribuição de relatórios especificando explicitamente quais hosts podem receber a entrega de email. Em **PermittedHosts**, cada host é especificado como um elemento **HostName** , onde o valor é um endereço IP ou um nome DNS.<br /><br /> Só contas de email definidas para o host são destinatários válidos. Se você especificar **DefaultHostName**, inclua o host como elemento **HostName** de **PermittedHosts**. Este valor deve ser um ou mais nomes DNS ou endereços IP. Por padrão, esse valor não é definido. Se o valor não for definido, não haverá nenhuma restrição sobre quem pode receber relatórios enviados por email.|  
  
####  <a name="bkmk_documentlibrary_extension"></a> Configuração da extensão da biblioteca de documentos do SharePoint do Servidor de Relatório  
 A biblioteca de documentos do servidor de relatório envia um relatório que foi exportado em um formato de arquivo de aplicativo para uma biblioteca de documentos. Esta extensão de entrega pode ser usada somente por um servidor de relatório configurado para execução no modo integrado do SharePoint. Para obter mais informações, consulte [SharePoint Library Delivery in Reporting Services](../subscriptions/sharepoint-library-delivery-in-reporting-services.md).  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**ExcludedRenderFormats, RenderingExtension**|Estas configurações são usadas para excluir intencionalmente formatos de exportação que não funcionam bem com a entrega de biblioteca de documentos. As extensões de entrega HTMLOWC, RGDI e Null são excluídas. Estes formatos normalmente são usados para relatórios interativos, visualização ou para pré-carregar o cache de relatório. Eles não produzem arquivos de aplicativo que podem ser exibidos facilmente a partir de um aplicativo de desktop.|  
  
####  <a name="bkmk_null_extension"></a> Configuração de extensão de entrega NULL  
 O provedor de entrega NULL é usado para pré-carregar o cache com relatórios gerados previamente para usuários individuais. Não há nenhuma configuração para esta extensão de entrega. Para obter mais informações, consulte [Armazenando relatórios em cache &#40;SSRS&#41;](caching-reports-ssrs.md).  
  
###  <a name="bkmk_ui"></a> Configuração geral de extensões da interface do usuário de entrega  
 Especifica extensões de entrega que contêm um componente de interface de usuário que aparece nas páginas de definição de assinatura usadas ao definir assinaturas individuais no Gerenciador de Relatórios. Se você criar e implantar uma extensão de entrega personalizada que tem opções definidas pelo usuário e desejar usar o Gerenciador de Relatórios, registre a extensão de entrega nesta seção. Por padrão, há configurações o email e o compartilhamento de arquivos do servidor de relatório. As extensões de entrega usadas somente em assinaturas controladas por dados ou em páginas de aplicativo do SharePoint não têm configurações nesta seção.  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**DefaultDeliveryExtension**|Essa configuração determina qual extensão de entrega aparece primeiro na lista de tipos de entrega na página de definição de assinatura. Somente uma extensão de entrega pode conter essa configuração. Os valores válidos incluem `True` ou `False`. Quando esse valor está definido como `True`, essa extensão é a seleção padrão.|  
|**Configuração**|Especifica opções de configuração para uma extensão de entrega. Você pode definir um formato de renderização padrão para cada extensão de entrega. Os valores válidos são os nomes de extensão de renderização anotados na seção de processamento do arquivo rsreportserver.config.|  
|**DefaultRenderingExtension**|Especifica se uma extensão de entrega é o padrão. Email do servidor de relatório é a extensão de entrega padrão. Os valores válidos incluem `True` ou `False`. Se mais de uma extensão contiver o valor `True`, a primeira extensão será considerada a extensão padrão.|  
  
###  <a name="bkmk_rendering"></a> Configuração geral de extensões de renderização  
 Especifica extensões de renderização padrão (e possivelmente personalizadas) usadas na apresentação de relatório.  
  
 Não modifique esta seção a menos que esteja implantando uma extensão de renderização personalizada. Para obter mais informações, consulte [Implementing a Rendering Extension](../extensions/rendering-extension/implementing-a-rendering-extension.md).  
  
 As extensões de renderização padrão incluem o seguinte:  
  
-   XML  
  
-   Nulo  
  
-   CSV  
  
-   PDF  
  
-   RGDI  
  
-   HTML4.0  
  
-   MHTML  
  
-   EXCEL  
  
-   RPL  
  
-   IMAGE  
  
 A partir da versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , as renderizações de MHTML e HTML 4.0 contêm, por padrão, a configuração de informações de dispositivo a seguir para controlar o comportamento do dimensionamento de visualizações de dados.  
  
```  
<DeviceInfo><DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing></DeviceInfo>  
```  
  
 Para obter mais informações sobre as configurações de DeviceInfo, consulte o seguinte:  
  
-   [Configurações das informações do dispositivo MHTML](../html-device-information-settings.md)  
  
-   [Configurações de informações do dispositivo HTML...] /.. / html-dispositivo-informações-settings.md)  
  
-   [Configurações de informações de dispositivos para extensões de renderização &#40;Reporting Services&#41;](../device-information-settings-for-rendering-extensions-reporting-services.md)  
  
 Para obter informações sobre os atributos do elemento **\<Extension>** filho em **\<Render>** , consulte o seguinte:  
  
-   [Personalizar parâmetros de extensão de renderização em RSReportServer.config](../customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
-   [Implantando uma extensão de renderização](../extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
 Não modifique esta seção a menos que esteja implantando uma extensão de renderização personalizada. Para obter mais informações, consulte [Implementing a Rendering Extension](../extensions/rendering-extension/implementing-a-rendering-extension.md).  
  
###  <a name="bkmk_data"></a> Configuração geral de extensões de dados  
 Especifica extensões de processamento de dados padrão (e possivelmente personalizadas) usadas para processar consultas. As extensões de processamento de dados padrão incluem o seguinte:  
  
-   SQL  
  
-   SQLAZURE  
  
-   SQLPDW  
  
-   OLEDB  
  
-   OLEDB-MD  
  
-   ORACLE  
  
-   ODBC  
  
-   XML  
  
-   SHAREPOINTLIST  
  
-   SAPBW  
  
-   ESSBASE  
  
-   TERADATA  
  
 Não modifique esta seção a menos que esteja adicionando extensões de processamento de dados personalizadas. Para obter mais informações, consulte [Implementing a Data Processing Extension](../extensions/data-processing/implementing-a-data-processing-extension.md).  
  
###  <a name="bkmk_semantic"></a> Configuração geral de extensões de consulta semântica  
 Especifica a extensão de processamento de consulta semântica usada para processar modelos de relatório. As extensões de processamento de consulta semântica incluídas no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dão suporte para os dados relacionados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Oracle e dados multidimensionais do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Não modifique esta seção. O processamento de consulta não é extensível.  
  
###  <a name="bkmk_model"></a> Configuração de geração de modelos  
 Especifica uma extensão de geração de modelos usada para criar modelos de relatórios a partir de uma fonte de dados compartilhada que já está publicada em um servidor de relatório. Você pode gerar modelos para dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Oracle e fontes de dados multidimensionais do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Não modifique esta seção. A geração de modelos não é extensível.  
  
###  <a name="bkmk_security"></a> Configuração de extensão de segurança  
 Especifica o componente de autorização usado pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esse componente é usado pela extensão de autenticação registrada no elemento `Authentication` do arquivo RSReportServer.config. Não modifique esta seção a menos que esteja implantando uma extensão de autenticação personalizada. Para obter mais informações sobre como adicionar recursos de segurança personalizados, consulte [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md). Para obter mais informações sobre autorização, consulte [Authorization in Reporting Services](../extensions/security-extension/authorization-in-reporting-services.md).  
  
###  <a name="bkmk_authentication"></a> Configuração de extensão de autenticação  
 Especifica as extensões de autenticação padrão e personalizadas usadas pelo servidor de relatório. A extensão padrão baseia-se na Autenticação do Windows. Não modifique esta seção a menos que esteja implantando uma extensão de autenticação personalizada. Para obter mais informações sobre autenticação no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Autenticação no Reporting Services](../extensions/security-extension/authentication-in-reporting-services.md) e [Autenticação com o Servidor de Relatório](../security/authentication-with-the-report-server.md). Para obter mais informações sobre como adicionar recursos de segurança personalizados, consulte [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md).  
  
###  <a name="bkmk_eventprocessing"></a> Processamento de eventos  
 Especifica manipuladores de eventos padrão. Não modifique esta seção. Esta seção não é extensível.  
  
###  <a name="bkmk_reportdefinition"></a> Personalização de definição de relatório  
 Especifica o nome e o tipo de uma extensão personalizada que modifica uma definição de relatório.  
  
###  <a name="bkmk_rdlsandboxing"></a> RDLSandboxing  
 Especifica um modo de linguagem RDL que permite ajudar a detectar e restringir o uso de tipos específicos de recursos de relatório por inquilinos individuais em um cenário onde vários inquilinos compartilham um único Web farm de servidores de relatório. Para obter mais informações, consulte [Habilitar e desabilitar o RDL Sandboxing](../enable-and-disable-rdl-sandboxing.md).  
  
##  <a name="bkmk_MapTileServer"></a> MapTileServerConfiguration (RSReportServer.config file)  
 `MapTileServerConfiguration` Define as configurações para [!INCLUDE[msCoName](../../includes/msconame-md.md)] serviços Web do Bing Maps que fornece um plano de fundo de um mapa de item de relatório em um relatório publicado em um servidor de relatório. Todos os elementos filho são necessários.  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**MaxConnections**|Especifica o número máximo de conexões com Serviços Web Bing Maps.|  
|**Tempo Limite**|Especifica o tempo limite, em segundos, de espera por uma resposta dos Serviços Web Bing Maps.|  
|**AppID**|Especifica o AppID (identificador de aplicativo) a ser usado para os Serviços Web Bing Maps. `(Default)` especifica o AppID padrão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Para obter mais informações sobre o uso de peças de mapa do Bing no seu relatório, consulte [termos de uso adicionais](https://go.microsoft.com/fwlink/?LinkId=151371) e a [Política de Privacidade](https://go.microsoft.com/fwlink/?LinkId=151372).<br /><br /> Não altere este valor a menos que você precise especificar um AppID personalizado para o seu próprio contrato de licença do Bing Maps. Ao alterar o AppID, você não precisa reiniciar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para que a alteração se efetive.|  
|**CacheLevel**|Especifica um valor da Enumeração HttpRequestCacheLevel de System.Net.Cache. O valor padrão é `Default`. Para obter mais informações, consulte [Enumeração HttpRequestCacheLevel](https://go.microsoft.com/fwlink/?LinkId=153353).|  
  
##  <a name="bkmk_nativedefaultfile"></a> Arquivo de configuração padrão para um servidor de relatório no modo nativo  
 Por padrão, o arquivo rsreportserver.config é instalado no seguinte local:  
  
 **C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer**  
  
```  
<Configuration>     <Dsn>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAoyfT3iJKS0qxG3ibhRCYhAQAAAAiAAAAUgBlAHAAbwByAHQAaQBuAGcAIABTAGUAcgB2AGUAcgAAAANmAADAAAAAEAAAADMnIAaBwxRDy2mu4yg0zKAAAAAABIAAAKAAAAAQAAAAX+0WIyZTGyyEE7R8rtmmZegAAAByz0h1aXSAggJLDnVfd1eyGlLqTln9cCff3DQ25pcNBccP2rsLkwokUrS9kcee4up6UOawgKQuQjqWbLXfpqY9Dp/ueDTcF8h+VlSWNCmcH/OlDo7Pt2S6FestlnrmFrUXImx+XPZoeDYQelDUTgy8cHUAgUlD/wW8beboXXcS04QB0uTy2mwtUl5/xAPOGXFOKkXp6w8wqnxkEdVd60WyyppOu7djRf25OBSZn3I4T5dwaORHqPGVJmVGzcagoG5u0hDqtEf2RD4FnJgcAAIRHcqxj+jqOV+ZCVvmDcdBWCsbg5OdvIBEFAAAABi/yAmdbbA2emMyOAFIQ1k0His4</Dsn>     <ConnectionType>Default</ConnectionType>     <LogonUser></LogonUser>     <LogonDomain></LogonDomain>     <LogonCred></LogonCred>     <InstanceId>MSRS12.MSSQLSERVER</InstanceId>     <InstallationID>{6af9ea4c-2593-4dd8-8e2b-6315014c1a52}</InstallationID>     <Add Key="SecureConnectionLevel" Value="0"/>     <Add Key="DisableSecureFormsAuthenticationCookie" Value="false"/>     <Add Key="CleanupCycleMinutes" Value="10"/>     <Add Key="MaxActiveReqForOneUser" Value="20"/>     <Add Key="DatabaseQueryTimeout" Value="120"/>     <Add Key="RunningRequestsScavengerCycle" Value="60"/>     <Add Key="RunningRequestsDbCycle" Value="60"/>     <Add Key="RunningRequestsAge" Value="30"/>     <Add Key="MaxScheduleWait" Value="5"/>     <Add Key="DisplayErrorLink" Value="true"/>     <Add Key="WebServiceUseFileShareStorage" Value="false"/>     <!--  <Add Key="ProcessTimeout" Value="150" /> -->     <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->     <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->     <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->     <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->     <Add Key="WatsonFlags" Value="0x0428"/>     <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException"/>     <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException"/>     <URLReservations>          <Application>               <Name>ReportServerWebService</Name>               <VirtualDirectory>ReportServer</VirtualDirectory>               <URLs>                    <URL>                         <UrlString>http://+:80</UrlString>                         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>                         <AccountName>NT Service\ReportServer</AccountName>                    </URL>               </URLs>          </Application>          <Application>               <Name>ReportManager</Name>               <VirtualDirectory>Reports</VirtualDirectory>               <URLs>                    <URL>                         <UrlString>http://+:80</UrlString>                         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>                         <AccountName>NT Service\ReportServer</AccountName>                    </URL>               </URLs>          </Application>     </URLReservations>     <Authentication>          <AuthenticationTypes>               <RSWindowsNTLM/>          </AuthenticationTypes>          <RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>          <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>          <EnableAuthPersistence>true</EnableAuthPersistence>     </Authentication>     <Service>          <IsSchedulingService>True</IsSchedulingService>          <IsNotificationService>True</IsNotificationService>          <IsEventService>True</IsEventService>          <PollingInterval>10</PollingInterval>          <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>          <MemorySafetyMargin>80</MemorySafetyMargin>          <MemoryThreshold>90</MemoryThreshold>          <RecycleTime>720</RecycleTime>          <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>          <MaxQueueThreads>0</MaxQueueThreads>          <UrlRoot>          </UrlRoot>          <UnattendedExecutionAccount>               <UserName></UserName>               <Password></Password>               <Domain></Domain>          </UnattendedExecutionAccount>          <PolicyLevel>rssrvpolicy.config</PolicyLevel>          <IsWebServiceEnabled>True</IsWebServiceEnabled>          <IsReportManagerEnabled>True</IsReportManagerEnabled>          <FileShareStorageLocation>               <Path>               </Path>          </FileShareStorageLocation>     </Service>     <UI>          <ReportServerUrl>          </ReportServerUrl>          <PageCountMode>Estimate</PageCountMode>     </UI>     <Extensions>          <Delivery>               <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider,ReportingServicesFileShareDeliveryProvider">                    <MaxRetries>3</MaxRetries>                    <SecondsBeforeRetry>900</SecondsBeforeRetry>                    <Configuration>                         <FileShareConfiguration>                              <ExcludedRenderFormats>                                   <RenderingExtension>HTMLOWC</RenderingExtension>                                   <RenderingExtension>NULL</RenderingExtension>                                   <RenderingExtension>RGDI</RenderingExtension>                              </ExcludedRenderFormats>                         </FileShareConfiguration>                    </Configuration>               </Extension>               <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider,ReportingServicesEmailDeliveryProvider">                    <MaxRetries>3</MaxRetries>                    <SecondsBeforeRetry>900</SecondsBeforeRetry>                    <Configuration>                         <RSEmailDPConfiguration>                              <SMTPServer></SMTPServer>                              <SMTPServerPort>                              </SMTPServerPort>                              <SMTPAccountName>                              </SMTPAccountName>                              <SMTPConnectionTimeout>                              </SMTPConnectionTimeout>                              <SMTPServerPickupDirectory>                              </SMTPServerPickupDirectory>                              <SMTPUseSSL>                              </SMTPUseSSL>                              <SendUsing>2</SendUsing>                              <SMTPAuthenticate>                              </SMTPAuthenticate>                              <From></From>                              <EmbeddedRenderFormats>                                   <RenderingExtension>MHTML</RenderingExtension>                              </EmbeddedRenderFormats>                              <PrivilegedUserRenderFormats>                              </PrivilegedUserRenderFormats>                              <ExcludedRenderFormats>                                   <RenderingExtension>HTMLOWC</RenderingExtension>                                   <RenderingExtension>NULL</RenderingExtension>                                   <RenderingExtension>RGDI</RenderingExtension>                              </ExcludedRenderFormats>                              <SendEmailToUserAlias>True</SendEmailToUserAlias>                              <DefaultHostName>                              </DefaultHostName>                              <PermittedHosts>                              </PermittedHosts>                         </RSEmailDPConfiguration>                    </Configuration>               </Extension>               <Extension Name="Report Server DocumentLibrary" Type="Microsoft.ReportingServices.SharePoint.SharePointDeliveryExtension.DocumentLibraryProvider,ReportingServicesSharePointDeliveryExtension">                    <MaxRetries>3</MaxRetries>                    <SecondsBeforeRetry>900</SecondsBeforeRetry>                    <Configuration>                         <DocumentLibraryConfiguration>                              <ExcludedRenderFormats>                                   <RenderingExtension>HTMLOWC</RenderingExtension>                                   <RenderingExtension>NULL</RenderingExtension>                                   <RenderingExtension>RGDI</RenderingExtension>                              </ExcludedRenderFormats>                         </DocumentLibraryConfiguration>                    </Configuration>               </Extension>               <Extension Name="NULL" Type="Microsoft.ReportingServices.NullDeliveryProvider.NullProvider,ReportingServicesNullDeliveryProvider"/>          </Delivery>          <DeliveryUI>               <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">                    <DefaultDeliveryExtension>True</DefaultDeliveryExtension>                    <Configuration>                         <RSEmailDPConfiguration>                              <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>                         </RSEmailDPConfiguration>                    </Configuration>               </Extension>               <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>          </DeliveryUI>          <Render>               <Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering"/>               <Extension Name="NULL" Type="Microsoft.ReportingServices.Rendering.NullRenderer.NullReport,Microsoft.ReportingServices.NullRendering" Visible="false"/>               <Extension Name="CSV" Type="Microsoft.ReportingServices.Rendering.DataRenderer.CsvReport,Microsoft.ReportingServices.DataRendering"/>               <Extension Name="ATOM" Type="Microsoft.ReportingServices.Rendering.DataRenderer.AtomDataReport,Microsoft.ReportingServices.DataRendering" Visible="false"/>               <Extension Name="PDF" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.PDFRenderer,Microsoft.ReportingServices.ImageRendering"/>               <Extension Name="RGDI" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.RGDIRenderer,Microsoft.ReportingServices.ImageRendering" Visible="false"/>               <Extension Name="HTML4.0" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html40RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">                    <Configuration>                         <DeviceInfo>                              <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>                         </DeviceInfo>                    </Configuration>               </Extension>               <Extension Name="MHTML" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.MHtmlRenderingExtension,Microsoft.ReportingServices.HtmlRendering">                    <Configuration>                         <DeviceInfo>                              <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>                         </DeviceInfo>                    </Configuration>               </Extension>               <Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>               <Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>               <Extension Name="RPL" Type="Microsoft.ReportingServices.Rendering.RPLRendering.RPLRenderer,Microsoft.ReportingServices.RPLRendering" Visible="false" LogAllExecutionRequests="false"/>               <Extension Name="IMAGE" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering"/>               <Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>               <Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>          </Render>          <Data>               <Extension Name="SQL" Type="Microsoft.ReportingServices.DataExtensions.SqlConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.DataExtensions.SqlAzureConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.DataExtensions.SqlDwConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="OLEDB" Type="Microsoft.ReportingServices.DataExtensions.OleDbConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="OLEDB-MD" Type="Microsoft.ReportingServices.DataExtensions.AdoMdConnection,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="ORACLE" Type="Microsoft.ReportingServices.DataExtensions.OracleClientConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="ODBC" Type="Microsoft.ReportingServices.DataExtensions.OdbcConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="XML" Type="Microsoft.ReportingServices.DataExtensions.XmlDPConnection,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SHAREPOINTLIST" Type="Microsoft.ReportingServices.DataExtensions.SharePointList.SPListConnection,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SAPBW" Type="Microsoft.ReportingServices.DataExtensions.SapBw.SapBwConnection,Microsoft.ReportingServices.DataExtensions.SapBw"/>               <Extension Name="ESSBASE" Type="Microsoft.ReportingServices.DataExtensions.Essbase.EssbaseConnection,Microsoft.ReportingServices.DataExtensions.Essbase"/>               <Extension Name="TERADATA" Type="Microsoft.ReportingServices.DataExtensions.TeradataConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>          </Data>          <SemanticQuery>               <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>False</EnableMathOpCasting>                    </Configuration>               </Extension>               <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>False</EnableMathOpCasting>                    </Configuration>               </Extension>               <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQLADW.MSSqlAdwSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>False</EnableMathOpCasting>                    </Configuration>               </Extension>               <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>True</EnableMathOpCasting>                         <DisableNO_MERGEInLeftOuters>False</DisableNO_MERGEInLeftOuters>                         <EnableUnistr>False</EnableUnistr>                         <DisableTSTruncation>False</DisableTSTruncation>                    </Configuration>               </Extension>               <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>True</EnableMathOpCasting>                         <ReplaceFunctionName>oREPLACE</ReplaceFunctionName>                    </Configuration>               </Extension>               <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.QueryExecution.ASSemanticQueryCommand,Microsoft.AnalysisServices.Modeling"/>          </SemanticQuery>          <ModelGeneration>               <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.Generation.ModelGeneratorExtention,Microsoft.AnalysisServices.Modeling"/>          </ModelGeneration>          <Security>               <Extension Name="Windows" Type="Microsoft.ReportingServices.Authorization.WindowsAuthorization, Microsoft.ReportingServices.Authorization"/>          </Security>          <Authentication>               <Extension Name="Windows" Type="Microsoft.ReportingServices.Authentication.WindowsAuthentication, Microsoft.ReportingServices.Authorization"/>          </Authentication>          <EventProcessing>               <Extension Name="SnapShot Extension" Type="Microsoft.ReportingServices.Library.HistorySnapShotCreatedHandler,ReportingServicesLibrary">                    <Event>                         <Type>ReportHistorySnapshotCreated</Type>                    </Event>               </Extension>               <Extension Name="Timed Subscription Extension" Type="Microsoft.ReportingServices.Library.TimedSubscriptionHandler,ReportingServicesLibrary">                    <Event>                         <Type>TimedSubscription</Type>                    </Event>               </Extension>               <Extension Name="Cache Refresh Plan Extension" Type="Microsoft.ReportingServices.Library.CacheRefreshPlanHandler,ReportingServicesLibrary">                    <Event>                         <Type>RefreshCache</Type>                    </Event>               </Extension>               <Extension Name="Cache Update Extension" Type="Microsoft.ReportingServices.Library.ReportExecutionSnapshotUpdateEventHandler,ReportingServicesLibrary">                    <Event>                         <Type>SnapshotUpdated</Type>                    </Event>               </Extension>          </EventProcessing>     </Extensions>     <MapTileServerConfiguration>          <MaxConnections>2</MaxConnections>          <Timeout>10</Timeout>          <AppID>(Default)</AppID>          <CacheLevel>Default</CacheLevel>     </MapTileServerConfiguration></Configuration>  
```  
  
##  <a name="bkmk_sharepointdefaultfile"></a> Arquivo de configuração padrão para o servidor de relatório modo do SharePoint  
 Por padrão, o arquivo rsreportserver.config é instalado no seguinte local:  
  
 **C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\WebServices\Reporting**  
  
```  
<Configuration>  
  <Dsn />  
  <ConnectionType>Default</ConnectionType>  
  <LogonUser>  
  </LogonUser>  
  <LogonDomain>  
  </LogonDomain>  
  <LogonCred>  
  </LogonCred>  
  <InstanceId>MSRS12.@Sharepoint</InstanceId>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="CleanupCycleMinutes" Value="10" />  
  <Add Key="MaxActiveReqForOneUser" Value="20" />  
  <Add Key="AlertingCleanupCycleMinutes" Value="20" />  
  <Add Key="AlertingDataCleanupMinutes" Value="360" />  
  <Add Key="AlertingExecutionLogCleanupMinutes" Value="10080" />  
  <Add Key="AlertingMaxDataRetentionDays" Value="180" />  
  <Add Key="RunningRequestsScavengerCycle" Value="60" />  
  <Add Key="RunningRequestsDbCycle" Value="60" />  
  <Add Key="RunningRequestsAge" Value="30" />  
  <Add Key="MaxScheduleWait" Value="5" />  
  <Add Key="DisplayErrorLink" Value="true" />  
  <Add Key="WebServiceUseFileShareStorage" Value="false" />  
  <!--  <Add Key="ProcessTimeout" Value="150" /> -->  
  <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->  
  <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->  
  <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->  
  <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->  
  <Add Key="WatsonFlags" Value="0x0428" />  
  <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException" />  
  <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException" />  
  <RStrace>  
    <add name="FileName" value="ReportServerService" />  
    <add name="FileSizeLimitMb" value="32" />  
    <add name="KeepFilesForDays" value="14" />  
    <add name="Prefix" value="tid, time" />  
    <add name="TraceListeners" value="file" />  
    <add name="TraceFileMode" value="unique" />  
    <add name="Components" value="all:3" />  
  </RStrace>  
  <URLReservations>  
    <Application>  
      <Name>ReportServerWebService</Name>  
      <VirtualDirectory>ReportServer</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
    <Application>  
      <Name>ReportManager</Name>  
      <VirtualDirectory>Reports</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
  </URLReservations>  
  <Authentication>  
    <AuthenticationTypes>  
      <RSWindowsNTLM />  
    </AuthenticationTypes>  
    <EnableAuthPersistence>true</EnableAuthPersistence>  
  </Authentication>  
  <Service>  
    <IsSchedulingService>True</IsSchedulingService>  
    <IsNotificationService>True</IsNotificationService>  
    <IsEventService>True</IsEventService>  
    <IsAlertingService>True</IsAlertingService>  
    <PollingInterval>10</PollingInterval>  
    <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>  
    <MemorySafetyMargin>80</MemorySafetyMargin>  
    <MemoryThreshold>90</MemoryThreshold>  
    <RecycleTime>720</RecycleTime>  
    <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>  
    <MaxQueueThreads>0</MaxQueueThreads>  
    <UrlRoot>  
    </UrlRoot>  
    <PolicyLevel>rssrvpolicy.config</PolicyLevel>  
    <IsWebServiceEnabled>True</IsWebServiceEnabled>  
    <IsReportManagerEnabled>True</IsReportManagerEnabled>  
    <FileShareStorageLocation>  
      <Path>  
      </Path>  
    </FileShareStorageLocation>  
  </Service>  
  <UI>  
    <ReportServerUrl>  
    </ReportServerUrl>  
    <PageCountMode>Estimate</PageCountMode>  
  </UI>  
  <MapTileServerConfiguration>  
    <MaxConnections>2</MaxConnections>  
    <Timeout>10</Timeout>  
    <AppID>(Default)</AppID>  
    <CacheLevel>Default</CacheLevel>  
  </MapTileServerConfiguration>  
</Configuration>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurar memória disponível para aplicativos do Servidor de Relatório](../report-server/configure-available-memory-for-report-server-applications.md)   
 [Personalizar folhas de estilo para o Visualizador de HTML e o Gerenciador de Relatórios](../customize-style-sheets-for-html-viewer-and-report-manager.md)   
 [Arquivos de configuração do Reporting Services](reporting-services-configuration-files.md)   
 [Inicializar um servidor de relatório &#40; Configuration Manager do SSRS&#41;](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Armazenar dados criptografados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
