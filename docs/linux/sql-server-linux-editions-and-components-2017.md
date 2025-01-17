---
title: Edições e recursos com suporte do SQL Server 2017 ~ Linux
ms.date: 09/14/2017
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- default components
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: 5955406abee1c7557a920d45d1280c7ab23199d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077304"
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>Edições e recursos compatíveis do SQL Server 2017 no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo fornece detalhes dos recursos suportados pelas várias edições do SQL Server 2017 no Linux. Para as edições e recursos com suporte do SQL Server no Windows, consulte [SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md).  
  
Os requisitos de instalação variam de acordo com as necessidades do aplicativo. As diferentes edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] acomodam desempenho, tempo de execução e requisitos de preço exclusivos para organizações e indivíduos. Os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que você instala dependem também dos seus requisitos específicos. As seções a seguir ajudarão você a entender como fazer a melhor escolha entre as edições e os componentes disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

Para notas de versão mais recentes e informações sobre novidades, consulte o seguinte:
- [Notas de versão do SQL Server no Linux](sql-server-linux-release-notes.md)
- [O que há de novo no SQL Server no Linux](sql-server-linux-whats-new.md)

Para obter uma lista dos recursos do SQL Server não está disponíveis no Linux, consulte [recursos sem suporte e serviços](sql-server-linux-release-notes.md#Unsupported).

### <a name="try-sql-server"></a>Experimente o SQL Server.    
    
[Baixar o SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>Edições do[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]  
 A tabela a seguir descreve essas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edição|Definição|  
|---------------------------------------|----------------|  
|Enterprise|A oferta premium, [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise edition fornece recursos de datacenter abrangentes de alta tecnologia com desempenho incrivelmente rápido habilitando altos níveis de serviço para cargas de trabalho de missão crítica.|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard edition oferece o gerenciamento de dados básicos para departamentos e pequenas empresas executarem seus aplicativos e dá suporte a ferramentas de desenvolvimento comuns no local e na nuvem – permitindo o gerenciamento de banco de dados eficiente com mínimos recursos de TI.|  
|Web|A edição[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web é uma opção de baixo custo total de propriedade para hospedagem de sites e VAPs da Web que fornece recursos de escalabilidade, economia e capacidade de gerenciamento para propriedades da Web de pequeno a grande porte.|  
|Desenvolvedor|A edição[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer permite que os desenvolvedores criem qualquer tipo de aplicativo com base no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ele inclui todas as funcionalidades da edição Enterprise, mas é licenciado para ser usado como um sistema de teste e desenvolvimento, e não como um servidor de produção. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer é uma opção ideal para pessoas que criam e testam aplicativos.|  
|Express edition|A edição Express é o banco de dados gratuito de nível de entrada, ideal para conhecer e criar aplicativos de área de trabalho e aplicativos controlados por dados de pequenos servidores. É a melhor escolha para fornecedores de software independente, desenvolvedores e interessados que criam aplicativos cliente. Se precisar de recursos mais avançados de banco de dados, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express pode ser perfeitamente atualizado para versões mais sofisticadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Usando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com aplicativos cliente/servidor  

Você pode instalar apenas os componentes cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador que esteja executando aplicativos cliente/servidor que se conectam diretamente a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A instalação dos componentes cliente é também uma boa opção se você administra uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um servidor de banco de dados ou se planeja desenvolver aplicativos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] componentes  

SQL Server 2017 no Linux dá suporte ao mecanismo de banco de dados do SQL Server. A tabela a seguir descreve os recursos no mecanismo de banco de dados.   
  
|Componentes de servidor|Descrição|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] inclui o [!INCLUDE[ssDE](../includes/ssde-md.md)], o serviço principal para armazenamento, processamento e segurança de dados, replicação, pesquisa de texto completo, ferramentas para gerenciar relacionais e dados XML e na integração da análise de banco de dados.|  

**Edições Developer, Enterprise Core e avaliação**  
Para recursos com suporte, Enterprise Core, edições Developer e Evaluation, consulte os recursos listados para o SQL Server Enterprise edition nas tabelas a seguir.

A Developer edition continua a dar suporte a apenas um cliente para o [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md). 
  
##  <a name="Cross-BoxScaleLimits"></a> Limites de escala  
  
|Recurso|Enterprise|Standard|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos| 
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|
|Memória máxima para o pool de buffers por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Máximo do sistema operacional|128 GB|64 GB|1410 MB|
|Máximo de memória para cache do segmento Columnstore por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB| 16 GB| 352 MB|  
|Tamanho de dados máximo otimizado para memória de acordo com banco de dados em [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB| 16 GB| 352 MB|
|Tamanho máximo do banco de dados relacional|524 PB|524 PB|524 PB|10 GB|  
  
<sup>1</sup> Enterprise edition with Server + cliente acesso licenciamento CAL (licença) com base (não disponível para novos contratos) é limitado a um máximo de 20 núcleos por instância do SQL Server. Não há limites no modelo de Licenciamento de Servidor Baseado em Núcleo. Para obter mais informações, consulte [computar limites de capacidade por edição do SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="RDBMSHA"></a> Alta Disponibilidade do RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|Envio de logs|Sim|Sim|Sim|Não|  
|Compactação de backup|Sim|Sim|Não|Não| 
|Instantâneo do banco de dados|Sim|Não|Não|Não|
|Instância de cluster de failover do AlwaysOn<sup>1</sup>|Sim|Sim|Não|Não| 
|Grupos de disponibilidade Always On<sup>2</sup>|Sim|Não|Não|Não|
|Grupos de disponibilidade básicos <sup>3</sup>|Não|Sim|Não|Não|
|Configuração de grupos de disponibilidade de confirmação de réplica mínima|Sim|Sim|Não|Não|
|Grupo de disponibilidade sem cluster|Sim|Sim|Não|Não|
|Restauração de arquivo e página online|Sim|Não|Não|Não|
|Indexação online|Sim|Não|Não|Não|
|Recompilações de índice online retomáveis|Sim|Não|Não|Não|
|Alteração de esquema online|Sim|Não|Não|Não|
|Recuperação rápida|Sim|Não|Não|Não|
|Backups espelhados|Sim|Não|Não|Não|
|Adição de memória a quente e CPU|Sim|Não|Não|Não|
|Backup criptografado|Sim|Sim|Não|Não|
|Backup híbrido para o Microsoft Azure (backup para URL)|Sim|Sim|Não|Não|
  
<sup>1</sup> na Enterprise edition, o número de nós é o máximo do sistema operacional. Na Standard Edition, há suporte para dois nós. 

<sup>2</sup> na Enterprise edition, fornece suporte para até 8 réplicas secundárias, incluindo 2 réplicas secundárias síncronas. 

<sup>3</sup> standard edition oferece suporte a grupos de disponibilidade básicos. Um grupo de disponibilidade básico dá suporte a duas réplicas, com um banco de dados. Para obter mais informações sobre grupos de disponibilidade básicos, consulte [Grupos de Disponibilidade Básicos](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).    

##  <a name="RDBMSSP"></a> Escalabilidade e desempenho do RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|Columnstore <sup>1</sup>|Sim|Sim|Sim|Sim|  
|Binários de objeto grandes em índices columnstore clusterizados|Sim|Sim|Sim|Sim|  
|Recompilação de índice columnstore não clusterizado online|Sim|Não|Não|Não|
|OLTP na memória <sup>1</sup>|Sim|Sim|Sim|Sim|
|Memória principal persistente|Sim|Sim|Sim|Sim|
|Particionamento de tabela e índice|Sim|Sim|Sim|Sim|  
|Compactação de dados|Sim|Sim|Sim|Sim|
|Administrador de Recursos|Sim|Não|Não|Não|  
|Paralelismo de tabela particionada|Sim|Não|Não|Não|
|Memória de página grande com reconhecimento para NUMA e alocação de matriz de buffer|Sim|Não|Não|Não|
|Administração do recurso de E/S|Sim|Não|Não|Não|  
|Durabilidade atrasada|Sim|Sim|Sim|Sim|
|Ajuste Automático|Sim|Não|Não|Não|
|Junções Adaptáveis de Modo de Lote|Sim|Não|Não|Não|
|Comentários de Concessão de Memória do Modo de Lote|Sim|Não|Não|Não|
|Execução Intercalada para Funções com Valor de Tabela de Várias Instruções|Sim|Sim|Sim|Sim|
|Aprimoramentos de inserção em massa|Sim|Sim|Sim|Sim|


<sup>1</sup> Tamanho de dados de OLTP na memória e cache do segmento Columnstore são limitados a quantidade de memória especificada por edição na seção limites de escala. Os graus de máximos de paralelismo é limitado. Os graus de paralelismo (DOP) do processo de criação de um índice é limitado a 2 DOP para a Standard edition e 1 DOP para as edições Web e Express. Refere-se a índices de columnstore criados em tabelas baseadas em disco e tabelas com otimização de memória.

##  <a name="RDBMSS"></a> Segurança do RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|Segurança em nível de linha|Sim|Sim|Sim|Sim|  
|Sempre Criptografado|Sim|Sim|Sim|Sim| 
|Mascaramento de dados dinâmicos|Sim|Sim|Sim|Sim|   
|Auditoria básica|Sim|Sim|Sim|Sim| 
|Auditoria refinada|Sim|Sim|Sim|Sim| 
|Criptografia transparente do banco de dados|Sim|Não|Não|Não|   
|Funções definidas pelo usuário|Sim|Sim|Sim|Sim| 
|Bancos de dados independentes|Sim|Sim|Sim|Sim| 
|Criptografia para backups|Sim|Sim|Não|Não|  

##  <a name="RDBMSM"></a> Gerenciamento RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|Conexão dedicada de administrador|Sim|Sim|Sim|Sim, com o sinalizador de rastreamento|Sim, com o sinalizador de rastreamento|   
|Suporte de scripts PowerShell|Sim|Sim|Sim|Sim| 
|Suporte para operações de componente do aplicativo da camada de dados – extrair, implantar, atualizar, excluir|Sim|Sim|Sim|Sim| 
|Automação de política (verificação de agenda e alterações)|Sim|Sim|Sim|Não|Não|   
|Coletor de dados de desempenho|Sim|Sim|Sim|Não|Não| 
|Relatórios de desempenho padrão|Sim|Sim|Sim|Não|Não| 
|Guias de plano e planejar congelamento para guias de plano|Sim|Sim|Sim|Não|Não|   
|Direcione a consulta de exibições indexadas (usando a dica de NOEXPAND)|Sim|Sim|Sim|Sim| 
|Manutenção automática de exibições indexadas|Sim|Sim|Sim|Não|Não| 
|Exibições particionadas distribuídas|Sim|Não|Não|Não| 
|Operações indexadas paralelas|Sim|Não|Não|Não|  
|Uso automático da exibição indexada através do otimizador de consulta|Sim|Não|Não|Não| 
|Verificação de consistência paralela|Sim|Não|Não|Não| 
|Ponto de controle do Utilitário do SQL Server|Sim|Não|Não|Não|    

##  <a name="Programmability"></a> Programmability  
  
|Recurso|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|Sim|Sim|Sim|Sim|   
|Repositório de Consultas|Sim|Sim|Sim|Sim|   
|Temporal|Sim|Sim|Sim|Sim|   
|Suporte a XML nativo|Sim|Sim|Sim|Sim| 
|Indexação XML|Sim|Sim|Sim|Sim| 
|Funcionalidades MERGE e UPSERT|Sim|Sim|Sim|Sim|   
|Tipos de dados de Data e Hora|Sim|Sim|Sim|Sim|  
|Suporte à internacionalização|Sim|Sim|Sim|Sim| 
|Pesquisa semântica e de texto completo|Sim|Sim|Sim|Sim|Não| 
|Especificação de idioma em consulta|Sim|Sim|Sim|Sim|Não|   
|Service Broker (mensagens)|Sim|Sim|Não (Somente cliente)|Não (Somente cliente)|Não (Somente cliente)|   
|pontos de extremidade Transact-SQL|Sim|Sim|Sim|Não|Não| 
|Gráfico|Sim|Sim|Sim|Sim|  


<sup>1</sup> Expansão com vários nós de computação requer um nó de cabeçalho.

## <a name="IS"></a> Integration Services

Para obter informações sobre os recursos do Integration Services (SSIS) com suporte nas edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [recursos do Integration Services compatíveis com as edições do SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="SLS"></a> Serviços espaciais e de localização  
  
|Nome do recurso|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciais|Sim|Sim|Sim|Sim|   
|Tipos de dados planares e geodésicos|Sim|Sim|Sim|Sim| 
|Bibliotecas espaciais avançadas|Sim|Sim|Sim|Sim|   
|Importação/exportação de formatos de dados espaciais padrão da indústria|Sim|Sim|Sim|Sim|   

  
## <a name="next-steps"></a>Próximas etapas 
 [Edições e recursos com suporte do SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [Edições e recursos com suporte do SQL Server 2016 - Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [Edições e recursos com suporte do SQL Server 2014 - Windows](https://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [Instalação do SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [Especificações de produto do SQL Server](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb) 

  
  
