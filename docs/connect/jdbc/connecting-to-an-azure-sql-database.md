---
title: Conectar-se a um banco de dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2eef48c472ee9b23d941be88ae76cb0349067739
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66789343"
---
# <a name="connecting-to-an-azure-sql-database"></a>Conectando-se a um banco de dados SQL do Azure

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artigo aborda os problemas ocorridos no uso do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para conexão com um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]. Para obter mais informações sobre como se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], confira:  
  
- [Banco de Dados do SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)  
  
- [Como se conectar ao SQL Azure usando o JDBC](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)  

- [Conectar-se usando a Autenticação do Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>Detalhes

Ao se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], você deve se conectar ao banco de dados mestre para chamar **sqlserverdatabasemetadata. GetCatalogs**.  
O [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] não dá suporte ao retorno de todo o conjunto de catálogos em um banco de dados de usuário. **Sqlserverdatabasemetadata. GetCatalogs** usar a exibição de sys. Databases para obter os catálogos. Consulte a discussão de permissões no [sys. Databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) entender **sqlserverdatabasemetadata. GetCatalogs** comportamento em um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)].  
  
## <a name="connections-dropped"></a>Conexões removidas

Ao se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], as conexões ociosas podem ser terminadas por um componente de rede (como um firewall) após um período de inatividade. Existem dois tipos de conexões ociosas nesse contexto:  

- Ociosas na camada TCP, onde as conexões podem ser removidas por qualquer número de dispositivos de rede.  

- Ociosas pelo Gateway do SQL Azure, no qual as mensagens **keepalive** do TCP podem ocorrer (tornando a conexão não ociosa de uma perspectiva do TCP), mas sem uma consulta ativa em 30 minutos. Nesse cenário, o Gateway determina se a conexão TDS é ociosa em 30 minutos e termina a conexão.  
  
Para evitar a remoção de conexões ociosas por um componente de rede, as configurações do Registro a seguir (ou seus equivalentes em ambientes não Windows) devem ser definidas no sistema operacional no qual o driver foi carregado:  
  
|Configuração do Registro|Valor recomendado|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveInterval|1\.000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ TcpMaxDataRetransmissions|10|  
  
Reinicie o computador para que as configurações do Registro tenham efeito.  

Para obter esse efeito no Windows Azure, crie uma tarefa de inicialização para adicionar as chaves do Registro.  Por exemplo, adicione a tarefa de inicialização abaixo ao arquivo de definição de serviço:  

```xml
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```

Depois adicione um arquivo AddKeepAlive.cmd file ao seu projeto. Defina a configuração "Copiar para Diretório de Saída" para Copiar sempre. A seguir, há um exemplo de arquivo AddKeepAlive.cmd:  

```bat
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```

## <a name="appending-the-server-name-to-the-userid-in-the-connection-string"></a>Anexando o nome do servidor à ID de usuário na cadeia de conexão  

Antes da versão 4.0 do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ao se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], era necessário acrescentar o nome do servidor à ID de usuário na cadeia de conexão. Por exemplo, user@servername. A partir da versão 4.0 do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], não é mais necessário acrescentar @servername à ID de usuário na cadeia de conexão.  

## <a name="using-encryption-requires-setting-hostnameincertificate"></a>Uso de criptografia requer a configuração de hostNameInCertificate

Antes da versão 7.2 do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ao se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], você deve especificar **hostNameInCertificate** se você especificar **criptografar = true** (se o nome do servidor em que a conexão cadeia de caracteres é *shortName*. *domainName*, defina a **hostNameInCertificate** propriedade \*. *domainName*.). Essa propriedade é opcional a partir da versão 7.2 do driver.

Por exemplo:

```java
jdbc:sqlserver://abcd.int.mscds.com;databaseName=myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate=*.int.mscds.com;
```

## <a name="see-also"></a>Consulte Também

[Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
