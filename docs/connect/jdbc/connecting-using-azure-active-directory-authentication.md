---
title: Conectando-se usando a Autenticação do Azure Active Directory | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 802172caef018224403544aad5c3c4fd53778305
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66775964"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Conectando-se usando a Autenticação do Azure Active Directory

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo fornece informações sobre como desenvolver aplicativos Java para usar o recurso de autenticação do Azure Active Directory com o Microsoft JDBC Driver para SQL Server.

Você pode usar a autenticação do Azure Active Directory (AAD), que é um mecanismo para se conectar ao banco de dados SQL v12 usando identidades no Azure Active Directory. Use a autenticação do Azure Active Directory para gerenciar centralmente as identidades de usuários do banco de dados e como uma alternativa à autenticação do SQL Server. O Driver JDBC permite que você especifique suas credenciais do Active Directory do Azure na cadeia de caracteres de conexão JDBC para se conectar ao BD SQL do Azure. Para obter informações sobre como configurar a autenticação do Active Directory do Azure, visite [conectar-se ao SQL banco de dados usando Azure Active Directory a autenticação](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Propriedades de Conexão para dar suporte à autenticação do Azure Active Directory no Microsoft JDBC Driver para SQL Server são:
*   **autenticação**: Use essa propriedade para indicar qual método de autenticação do SQL a ser usado para a conexão. Os valores possíveis são: 
    * **ActiveDirectoryMSI**
        * Suporte desde a versão do driver **v7.2**, `authentication=ActiveDirectoryMSI` pode ser usado para se conectar a um Warehouse banco de dados de SQL do Azure de dentro de um recurso do Azure com suporte "Identity" habilitado. Opcionalmente, **msiClientId** também pode ser especificado nas propriedades de Conexão/fonte de dados, juntamente com esse modo de autenticação, que deve conter a ID do cliente de uma identidade de serviço gerenciado a ser usado para adquirir o  **accessToken** para estabelecer a conexão.
    * **ActiveDirectoryIntegrated**
        * Suporte desde a versão do driver **v6.0**, `authentication=ActiveDirectoryIntegrated` pode ser usado para se conectar a um depósito de banco de dados do SQL Azure usando a autenticação integrada. Para usar esse modo de autenticação, você precisa federar o local Active Directory federação Services (ADFS) com o Azure Active Directory na nuvem. Depois que ele é configurado, você pode se conectar, adicionando a biblioteca nativa 'sqljdbc_auth' ao caminho de classe do aplicativo em um sistema operacional do Windows ou configuração de um tíquete Kerberos para o suporte à autenticação de plataforma cruzada. Você será capaz de acessar o Azure SQL DB/DW sem inserir as credenciais quando você está conectado a uma máquina de ingressado no domínio.
    * **ActiveDirectoryPassword**
        * Suporte desde a versão do driver **v6.0**, `authentication=ActiveDirectoryPassword` pode ser usado para se conectar a um depósito de banco de dados do SQL Azure usando um nome de entidade de segurança do Azure AD e a senha.
    * **SqlPassword**
        * Use `authentication=SqlPassword` para se conectar a um SQL Server usando as propriedades de nome de usuário e senha.
    * **NotSpecified**
        * Use `authentication=NotSpecified` ou deixá-lo como o padrão quando nenhum desses métodos de autenticação são necessárias.

*   **accessToken**: Use essa propriedade de conexão para se conectar a um banco de dados SQL usando um token de acesso. accessToken só pode ser definida usando o parâmetro de propriedades do método getConnection () na classe de Gerenciador de driver. Ele não pode ser usado na URL de conexão.  

Para obter mais informações, consulte a propriedade de autenticação sobre o [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md) página.  


## <a name="client-setup-requirements"></a>Requisitos de instalação do cliente
Para **ActiveDirectoryMSI** autenticação, o abaixo de componentes deve ser instalado no computador cliente:
* Java 8 ou superior
* 7\.2 (ou superior) do Microsoft JDBC Driver para SQL Server
* Ambiente do cliente deve ser um recurso do Azure e deve ter o suporte ao recurso de "Identidade" habilitada.
* Um usuário de banco de dados independente que representa o sistema atribuído identidade gerenciada do recurso do Azure ou atribuído gerenciados identidade do usuário ou um dos grupos aos quais que pertence o MSI, deve existir no banco de dados de destino e deve ter a permissão CONNECT.

Para outros modos de autenticação, o abaixo de componentes deve ser instalado no computador cliente:
* Java 7 ou superior
* Microsoft JDBC Driver 6.0 (ou superior) para o SQL Server
* Se você estiver usando o modo de autenticação baseada em token de acesso, você precisa [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências ao executar os exemplos deste artigo. Para obter mais informações, consulte o **conectando-se usando um Token de acesso** seção.
* Se você estiver usando o **ActiveDirectoryPassword** modo de autenticação, você precisa [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências. Para obter mais informações, consulte o **conectando-se usando o modo de autenticação ActiveDirectoryPassword** seção.
* Se você estiver usando o **ActiveDirectoryIntegrated** modo, você precisa do azure-activedirectory-library-for-java e suas dependências. Para obter mais informações, consulte o **conectando-se usando o modo de autenticação ActiveDirectoryIntegrated** seção.

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>Conectando-se usando o modo de autenticação ActiveDirectoryMSI
O exemplo a seguir mostra como usar o modo `authentication=ActiveDirectoryMSI`. Execute esse exemplo de dentro de um recurso do Azure, e, g uma máquina Virtual do Azure, serviço de aplicativo ou um aplicativo de funções é federado com o Azure Active Directory.

Substitua o nome de servidor/banco de dados com o seu nome de servidor/banco de dados nas linhas a seguir antes de executar o exemplo:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

O exemplo para usar o modo de autenticação ActiveDirectoryMSI:

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Executar esse exemplo em uma máquina Virtual do Azure busca o token de acesso do _identidade gerenciada do sistema atribuída_ ou _identidade gerenciada do usuário atribuído_ (se **msiClientId** é especificado) e estabelece uma conexão usando o token de acesso de busca. Se uma conexão for estabelecida, você verá a seguinte mensagem:

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Conectando-se usando o modo de autenticação ActiveDirectoryIntegrated
A versão 6.4, Microsoft JDBC Driver adiciona suporte para autenticação ActiveDirectoryIntegrated usando um tíquete Kerberos em várias plataformas (Windows, Linux e macOS).
Para obter mais informações, consulte [tíquete Kerberos definido no Windows, Linux e Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) para obter mais detalhes. Como alternativa, no Windows, sqljdbc_auth também pode ser usado para autenticação de ActiveDirectoryIntegrated com o Driver JDBC.

> [!NOTE]
>  Se você estiver usando uma versão mais antiga do driver, verifique isso [link](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) para as respectivas dependências que são necessários para usar esse modo de autenticação. 

O exemplo a seguir mostra como usar o modo `authentication=ActiveDirectoryIntegrated`. Execute esse exemplo em um computador ingressado no domínio que é federado com o Azure Active Directory. Um usuário de banco de dados independente que representa sua entidade de segurança do Azure AD ou um dos grupos que você pertence, deve existir no banco de dados e deve ter a permissão CONNECT. 

Antes de compilar e executar o exemplo, o computador cliente (no qual, você deseja executar o exemplo), baixe o [biblioteca azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e incluí-los no caminho de compilação de Java

Substitua o nome de servidor/banco de dados com o seu nome de servidor/banco de dados nas linhas a seguir antes de executar o exemplo:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

O exemplo para usar o modo de autenticação ActiveDirectoryIntegrated:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

Executar esse exemplo em um computador cliente automaticamente usa o tíquete do Kerberos e nenhuma senha é necessária. Se uma conexão for estabelecida, você verá a seguinte mensagem:

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Definir o tíquete do Kerberos no Windows, Linux e Mac

Você precisa configurar um tíquete de Kerberos a vinculação de seu usuário atual para uma conta de domínio do Windows. Um resumo das principais etapas está incluído abaixo.

#### <a name="windows"></a>Windows
JDK vem com `kinit`, que pode ser usado para obter um TGT do Centro de distribuição de chaves (KDC) em um domínio ingressado no computador que está federado com o Azure Active Directory.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Etapa 1: Recuperação de tíquete de concessão de tíquete
- **Executar em**: Windows
- **Ação**:
  - Use o comando `kinit username@DOMAIN.COMPANY.COM` para obter um TGT do KDC, em seguida, ele solicitará sua senha do domínio.
  - Use `klist` para ver os tíquetes disponíveis. Se o kinit foi bem-sucedida, você deverá ver um tíquete do krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

> [!NOTE]
>  Talvez seja necessário especificar uma `.ini` de arquivos com `-Djava.security.krb5.conf` para seu aplicativo para localizar o KDC.

#### <a name="linux-and-mac"></a>Linux e Mac

##### <a name="requirements"></a>Requisitos
Acesso a um computador ingressado no domínio do Windows para consultar seu controlador de domínio do Kerberos.

##### <a name="step-1-find-kerberos-kdc"></a>Etapa 1: Localizar o KDC do Kerberos
- **Executar em**: linha de comando do Windows
- **Ação**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (onde "DOMAIN.COMPANY.COM" é mapeada para o nome do seu domínio)
- **Saída de exemplo**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Informações para extrair** Nomeie o controlador de domínio, nesse caso `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Etapa 2: Configurando o KDC no krb5
- **Executar em**: Linux/Mac
- **Ação**: editar o /etc/krb5.conf em um editor de sua escolha. Configure as seguintes chaves
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  Em seguida, salve o arquivo krb5.conf e sair

> [!NOTE]
>  Domínio deve estar em letras maiusculas.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>Etapa 3: Testar a recuperação de tíquete de concessão de tíquete
- **Executar em**: Linux/Mac
- **Ação**:
  - Use o comando `kinit username@DOMAIN.COMPANY.COM` para obter um TGT do KDC, em seguida, ele solicitará sua senha do domínio.
  - Use `klist` para ver os tíquetes disponíveis. Se o kinit foi bem-sucedida, você deverá ver um tíquete do krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Conectando-se usando o modo de autenticação ActiveDirectoryPassword
O exemplo a seguir mostra como usar o modo `authentication=ActiveDirectoryPassword`.

Antes de criar e executar o exemplo:
1.  No computador cliente (no qual, você deseja executar o exemplo), baixe o [biblioteca azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) e suas dependências e incluí-los no caminho de compilação de Java
2.  Localize as seguintes linhas de código e substitua o nome do servidor/banco de dados pelo seu nome de servidor/banco de dados.
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Localize as seguintes linhas de código e substitua o nome de usuário, com o nome do usuário AAD que você deseja conectar-se como.
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

O exemplo para usar o modo de autenticação ActiveDirectoryPassword:
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
Se a conexão for estabelecida, você verá a seguinte mensagem como saída:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Um banco de dados do usuário independente deve existir e um usuário de banco de dados independente que representa o especificada usuário do Azure AD ou um dos grupos, o Azure especificado pertence ao usuário do AD, deve existir no banco de dados e deve ter a permissão CONNECT (exceto para o Azure Active Directory administrador do servidor ou grupo)

## <a name="connecting-using-access-token"></a>Conectando-se usando um Token de acesso
Aplicativos/serviços pode recuperar um token de acesso do Active Directory do Azure e usá-lo para se conectar ao banco de dados/Data Warehouse de SQL do Azure.

> [!NOTE] 
> **accessToken** só pode ser definido usando o parâmetro de propriedades do método getConnection () na classe de Gerenciador de driver. Ele não pode ser usado na cadeia de conexão.

O exemplo a seguir contém um aplicativo Java simples que se conecta ao banco de dados/Data Warehouse do Azure SQL usando a autenticação baseada em token de acesso. Antes de criar e executar o exemplo, execute as seguintes etapas:
1.  Crie uma conta de aplicativo no Azure Active Directory para seu serviço.
    1. Entre no portal do Azure.
    2. Clique em Active Directory do Azure no painel de navegação esquerdo.
    3. Clique na guia "Registros do aplicativo".
    4. Na gaveta, clique em "Novo registro de aplicativo".
    5. Insira mytokentest como um nome amigável para o aplicativo, selecione "aplicativo Web/API".
    6. URL de logon não é necessário. Basta fornecer qualquer coisa: "https://mytokentest".
    7. Clique em "Criar" na parte inferior.
    9. Ainda no portal do Azure, clique na guia "Configurações" do seu aplicativo e abra a guia "Propriedades".
    10. Localize o valor de "ID do aplicativo" (também conhecido como ID do cliente) e copie-o, pois você precisará dele mais tarde ao configurar seu aplicativo (por exemplo, 1846943b-ad04-4808-aa13-4702d908b5c1). Consulte o instantâneo a seguir.
    11. Na seção "Chaves", crie uma chave preenchendo o campo de nome, selecionando a duração da chave, e salvar a configuração (deixe o campo de valor vazio). Depois de salvar, o campo de valor deve ser preenchido automaticamente, copie o valor gerado. Esse é o Segredo do cliente.
    12. No painel à esquerda, clique em Active Directory do Azure. Em "Registros do aplicativo", localize a guia "Pontos de extremidade". Copie a URL em "ENDPOINT TOKEN OATH 2.0", que é a URL do STS.
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Faça logon no banco de dados de usuário do Azure SQL Server como um administrador do Active Directory do Azure e usando um usuário de banco de dados independente de uma provisão do comando T-SQL para seu aplicativo principal. Para obter mais informações, consulte o [conectar-se ao banco de dados SQL ou SQL Data Warehouse por usando o Azure Active Directory autenticação](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) para obter mais detalhes sobre como criar um administrador do Active Directory do Azure e um usuário de banco de dados independente.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  No computador cliente (no qual, você deseja executar o exemplo), baixe o [azure-activedirectory-library-for-java](https://github.com/AzureAD/azure-activedirectory-library-for-java) biblioteca e suas dependências e incluí-los no caminho de compilação de Java. Observe que o azure-activedirectory-library-for-java somente é necessário para executar esse exemplo específico. O exemplo usa as APIs desta biblioteca para recuperar o token de acesso do AAD do Azure. Se você já tiver um token de acesso, você pode ignorar esta etapa. Observe que você também precisará remover a seção de exemplo que recupera o token de acesso.

No exemplo a seguir, substitua o nome de URL do STS, ID do cliente, segredo do cliente, servidor e banco de dados com seus valores.

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

Se a conexão for bem-sucedida, você verá a seguinte mensagem como saída:

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
