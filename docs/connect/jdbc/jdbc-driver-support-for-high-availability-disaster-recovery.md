---
title: Suporte a JDBC driver para alta disponibilidade e recuperação de desastre | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6e760523026251463f80d7f7e3e14b7e52b36ab2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781541"
---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>Suporte a JDBC driver para alta disponibilidade e recuperação de desastre
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Este tópico aborda o suporte do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para alta disponibilidade, recuperação de desastre – [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]. Para obter mais informações sobre o [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], consulte os Manuais Online do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] .  
  
 Com a versão 4.0 do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], é possível especificar o ouvinte do grupo de disponibilidade de um AG (grupo de disponibilidade) (alta disponibilidade, recuperação de desastre) na propriedade de conexão. Se um aplicativo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] estiver conectado a um banco de dados AlwaysOn que efetua failover, a conexão original será interrompida e o aplicativo deverá abrir uma nova conexão para continuar o trabalho após o failover. As seguintes [propriedades de conexão foram](../../connect/jdbc/setting-the-connection-properties.md) adicionadas ao [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]:  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
Especifique multiSubnetFailover=true ao se conectar ao ouvinte do grupo de disponibilidade de um grupo de disponibilidade ou uma instância de cluster de failover. Observe que **multiSubnetFailover** é false por padrão. Use **applicationIntent** para declarar o tipo de carga de trabalho do aplicativo. Consulte as seções abaixo para obter mais detalhes.
 
Começando na versão 6.0 do Microsoft JDBC Driver para SQL Server, uma nova propriedade de conexão **transparentNetworkIPResolution** (TNIR) é adicionado para conexão transparente aos grupos de disponibilidade Always On ou para um servidor que tem vários endereços IP associados. Quando **transparentNetworkIPResolution** for true, o driver tenta se conectar ao primeiro endereço IP. Se a primeira tentativa falhar, o driver tenta se conectar a todos os endereços IP em paralelo, até que o tempo limite expirar, descartando qualquer tentativa de conexão pendente quando um deles é bem-sucedida.   

Observe que:
* transparentNetworkIPResolution é verdadeiro por padrão
* transparentNetworkIPResolution será ignorado se multiSubnetFailover for true
* transparentNetworkIPResolution será ignorado se o espelhamento de banco de dados é usado
* transparentNetworkIPResolution será ignorado se houver mais de 64 endereços IP
* Quando transparentNetworkIPResolution for true, a primeira tentativa de conexão usa um valor de tempo limite de 500 ms. O restante das tentativas de conexão seguem a mesma lógica do recurso de multiSubnetFailover. 

> [!NOTE]
> Se você estiver usando o Microsoft JDBC Driver 4.2 (ou diminuir) para o SQL Server e se **multiSubnetFailover** é false, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] tenta se conectar ao primeiro endereço IP. Se o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não puder estabelecer uma conexão com o primeiro endereço IP, a conexão apresentará falha. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] não tentará se conectar a nenhum endereço IP subsequente associado ao servidor. 
> 
> 
> [!NOTE]
>  O aumento do tempo limite de conexão e a implementação de lógica de repetição de conexão aumentarão a probabilidade de um aplicativo se conectar a um grupo de disponibilidade. Além disso, como uma conexão pode falhar devido a um failover de grupo de disponibilidade, você deve implementar lógica de repetição de conexão, repetindo uma conexão com falha até se reconectar.  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>Conectando-se ao MultiSubnetFailover  
 Sempre especifique **multiSubnetFailover=True** ao se conectar ao ouvinte de um grupo de disponibilidade do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou a uma instância de cluster de failover do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. **multiSubnetFailover** permite o failover mais rápido para todos os Grupos de Disponibilidade e instâncias de cluster de failover no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e reduzirá significativamente o tempo de failover para topologias AlwaysOn de uma ou várias sub-redes. Durante um failover de várias sub-redes, o cliente tentará conexões em paralelo. Durante um failover de sub-rede, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] repetirá agressivamente a conexão TCP.  
  
 A propriedade de conexão **multiSubnetFailover** indica que o aplicativo está sendo implantado em um grupo de disponibilidade ou instância de cluster de failover e que o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] tentará se conectar ao banco de dados na instância primária do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentando se conectar a todos os endereços IP do grupo de disponibilidade. Quando **MultiSubnetFailover=true** é especificado para uma conexão, o cliente repete as tentativas de conexão TCP mais rapidamente do que os intervalos de retransmissão TCP padrão do sistema operacional. Isto permite uma reconexão mais rápida depois de failover de um Grupo de disponibilidade AlwaysOn ou uma Instância de Cluster de Failover AlwaysOn e é aplicável a Grupos de disponibilidade único e de várias sub-redes e Instâncias de Cluster de Failover.  
  
 Para obter mais informações sobre palavras-chave de cadeia de caracteres de conexão na [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 A especificação de **multiSubnetFailover=true** durante a conexão a algo que não seja um ouvinte de grupo de disponibilidade ou uma Instância de Cluster de Failover pode resultar em um impacto de desempenho negativo e isso não é compatível.  
  
 Se o gerenciador de segurança não for instalado, a Máquina Virtual Java armazenará VIPs (endereços IP virtuais) em cache por um período determinado, por padrão, definido pela implementação JDK e as propriedades Java networkaddress.cache.ttl e networkaddress.cache.negative.ttl. Se o gerenciador de segurança JDK for instalado, a Máquina Virtual Java armazenará VIPs em cache e não atualizará o cache, por padrão. Você deve definir a "vida útil" (networkaddress.cache.ttl) para um dia no cache da Máquina Virtual Java. Se você não alterar o valor padrão para um dia (ou valor parecido), o valor antigo não será limpo no cache da Máquina Virtual Java quando um VIP for adicionado ou atualizado. Para obter mais informações sobre networkAddress e networkAddress, consulte [ https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html ](https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html).  
  
 Use as diretrizes a seguir para conectar-se a um servidor em um grupo de disponibilidade ou Instância de Cluster de Failover:  
  
-   O driver gerará um erro se o **nome_da_instância** propriedade de conexão é usada na mesma cadeia de conexão como o **multiSubnetFailover** propriedade de conexão. Isso acontece porque o Navegador SQL não é usado em um grupo de disponibilidade. No entanto, se o **portNumber** propriedade de conexão também for especificada, o driver ignorará **instanceName** e use **portNumber**.  
  
-   Use a propriedade de conexão **multiSubnetFailover** quando estiver se conectando a uma ou várias sub-redes, isso melhorará o desempenho em ambos os casos.  
  
-   Para conectar-se a um grupo de disponibilidade, especifique o ouvinte do grupo de disponibilidade como o servidor em sua cadeia de conexão. Por exemplo, jdbc:sqlserver://VNN1.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada com mais de 64 endereços IP causará uma falha de conexão.  
  
-   O comportamento de um aplicativo que usa a propriedade de conexão **multiSubnetFailover** não é afetado com base no tipo de autenticação: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticação, Autenticação Kerberos ou Autenticação do Windows.  
  
-   Aumente o valor de **loginTimeout** para acomodar o tempo de failover e reduzir as tentativas de repetição de conexão do aplicativo.  
  
-   Não há suporte a transações distribuídas.  
  
 Se o roteamento somente leitura não estiver em ação, conectar-se a um local de réplica secundária em um grupo de disponibilidade apresentará falha nas seguintes situações:  
  
1.  Se o local de réplica secundário não for configurado para aceitar conexões.  
  
2.  Se um aplicativo usar **applicationIntent=ReadWrite** (discutido abaixo) e o local de réplica secundária estiver configurado para acesso somente leitura.  
  
 Uma conexão falhará se uma réplica primária for configurada para rejeitar cargas de trabalho somente leitura e a cadeia de conexão contiver **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Atualizando para usar clusters de várias sub-redes a partir do espelhamento de banco de dados  
 Se você atualizar um aplicativo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] que atualmente usa o espelhamento de banco de dados em um cenário de várias sub-redes, deverá remover a propriedade de conexão **failoverPartner** e substituí-la por **multiSubnetFailover** definido como **true** e substituir o nome do servidor da cadeia de conexão por um ouvinte de grupo de disponibilidade. Se uma cadeia de conexão usa **failoverPartner** e **multiSubnetFailover=true**, o driver gerará um erro. No entanto, se uma cadeia de conexão usar **failoverPartner** e **multiSubnetFailover=false** (ou **ApplicationIntent=ReadWrite**), o aplicativo usará o espelhamento de banco de dados.  
  
 O driver retornará um erro se o espelhamento de banco de dados for usado no banco de dados primário no AG e se **multiSubnetFailover=true** for usado na cadeia de conexão que se conecta a um banco de dados primário, em vez de ao ouvinte do grupo de disponibilidade.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>Novos métodos que oferecem suporte a multiSubnetFailover e applicationIntent  
 Os seguintes métodos oferecem acesso programático para o **multiSubnetFailover**, **applicationIntent** e **transparentNetworkIPResolution** cadeia de caracteres de conexão palavras-chave:  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 O **getMultiSubnetFailover**, **setMultiSubnetFailover**, **getApplicationIntent**, **setApplicationIntent**, **getTransparentNetworkIPResolution** e **setTransparentNetworkIPResolution** métodos também são adicionados à [classe SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [ Classe SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), e [classe SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
## <a name="ssl-certificate-validation"></a>Validação do certificado SSL  
 Um grupo de disponibilidade consiste em vários servidores físicos. Suporte adicionado [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] para **Nome Alternativo da Entidade** nos certificados SSL para que vários hosts possam ser associados ao mesmo certificado. Para obter mais informações sobre o SSL, consulte [Noções básicas sobre suporte a SSL](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [Configurando as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
