---
title: Notas de versão para o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 083eda191d51ec7043f24511d03c90beff9bfe84
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657731"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver"></a>Notas de versão para o Microsoft JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo lista as versões dos _Microsoft JDBC Driver para SQL Server_. Para cada versão de lançamento, as alterações são nomeadas e descritas.

## <a name="721"></a>7.2.1

### <a name="compliance"></a>Conformidade

11 de fevereiro de 2019

| Alteração de conformidade | Detalhes |
| :---------------- | :------ |
| Baixe as atualizações mais recentes para o JDBC Driver 7.2. | &bull; &nbsp; [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?linkid=2063159)<br/>&bull; &nbsp; [GitHub 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1)<br/>&bull; &nbsp; [Central do Maven](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| Totalmente compatível com a especificação de API do JDBC 4.2. | Os jars no pacote 7.2 são nomeados de acordo com a compatibilidade de versão de Java.<br/><br/>Por exemplo, o arquivo de mssql-jdbc-7.2.1.jre11.jar do pacote 7.2 deve ser usado com o Java 11. |
| Compatível com JDK (Java Development Kit) versão 11.0, além de JDK 1.8. | Microsoft JDBC Driver 7.2 para o SQL Server agora é compatível com o Java Development Kit (JDK) versão 11.0, além de JDK 1.8. |
| &nbsp; | &nbsp; |

> [!NOTE]
> Um problema com a análise de instruções SQL foi encontrado no driver JDBC 7.2 Release To Web (RTW) lançado em 31 de janeiro de 2019. A alteração foi revertida e jars novo (versão 7.2.1) foram lançadas em 11 de fevereiro de 2019.
>
> Atualize seus projetos para usar o 7.2.1 jars de versão. Para obter mais informações, veja as notas de versão para [GitHub, 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1).

### <a name="active-directory-managed-service-identity-msi-authentication"></a>Active Directory _Managed Service Identity_ autenticação (MSI)

| Alteração MSI | Detalhes |
| :--------- | :------ |
| Dá suporte ao modo de autenticação do Active Directory MSI Managed Service Identity (). | Esse modo de autenticação é aplicável em recursos do Azure com suporte para o recurso de "Identidade" habilitado.<br/><br/>Ambos os tipos de identidades de sistema gerenciado (MSI) têm suporte pelo driver para adquirir **accessToken** para estabelecer a conexão segura. |
| Mais detalhes e um aplicativo de exemplo para usar esse modo de autenticação. | Confira [Como se conectar usando a autenticação do Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md). |
| &nbsp; | &nbsp; |

### <a name="introduces-open-service-gateway-initiative-osgi-support"></a>Apresenta _abrir iniciativa de Gateway de serviço_ suporte (OSGi)

| Alteração de OSGi | Detalhes |
| :---------- | :------ |
| **DataSourceFactory** implementação adicionada. | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| **Ativador** implementação adicionada. | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-sqlservererror-apis"></a>Apresenta _SQLServerError_ APIs

| Alteração de API de erro | Detalhes |
| :--------------- | :------ |
| API SQLServerError introduzido. | Getter APIs para recuperar os detalhes adicionais sobre o erro gerado a partir do servidor.<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| Detalhes adicionais. | Confira [Como tratar erros](../../connect/jdbc/handling-errors.md). |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-163"></a>A versão 1.6.3 da _ADAL4J (Biblioteca de Autenticação do Microsoft Azure Active Directory) para Java_ foi atualizada

| Alteração da ADAL4J | Detalhes |
| :------------ | :------ |
| Atualizada a dependência do Maven no ADAL4J para versão 1.6.3. | &nbsp; |
| Apresenta _tempo de execução de cliente de Java para AutoRest_ como uma dependência do Maven, versão 1.6.5. | &nbsp; |
| Detalhes adicionais. | Confira [Dependências de recurso do Microsoft JDBC Driver para SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-key-vault-sdk-for-java-version-120"></a>Atualizado _SDK do Microsoft Azure Key Vault para Java_, versão 1.2.0

| Alteração do SDK do Cofre de chave | Detalhes |
| :------------------- | :------ |
| Atualizado sua dependência do Maven no _SDK do Microsoft Azure Key Vault para Java_ para a versão 1.2.0. | &nbsp; |
| Introduz o _SDK do Microsoft Azure para Key Vault WebKey_ como uma dependência Maven, versão 1.2.0. | &nbsp; |
| Detalhes adicionais. | Confira [Dependências de recurso do Microsoft JDBC Driver para SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

| Problemas conhecidos | Detalhes |
| :----------- | :------ |
| Consultas parametrizadas, em determinados casos. | Uma atualização da versão 7.2, que será v7.2.1, será lançada em fevereiro de 2019 para resolver esse problema. |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

Microsoft JDBC Driver 7.0 para SQL Server é totalmente compatível com a especificação de API do JDBC 4.2. Os jars no pacote 7.0 são nomeados de acordo com a compatibilidade de versão de Java. Por exemplo, o arquivo de mssql-jdbc-7.0.0.jre10.jar do pacote 7.0 deve ser usado com o Java 10.

### <a name="support-for-jdk-10"></a>Suporte para JDK 10

Microsoft JDBC Driver 7.0 para SQL Server agora é compatível com o Java Development Kit (JDK) versão 10.0, além de JDK 1.8. Essa atualização também expõe o driver `Automatic-Module-Name` como `com.microsoft.sqlserver.jdbc` por meio de seu arquivo de manifesto.

### <a name="support-for-spatial-datatypes"></a>Suporte para tipos de dados espaciais

Microsoft JDBC Driver 7.0 para SQL Server agora oferece suporte para SQL Server spatial tipos de dados Geography e Geometry. Para obter mais informações sobre as APIs de tipo de dados espaciais e como usá-los, consulte [usando os tipos de dados espaciais](../../connect/jdbc/use-spatial-datatypes.md).

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>A implementação para JDBC 4.3 introduziu as APIs beginRequest() e endRequest() do java.sql.Connection.

Microsoft JDBC Driver 7.0 para SQL Server agora implementa `beginRequest()` e `endRequest()` APIs do `java.sql.Connection` classe. Essas APIs foram introduzidas com JDBC 4.3 especificações e JDK 9. Para obter mais informações sobre a implementação do driver dessas APIs, consulte [conformidade do JDBC 4.3 para o Driver JDBC](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="support-for-sql-data-discovery-and-classification"></a>Suporte para classificação e descoberta de dados SQL

Microsoft JDBC Driver 7.0 para o SQL Server oferece suporte para descoberta de dados SQL e classificação com qualquer banco de dados de destino que dá suporte a esse recurso. O driver agora expõe `SQLServerResultSet.getSensitivityClassification()` APIs para extrair essas informações o buscadas `ResultSet`.

Para obter mais informações sobre como usar esse recurso com o Driver JDBC, consulte o exemplo na [SQL dados de descoberta e classificação](../../connect/jdbc/data-discovery-classification-sample.md).

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>Adicionada a propriedade de conexão: useBulkCopyForBatchInsert

Microsoft JDBC Driver 7.0 para SQL Server apresenta uma nova propriedade de conexão, `useBulkCopyForBatchInsert`. Essa propriedade é suportada somente para o Azure SQL Data Warehouse.

Essa propriedade está desabilitada por padrão. Você pode habilitá-la aumentar o desempenho de aplicativos de usuário quando você estiver enviando dados de grandes quantidades Azure SQL Data Warehouse. Habilitar essa propriedade altera o comportamento de operações de inserção em lotes para alternar para operações de cópia em massa com dados fornecidos pelo usuário. Para obter mais informações sobre essa propriedade e suas limitações, consulte [operação de inserção usando o API de cópia em massa para o lote](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md).

### <a name="added-connection-property-cancelquerytimeout"></a>Adicionada a propriedade de conexão: cancelQueryTimeout

Microsoft JDBC Driver 7.0 para SQL Server apresenta uma nova propriedade de conexão `cancelQueryTimeout`, para cancelar `queryTimeout` nos `java.sql.Connection` e `java.sql.Statement` objetos.

### <a name="added-azure-key-vault-provider-constructors"></a>Construtores de Azure Key Vault Provider adicionados

Microsoft JDBC Driver 7.0 para SQL Server reintroduz um construtor removido anteriormente, para `SQLServerColumnEncryptionAzureKeyVaultProvider`. Ela permitida autenticação por meio de um método personalizado implementado no `SQLServerKeyVaultAuthenticationCallback` para buscar um token de acesso.

Novos construtores têm a seguinte definição:

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>A versão da "ADAL4J (Biblioteca de Autenticação do Microsoft Azure Active Directory para Java)" foi atualizada: 1.6.0

Microsoft JDBC Driver 7.0 para o SQL Server tiver atualizado sua dependência do Maven em "Microsoft Azure Active Directory Authentication Library (ADAL4J) para Java" para a versão 1.6.0. Para obter mais informações sobre dependências, consulte [dependências de recurso do Microsoft JDBC Driver para SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="64"></a>6.4

Microsoft JDBC Driver 6.4 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars no pacote de 6,4 são nomeados de acordo com a compatibilidade de versão de Java. Por exemplo, o arquivo de mssql-jdbc-6.4.0.jre8.jar do pacote de 6,4 deve ser usado com o Java 8.

### <a name="support-for-jdk-9"></a>Suporte para JDK 9

O driver dá suporte à versão 9.0, além de JDK 8.0 e 7.0 do JDK.

### <a name="jdbc-43-compliance"></a>Conformidade do JDBC 4.3

O driver é compatível com a especificação da API Java Database Connectivity 4.3, além da 4.1 e da 4.2. Os métodos da API do JDBC 4.3 são adicionados, mas ainda não implementados. Para obter detalhes, confira [Conformidade do JDBC 4.3 com o JDBC Driver](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="added-connection-property-sslprotocol"></a>Adicionada a propriedade de conexão: sslProtocol

Uma nova propriedade de conexão permite aos usuários especificar a palavra-chave de protocolo TLS. Os valores possíveis são: "TLS", "TLSv1", "TLSv1.1" e "TLSv1.2". Para obter detalhes, consulte [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol).

### <a name="deprecated-connection-property-fipsprovider"></a>Preterido de propriedade de conexão: fipsProvider

A propriedade de conexão `fipsProvider` é removido da lista de propriedades de conexão aceitos. Para obter detalhes, consulte relacionado [solicitação pull do GitHub](https://github.com/Microsoft/mssql-jdbc/pull/460).

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>Propriedades de conexão adicionada para especificar um TrustManager personalizado

O driver agora dá suporte à especificação de um TrustManager personalizado com adicionados `trustManagerClass` e `trustManagerConstructorArg` propriedades de conexão. Dinamicamente, você pode especificar um conjunto de certificados que são confiáveis em uma base por conexão sem modificar as configurações globais para o ambiente do Java (JVM) de máquina virtual.

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>Adicionado suporte para datetime/smallDatetime nos parâmetros com valor de tabela

O driver agora dá suporte os tipos de dados `datetime` e `smallDatetime` quando você estiver usando parâmetros com valor de tabela (TVPs).

### <a name="added-support-for-the-sqlvariant-datatype"></a>Adicionado suporte para o tipo de dados sql_variant

O Driver JDBC agora dá suporte a `sql_variant` tipos de dados a ser usado com o SQL Server. O `sql_variant` também há suporte para o tipo de dados com recursos como TVPs e cópia em massa com as seguintes limitações:

* **Para valores de data**: 

  Quando você estiver usando um TVP para popular uma tabela que contém `datetime`, `smalldatetime`, ou `date` valores armazenados em um `sql_variant` coluna, a chamada a `getDateTime()`, `getSmallDateTime()`, ou `getDate()` método no conjunto de resultados não funciona e gera a seguinte exceção:

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  Como alternativa, use o `getString()` ou `getObject()` método em vez disso.

* **Usando um TVP com sql_variant para valores nulos**:
  
  Se você estiver usando um TVP para popular uma tabela e enviar um valor nulo para o `sql_variant` tipo de coluna, você encontrará uma exceção. Inserindo um valor NULL com o tipo de coluna `sql_variant` em um TVP não é suportado atualmente.

### <a name="implemented-prepared-statement-metadata-caching"></a>Implementado o cache de metadados de instrução preparada

O Driver JDBC implementou o cache de metadados de instrução preparada para melhorar o desempenho. O driver agora dá suporte a cache de metadados de instrução preparada no driver com `disableStatementPooling` e `statementPoolingCacheSize` propriedades de conexão. Por padrão, esse recurso está desabilitado. Para obter mais informações, consulte [preparado instrução cache de metadados para o JDBC Driver](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md).

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>Adicionado suporte para autenticação integrada do AD do Azure no Linux/Mac

O JDBC Driver agora é compatível com a Autenticação Integrada do Azure AD (Azure Active Directory) em todos os sistemas operacionais compatíveis (Windows, Linux e Mac) com Kerberos. Como alternativa, em sistemas de operacionais do Windows, os usuários possam autenticar com sqljdbc_auth.

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>A versão da "ADAL4J (Biblioteca de Autenticação do Microsoft Azure Active Directory para Java)" foi atualizada: 1.4.0

O Driver JDBC atualizou sua dependência do Maven em "Microsoft Azure Active Directory Authentication Library (ADAL4J) para Java" para a versão 1.4.0. Para obter mais informações sobre dependências, consulte [dependências de recurso do Microsoft JDBC Driver para SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="62"></a>6.2

Microsoft JDBC Driver 6.2 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars no pacote 6.2 são nomeados de acordo com a compatibilidade de versão de Java. Por exemplo, o arquivo mssql-jdbc-6.2.2.jre8.jar do pacote 6.2 é recomendado para uso com Java 8.

> [!NOTE]  
> Um problema com o aperfeiçoamento de cache de metadados foi encontrado na RTW do 6.2 JDBC lançado em 29 de junho de 2017. A melhoria foi revertida e jars novo (versão 6.2.1) foram lançadas em 17 de julho de 2017. 
>
> Outro aprimoramento atualizado a versão da biblioteca dependente do Azure Key Vault para 1.0.0 e jars novo (versão 6.2.2) foram lançadas em 19 de outubro de 2017.
>
> Baixar as atualizações mais recentes para o JDBC Driver 6.2 partir [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2), e [Central do Maven](https://search.maven.org/search?q=g:com.microsoft.sqlserver). Atualize seus projetos para usar o 6.2.2 jars de versão. Para obter mais informações, veja as notas de versão para [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) e [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2).

### <a name="azure-ad-support-for-linux"></a>Suporte do Azure AD para Linux

Conecte seus aplicativos do Linux para o banco de dados SQL usando a autenticação do AD do Azure por meio de métodos de token de acesso e o nome de usuário e senha.

### <a name="fips-enabled-jvms"></a>JVMs FIPS habilitada

O Driver JDBC agora pode ser usado em JVMs executados no modo de conformidade 140 FIPS Federal Information Processing Standard () para atender aos padrões federais em conformidade.

### <a name="kerberos-authentication-improvements"></a>Melhorias de autenticação do Kerberos

O Driver JDBC agora tem suporte para:

- Método de entidade de segurança/senha para aplicativos em que a configuração do Kerberos não poderá ser modificada ou não é possível recuperar um novo token ou keytab. Esse método pode ser usado para autenticar a uma instância do SQL Server que permite apenas a autenticação Kerberos.
- Autenticação entre realms que usa a autenticação integrada Kerberos sem definir explicitamente o SPN do servidor. O driver agora computará automaticamente o realm, mesmo quando ele não for fornecido.
- Delegação restrita de Kerberos, aceitando representada as credenciais do usuário como um objeto de credencial GSS por meio da fonte de dados. Essa credencial representada, em seguida, é usada para estabelecer uma conexão Kerberos.

### <a name="added-timeouts"></a>Tempos limite adicionado

O Driver JDBC agora oferece suporte a limite configurável a seguir. Você pode alterá-los com base nas necessidades do seu aplicativo.

- Tempo limite da consulta para controlar o número de segundos a aguardar antes que um tempo limite ocorra quando você estiver executando uma consulta.
- Tempo limite de soquete para especificar o número de milissegundos de espera antes que ocorra um tempo limite em um soquete de leitura ou aceitar.

## <a name="61"></a>6.1

Microsoft JDBC Driver 6.1 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Isso é a versão inicial do código-fonte aberto do Driver JDBC. Ele contém os arquivos de mssql-jdbc-6.1.0.jre8.jar e mssql-jdbc-6.1.0.jre7.jar, que correspondem a compatibilidade de versão de Java.

## <a name="60"></a>6.0

Microsoft JDBC Driver 6.0 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars no pacote 6.0 são nomeados de acordo com sua conformidade com a versão de API do JDBC. Por exemplo, o arquivo sqljdbc42.jar do pacote 6.0 é compatível com JDBC API 4.2. Da mesma forma, o arquivo de sqljdbc41.jar está em conformidade com a API do JDBC 4.1.

Para garantir que você tenha o arquivo de sqljdbc41.jar ou sqljdbc42.jar correto, execute as seguintes linhas de código. Se a saída é "versão do Driver: 6.0.7507.100", você tem o pacote do JDBC Driver 6.0.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

O driver dá suporte ao recurso Always Encrypted no SQL Server 2016. Esse recurso garante que os dados confidenciais nunca sejam vistos em texto sem formatação em uma instância do SQL Server. O Always Encrypted funciona pela criptografia transparente de dados no aplicativo, de forma que o SQL Server apenas manipulará os dados criptografados e os valores de texto não criptografado. Mesmo se a instância do SQL Server ou o computador host estiverem comprometidos, o invasor apenas poderá obter um texto cifrado de dados confidenciais. Para obter detalhes, veja [Uso de Always Encrypted com o driver JDBC em Linux](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).

### <a name="internationalized-domain-names"></a>Nomes de domínio internacionalizados

O driver dá suporte a nomes de domínio internacionalizados (IDNs) para nomes de servidor. Para obter detalhes, consulte "Usando nomes de domínio internacionais" a [recursos internacionais do JDBC Driver](../../connect/jdbc/international-features-of-the-jdbc-driver.md) artigo.

### <a name="parameterized-queries"></a>Consultas parametrizadas

O driver agora é compatível com a recuperação de metadados de parâmetro com instruções preparadas para consultas complexas, como subconsultas e/ou junções. Observe que essa melhoria está disponível apenas no SQL Server 2012 e nas versões mais recentes.

### <a name="azure-active-directory"></a>Azure Active Directory

Autenticação do Azure AD é um mecanismo para se conectar ao banco de dados SQL v12 usando identidades no Azure AD. Use a autenticação do Azure AD para gerenciar de forma centralizada as identidades de usuários do banco de dados e como uma alternativa à autenticação do SQL Server. 

Você pode usar o JDBC Driver 6.0 para especificar suas credenciais do AD do Azure na cadeia de caracteres de conexão JDBC para se conectar ao banco de dados SQL. Para obter detalhes, consulte a propriedade de autenticação na [definindo as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md) artigo.

### <a name="table-valued-parameters"></a>Parâmetros com valor de tabela

Os TVPs fornecem uma maneira fácil de realizar marshaling em várias linhas de dados de um aplicativo cliente do SQL Server sem exigir várias viagens de ida e volta ou uma lógica especial do lado do servidor para processar os dados. Você pode usar os TVPs para encapsular linhas de dados em um aplicativo cliente e enviar os dados para o servidor em um único comando parametrizado. As linhas de dados de entrada são armazenadas em uma variável de tabela, em seguida, você pode operar em usando o Transact-SQL. Para obter detalhes, consulte [usando parâmetros com valor de tabela](../../connect/jdbc/using-table-valued-parameters.md).

### <a name="always-on-availability-groups"></a>Grupos de Disponibilidade AlwaysOn

O driver agora dá suporte a conexões transparentes para grupos de disponibilidade AlwaysOn. O driver descobre rapidamente a topologia Always On atual da infraestrutura de servidor e conecta-se ao servidor ativo atual de maneira transparente.

## <a name="42"></a>4.2

Microsoft JDBC Driver 4.2 para SQL Server é totalmente compatível com as especificações do JDBC 4.1 e 4.2. Os jars no pacote 4.2 são nomeados de acordo com sua conformidade com a versão de API do JDBC. Por exemplo, o arquivo sqljdbc42.jar do pacote 4.2 é compatível com JDBC API 4.2. Da mesma forma, o arquivo de sqljdbc41.jar está em conformidade com a API do JDBC 4.1.

Para garantir que você tem o direito sqljdbc42.jar ou arquivo sqljdbc41.jar, execute as seguintes linhas de código. Se a saída é "versão do Driver: 4.2.6420.100", você tem o pacote do JDBC Driver 4.2.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>Suporte para JDK 8

O driver dá suporte ao JDK versão 8.0, além de JDK 7.0, 6.0 e 5.0.

### <a name="jdbc-41-and-42-compliance"></a>Conformidade do JDBC 4.1 e 4.2

O driver é compatível com as especificações da API Java Database Connectivity 4.1 e 4.2, além da 4.0. Para obter detalhes, consulte [conformidade JDBC 4.1 para o Driver JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) e [conformidade JDBC 4.2 para o JDBC Driver](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).

### <a name="bulk-copy"></a>Cópia em massa

Você pode usar o recurso de cópia em massa para copiar rapidamente grandes quantidades de dados em tabelas ou em exibições nos bancos de dados do SQL Server. Para obter detalhes, confira [Usando uma cópia em massa com o JDBC Driver](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

### <a name="xa-transaction-rollback-option"></a>Opção de reversão de transação XA

O driver tem novas opções de tempo limite para reversão automática existente de transações não preparadas. Para obter detalhes, consulte [transações XA Noções básicas sobre](../../connect/jdbc/understanding-xa-transactions.md).

### <a name="new-kerberos-principal-connection-property"></a>Nova propriedade de conexão principal Kerberos

O driver usa uma nova propriedade de conexão para facilitar a flexibilidade com conexões Kerberos. Para obter detalhes, confira [Usando a autenticação integrada Kerberos para conectar-se ao SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).

## <a name="41"></a>4.1

### <a name="support-for-jdk-7"></a>Suporte para JDK 7

O driver dá suporte ao JDK versão 7.0, além de JDK 6.0 e 5.0.

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>O Itanium não é compatível com aplicativos do JDBC Driver 6.4, 6.0, 4.2 e 4.1

Não há suporte para execução de aplicativos Microsoft JDBC Drivers 6.4, 6.0, 4.2 e 4.1 for SQL Server em um computador Itanium.

## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)
