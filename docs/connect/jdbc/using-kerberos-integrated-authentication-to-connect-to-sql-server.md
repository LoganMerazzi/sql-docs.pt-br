---
title: Como usar a autenticação integrada do Kerberos para se conectar ao SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 89c87ecb551e3e75397bc431bdefc47fad18f8d2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798598"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Usando a autenticação integrada Kerberos para conectar-se ao SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Começando com o [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], um aplicativo pode usar a propriedade de conexão **authenticationScheme** para indicar que deseja se conectar a um banco de dados usando a autenticação integrada Kerberos tipo 4. Ver [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md) para obter mais informações sobre propriedades de conexão. Para obter mais informações sobre Kerberos, consulte [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758).

Ao usar a autenticação integrada com o Java **Krb5LoginModule**, você pode configurar o módulo usando a [Classe Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] define as seguintes propriedades para IBM Java VMs:

- **useDefaultCcache = true**
- **moduleBanner = false**

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] define as seguintes propriedades para todas as outras VMs Java:

- **useTicketCache = true**
- **doNotPrompt = true**

## <a name="remarks"></a>Remarks

Anteriores ao [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], aplicativos podiam especificar a autenticação integrada (usando Kerberos ou NTLM, dependendo de qual estivesse disponível) usando o **integratedSecurity** propriedade de conexão e referenciando  **sqljdbc_auth**, conforme descrito em [construindo a URL de Conexão](../../connect/jdbc/building-the-connection-url.md).

Começando com o [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], um aplicativo pode usar a propriedade de conexão **authenticationScheme** para indicar que deseja se conectar a um banco de dados usando a autenticação integrada Kerberos por meio da implementação Java Kerberos pura:

- Se você quiser usar a autenticação integrada **Krb5LoginModule**, ainda será necessário especificar o **integratedSecurity = true** propriedade de conexão. Especifique também o **authenticationScheme = JavaKerberos** propriedade de conexão.

- Para continuar usando a autenticação integrada com **sqljdbc_auth**, basta especificar **integratedSecurity = true** propriedade de conexão (e, opcionalmente, **authenticationScheme = NativeAuthentication**).

- Se você especificar **authenticationScheme = JavaKerberos** , mas também não especificar **integratedSecurity = true**, o driver ignorará a **authenticationScheme** propriedade de conexão e esperará a localização das credenciais de nome e a senha de usuário na cadeia de conexão.

Ao usar uma fonte de dados para criar conexões, você pode definir o esquema de autenticação de maneira programada usando **setAuthenticationScheme** e, opcionalmente, definir o SPN para conexões Kerberos usando **setServerSpn**.

Um novo agente foi adicionado para oferecer suporte à autenticação Kerberos: com.microsoft.sqlserver.jdbc.internals.KerbAuthentication. Para obter mais informações, veja [Rastreamento de operação do driver](../../connect/jdbc/tracing-driver-operation.md).

As seguintes diretrizes ajudarão você a configurar o Kerberos:

1. Definir **AllowTgtSessionKey** como 1 no registro do Windows. Para obter mais informações, veja o artigo sobre [Entradas de Registro do protocolo Kerberos e chaves de configuração do KDC no Windows Server 2003](https://support.microsoft.com/kb/837361).
2. Verifique se a configuração Kerberos (krb5.conf nos ambientes UNIX) indica o realm e KDC corretos para o seu ambiente.
3. Inicialize o cache TGT usando kinit ou logging no domínio.
4. Quando um aplicativo que usa **authenticationScheme=JavaKerberos** é executado nos sistemas operacionais Windows Vista ou Windows 7, você deve usar uma conta de usuário padrão. No entanto, se você executar o aplicativo na conta de um administrador, ele precisará ser executado com privilégios de administrador.

> [!NOTE]  
> O atributo de conexão serverSpn é compatível somente com os Microsoft JDBC Drivers 4.2 e superiores.

## <a name="service-principal-names"></a>Nomes de Entidade de Serviço

Um SPN (nome da entidade de serviço) é o nome pelo qual um cliente identifica exclusivamente uma instância de um serviço.

Você pode especificar o SPN usando a propriedade de conexão **serverSpn**, ou simplesmente deixar que o driver o crie para você (o padrão). Essa propriedade está no formato: "MSSQLSvc/fqdn:port\@REALM" em que fqdn é o nome de domínio totalmente qualificado, port é o número da porta e REALM é o realm do Kerberos do SQL Server em letras maiúsculas. A parte do realm dessa propriedade é opcional quando o realm padrão do Kerberos é o mesmo que o do servidor e não está incluído, por padrão. Se você quiser dar suporte a um cenário de autenticação entre áreas de autenticação em que a área de autenticação padrão na configuração Kerberos é diferente do servidor, você deve definir o SPN com a propriedade serverSpn.

Por exemplo, o SPN pode parecer com: "MSSQLSvc/some-server.zzz.corp.contoso.com:1433\@ZZZZ. CORP. CONTOSO.COM"

Para obter mais informações sobre SPNs (nomes de entidade de serviço), consulte:

- [Como usar a autenticação Kerberos no SQL Server](https://support.microsoft.com/kb/319723)

- [Uso de Kerberos com SQL Server](https://go.microsoft.com/fwlink/?LinkId=207814)

> [!NOTE]  
> Antes da versão 6.2 do JDBC driver para uso adequado de Cross Realm Kerberos, você precisará definir explicitamente o **serverSpn**.
>
> A partir da versão 6.2, o driver será capaz de criar o **serverSpn** por padrão, mesmo ao usar Cross Realm Kerberos. Embora seja possível usar um **serverSpn** explicitamente muito.

## <a name="creating-a-login-module-configuration-file"></a>Criando um arquivo de configuração de módulo de logon

Se desejar, você pode especificar um arquivo de configuração Kerberos. Se um arquivo de configuração não for especificado, as configurações a seguir estarão em vigor:

Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;

IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule required useDefaultCcache = true;

Se você decidir criar um arquivo de configuração de módulo de logon, o arquivo deverá ter o seguinte formato:

```java
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```

Um arquivo de configuração de logon consiste em uma ou mais entradas, cada uma especificando qual tecnologia de autenticação subjacente deve ser usada para um ou mais aplicativos específicos. Por exemplo,

```java
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```

Portanto, cada entrada do arquivo de configuração de módulo de logon consiste em um nome seguido por uma ou mais entradas específicas de LoginModule, onde cada uma delas é encerrada com um ponto-e-vírgula e todo o grupo de entradas específicas de LoginModule é delimitado por chaves. Cada entrada do arquivo de configuração é encerrado com um ponto-e-vírgula.

Além de permitir que o driver obtenha credenciais Kerberos usando as configurações especificadas no arquivo de configuração de módulo de logon, o driver pode usar credenciais existentes. Isso poderá ser útil quando o aplicativo precisar criar conexões usando as credenciais de mais de um usuário.

O driver tentará usar as credenciais existentes se elas estiverem disponíveis, antes de tentar fazer logon usando o módulo de logon especificado. Portanto, ao usar o método `Subject.doAs` para executar o código em um contexto específico, uma conexão será criada com as credenciais passadas para a chamada `Subject.doAs`.

Para obter mais informações, veja [Arquivo de configuração de logon JAAS](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html) e [Classe Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html).

A partir do Microsoft JDBC Driver 6.2, nome do arquivo de configuração do módulo de logon pode opcionalmente ser passado usando a propriedade de conexão `jaasConfigurationName`, isso permite que cada conexão ter sua própria configuração de logon.

## <a name="creating-a-kerberos-configuration-file"></a>Criando um arquivo de configuração Kerberos

Para obter mais informações sobre os arquivos de configuração Kerberos, leia o artigo sobre [Requisitos do Kerberos](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html).

Este é um arquivo de configuração de domínio de exemplo, em que YYYY e ZZZZ são os nomes de domínio.

```ini
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  

[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  

[realms]  
        YYYY.CORP.CONTOSO.COM = {  
  kdc = krbtgt/YYYY.CORP. CONTOSO.COM @ YYYY.CORP. CONTOSO.COM  
  default_domain = YYYY.CORP. CONTOSO.COM  
}  

        ZZZZ.CORP. CONTOSO.COM = {  
  kdc = krbtgt/ZZZZ.CORP. CONTOSO.COM @ ZZZZ.CORP. CONTOSO.COM  
  default_domain = ZZZZ.CORP. CONTOSO.COM  
}  

```

## <a name="enabling-the-domain-configuration-file-and-the-login-module-configuration-file"></a>Habilitando o arquivo de configuração de domínio e o arquivo de configuração de módulo de logon

Você pode habilitar um arquivo de configuração de domínio com -Djava.security.krb5.conf. Você pode habilitar um arquivo de configuração do módulo de logon com **-Djava.security.auth.login.config**.

Por exemplo, o comando a seguir pode ser usado para iniciar o aplicativo:

```bash
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  

```

## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Verificando se o SQL Server pode ser acessado via Kerberos

Execute a seguinte consulta no SQL Server Management Studio:

```sql
select auth_scheme from sys.dm_exec_connections where session_id=\@\@spid
```

Verifique se você tem a permissão necessária para executar essa consulta.

## <a name="constrained-delegation"></a>Delegação restrita

A partir do Microsoft JDBC Driver 6.2, o driver dá suporte à delegação restrita de Kerberos. A credencial de delegado pode ser passada como objeto org.ietf.jgss.GSSCredential, essas credenciais são usadas pelo driver para estabelecer a conexão.

```java
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>Usando nomes de entidade de segurança e a senha de Conexão de Kerberos

A partir do Microsoft JDBC Driver 6.2, o driver pode estabelecer Kerberos usando o nome da entidade e a senha de conexão passada na cadeia de caracteres de conexão.

```java
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```

A propriedade de nome de usuário não requer REALM se o usuário pertence a default_realm definido no arquivo krb5.conf. Quando `userName` e `password` é definida juntamente com `integratedSecurity=true;` e `authenticationScheme=JavaKerberos;` propriedade, a conexão é estabelecida com o valor de nome de usuário como entidade de segurança Kerberos junto com a senha fornecida.

## <a name="using-kerberos-authentication-from-unix-machines-on-the-same-domain"></a>Usando a autenticação Kerberos de máquinas Unix no mesmo domínio

Este guia pressupõe que um trabalho que já existe uma configuração do Kerberos. Execute o seguinte código em um computador Windows com trabalhando a autenticação Kerberos para verificar se a mencionada anteriormente é true. O código imprimirá "Esquema de autenticação: KERBEROS" no console se for bem-sucedido. Não há sinalizadores adicionais de tempo de execução, dependências ou as configurações do driver são necessárias fora dos fornecidos. O mesmo bloco de código pode ser executado no Linux para verificar as conexões bem-sucedidas.

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("JavaKerberos");
ds.setDatabaseName("<database>");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

1. Ingresse no domínio o computador cliente ao mesmo domínio que o servidor.
2. (Opcional) Defina o local de tíquete do Kerberos padrão. Mais convenientemente, isso é feito definindo o `KRB5CCNAME` variável de ambiente.
3. Obter o tíquete de Kerberos, gerando um novo ou a colocação de um existente um no local de tíquete do Kerberos padrão. Para gerar um tíquete, simplesmente usar um terminal e inicializar o tíquete via `kinit USER@DOMAIN.AD` onde "Usuário" e "domínio. AD"é a entidade de segurança e o domínio, respectivamente. Por exemplo: `kinit SQL_SERVER_USER03@MICROSOFT.COM`. O tíquete será gerado no local de tíquete padrão ou no `KRB5CCNAME` caminho se definido.
4. O terminal solicitará uma senha, digite a senha.
5. Verificar as credenciais no tíquete via `klist` e confirme se as credenciais são aqueles que você pretende usar para autenticação.
6. Execute o código de exemplo acima e confirme se a autenticação Kerberos foi bem-sucedida.

## <a name="see-also"></a>Consulte Também

[Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
