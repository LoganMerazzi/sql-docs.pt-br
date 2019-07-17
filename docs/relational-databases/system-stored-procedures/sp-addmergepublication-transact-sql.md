---
title: sp_addmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords:
- sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c6571ce334c1534dd6fe869f37f007da793469d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118046"
---
# <a name="spaddmergepublication-transact-sql"></a>sp_addmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma nova publicação de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados que está sendo publicado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergepublication [ @publication = ] 'publication'   
    [ , [ @description = ] 'description'   
    [ , [ @retention = ] retention ]   
    [ , [ @sync_mode = ] 'sync_mode' ]   
    [ , [ @allow_push = ] 'allow_push' ]   
    [ , [ @allow_pull = ] 'allow_pull' ]   
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]   
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]   
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @dynamic_filters = ] 'dynamic_filters' ]   
    [ , [ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder' ]   
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @pre_snapshot_script = ] 'pre_snapshot_script' ]   
    [ , [ @post_snapshot_script = ] 'post_snapshot_script' ]   
    [ , [ @compress_snapshot = ] 'compress_snapshot' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]   
    [ , [ @conflict_retention = ] conflict_retention ]   
    [ , [ @keep_partition_changes = ] 'keep_partition_changes' ]   
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]   
    [ , [ @allow_synctoalternate = ] 'allow_synctoalternate' ]   
    [ , [ @validate_subscriber_info = ] 'validate_subscriber_info' ]   
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]   
    [ , [ @max_concurrent_merge = ] maximum_concurrent_merge ]   
    [ , [ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots ]  
    [ , [ @use_partition_groups = ] 'use_partition_groups' ]  
    [ , [ @publication_compatibility_level = ] 'backward_comp_level' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot' ]   
    [ , [ @allow_web_synchronization = ] 'allow_web_synchronization' ]   
    [ , [ @web_synchronization_url = ] 'web_synchronization_url' ]  
    [ , [ @allow_partition_realignment = ] 'allow_partition_realignment' ]  
    [ , [ @retention_period_unit = ] 'retention_period_unit' ]  
    [ , [ @generation_leveling_threshold = ] generation_leveling_threshold ]  
    [ , [ @automatic_reinitialization_policy = ] automatic_reinitialization_policy ]  
    [ , [ @conflict_logging = ] 'conflict_logging' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação de mesclagem para criar. *publicação* está **sysname**, sem padrão e deve não ser a palavra-chave todos. O nome da publicação deve ser exclusivo no banco de dados.  
  
`[ @description = ] 'description'` É a descrição da publicação. *Descrição* está **nvarchar (255)** , com um padrão NULL.  
  
`[ @retention = ] retention` É o período de retenção na retenção de unidades de período, para o qual salvar as alterações para o determinado *publicação*. *retenção* está **int**, com um padrão de 14 unidades. Unidades de período de retenção são definidas por *retention_period_unit*. Se a assinatura não estiver sincronizada dentro do período de retenção e as alterações pendentes que por ventura tenha recebido tiverem sido removidas por uma operação de limpeza no Distribuidor, a assinatura irá expirar e deverá ser reiniciada. O período de retenção máximo permitido é o número de dias entre 31 de dezembro, 9999 e a data atual.  
  
> [!NOTE]  
>  O período de retenção para publicações de mesclagem tem um período de tolerância de 24 horas para acomodar Assinantes em fusos horários diferentes. Por exemplo, se você definir um período de retenção de um dia, o período de retenção real será de 48 horas.  
  
`[ @sync_mode = ] 'sync_mode'` É o modo de sincronização inicial de assinantes na publicação. *sync_mode* está **nvarchar (10)** , e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**nativo** (padrão)|Produz saída de programa de cópia em massa em modo nativo de todas as tabelas.|  
|**character**|Produz saída de programa de cópia em massa em modo de caractere de todas as tabelas. Necessário para dar suporte à [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] e não-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes.|  
  
`[ @allow_push = ] 'allow_push'` Especifica se podem ser criadas assinaturas push para a publicação determinada. *allow_push* está **nvarchar (5)** , com um padrão de TRUE, que permite assinaturas push na publicação.  
  
`[ @allow_pull = ] 'allow_pull'` Especifica se podem ser criadas assinaturas pull para a publicação determinada. *allow_pull* está **nvarchar (5)** , com um padrão de TRUE, que permite assinaturas pull na publicação. Você deve especificar verdadeiro para dar suporte [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes.  
  
`[ @allow_anonymous = ] 'allow_anonymous'` Especifica se podem ser criadas assinaturas anônimas para a publicação determinada. *allow_anonymous* está **nvarchar (5)** , com um padrão de TRUE, que permite assinaturas anônimas na publicação. Para dar suporte à [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes, você deve especificar **verdadeiro**.  
  
`[ @enabled_for_internet = ] 'enabled_for_internet'` Especifica se a publicação está habilitada para a Internet e determina se o protocolo de transferência de arquivo (FTP) pode ser usado para transferir os arquivos de instantâneo para um assinante. *enabled_for_internet* está **nvarchar (5)** , com um padrão de FALSE. Se **verdadeira**, os arquivos de sincronização para a publicação são colocados no diretório C:\Program Files\Microsoft SQL server\mssql\mssql.x\repldata\ftp. O usuário deve criar o diretório Ftp. Se **falsos**, a publicação não está habilitada para acesso à Internet.  
  
`[ @centralized_conflicts = ] 'centralized_conflicts'` Esse parâmetro foi preterido e só tem suporte para a compatibilidade com versões anteriores de scripts. Use *conflict_logging* para especificar o local onde os registros de conflito são armazenados.  
  
`[ @dynamic_filters = ] 'dynamic_filters'` Permite que a publicação de mesclagem use filtros de linha com parâmetros. *dynamic_filters* está **nvarchar (5)** , com um padrão de FALSE.  
  
> [!NOTE]  
>  Você não deve especificar esse parâmetro mas, em vez disso, permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine se filtros de linha com parâmetros estão sendo usado usados. Se você especificar um valor de **verdadeira** para *dynamic_filters*, você deve definir um filtro de linha com parâmetros para o artigo. Para obter mais informações, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
`[ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'` Especifica se os arquivos de instantâneo são armazenados na pasta padrão. *snapshot_in_default_folder* está **nvarchar (5)** , com um padrão de TRUE. Se **verdadeira**, arquivos de instantâneo podem ser encontrados na pasta padrão. Se **falsos**, os arquivos de instantâneo serão armazenados no local alternativo especificado por *alternate_snapshot_folder*. Os locais alternativos podem ser um outro servidor, uma unidade de rede ou uma mídia removível (como um CD-ROM ou discos removíveis). Você também pode salvar os arquivos de instantâneo em um site de FTP para recuperação posterior pelo Assinante. Observe que esse parâmetro pode ser verdadeiro e ainda ter um local especificado por *alt_snapshot_folder*. Essa combinação Especifica que os arquivos de instantâneo serão armazenados em ambos os locais padrão e alternativo.  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'` Especifica o local da pasta alternativa para o instantâneo. *alternate_snapshot_folder* está **nvarchar (255)** , com um padrão NULL.  
  
`[ @pre_snapshot_script = ] 'pre_snapshot_script'` Especifica um ponteiro para um **. SQL** local do arquivo. *pre_snapshot_script* está **nvarchar (255)** , com um padrão NULL. O Agente de Mesclagem executará o script pré-instantâneo antes de qualquer script de objeto replicado ao aplicar o instantâneo no Assinante. O script é executado no contexto de segurança usado pelo Agente de Mesclagem ao se conectar ao banco de dados de assinatura. Não são executados scripts de pré-instantâneo em [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes.  
  
`[ @post_snapshot_script = ] 'post_snapshot_script'` Especifica um ponteiro para um **. SQL** local do arquivo. *post_snapshot_script* está **nvarchar (255)** , com um padrão NULL. O Agente de Mesclagem executará o script pós-instantâneo depois que todos os outros scripts de objeto replicado tenham sido aplicados durante uma sincronização inicial. O script é executado no contexto de segurança usado pelo Agente de Mesclagem ao se conectar ao banco de dados de assinatura. Não são executados scripts de pós-instantâneo em [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes.  
  
`[ @compress_snapshot = ] 'compress_snapshot'` Especifica que o instantâneo gravado para o **@alt_snapshot_folder** local deve ser compactado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] formato CAB. *compress_snapshot* está **nvarchar (5)** , com um padrão de FALSE. **False** Especifica que o instantâneo não será compactado; **verdadeira** Especifica que o instantâneo deve ser compactado. Arquivos de instantâneo maiores que 2 GB não podem ser compactados. Arquivos de instantâneo compactados são descompactados no local onde o Agente de Mesclagem é executado; as assinaturas pull são geralmente usadas com instantâneos compactados para que os arquivos sejam descompactados no Assinante. O instantâneo na pasta padrão não pode ser compactado. Para dar suporte à [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes, você deve especificar **falso**.  
  
`[ @ftp_address = ] 'ftp_address'` É o endereço de rede do serviço FTP para o distribuidor. *ftp_address* está **sysname**, com um padrão NULL. Especifica onde os arquivos de instantâneo de publicação ficam localizados para o agente de mesclagem de um assinante para acompanhar. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter outro *ftp_address*. A publicação deve oferecer suporte à propagação de instantâneos por meio de FTP.  
  
`[ @ftp_port = ] ftp_port` É o número da porta do serviço FTP para o distribuidor. *ftp_port* está **int**, com um padrão de 21. Especifica onde os arquivos de instantâneo de publicação ficam localizados para serem captados pelo Agente de Mesclagem ou por um Assinante. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter seu próprio *ftp_port*.  
  
`[ @ftp_subdirectory = ] 'ftp_subdirectory'` Especifica onde os arquivos de instantâneo estarão disponíveis para o Merge Agent do assinante para acompanhar se a publicação oferece suporte à propagação de instantâneo usando FTP. *ftp_subdirectory* está **nvarchar (255)** , com um padrão NULL. Como essa propriedade é armazenada para cada publicação, cada publicação pode ter seu próprio *ftp_subdirctory* ou optar por não ter um subdiretório indicado com um valor nulo.  
  
 Na pré-geração de instantâneos para publicação com filtros com parâmetros, o instantâneo de dados de cada partição de Assinante precisa estar em sua própria pasta. A estrutura de diretório para instantâneos pré-gerados por meio de FTP deve seguir a estrutura a seguir:  
  
 *alternate_snapshot_folder*\ftp\\*publisher_publicationDB_publication*\\*partitionID*.  
  
> [!NOTE]  
>  Os valores acima em itálico dependerão das especificações da publicação e da partição de Assinante.  
  
`[ @ftp_login = ] 'ftp_login'` O nome de usuário é usado para se conectar ao serviço FTP. *ftp_login* está **sysname**, com um padrão de 'anonymous'.  
  
`[ @ftp_password = ] 'ftp_password'` A senha do usuário é usada para se conectar ao serviço FTP. *ftp_password* está **sysname**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte.  
  
`[ @conflict_retention = ] conflict_retention` Especifica o período de retenção em dias, para o qual os conflitos são retidos. *conflict_retention* está **int**, com um padrão de 14 dias antes do conflito de linha é limpo da tabela de conflitos.  
  
`[ @keep_partition_changes = ] 'keep_partition_changes'` Especifica se é para habilitar otimizações de alteração de partição quando partições pré-computadas não podem ser usadas. *keep_partition_changes* está **nvarchar (5)** , com um padrão de TRUE. **False** significa que as alterações de partição não é otimizadas e quando partições pré-computadas não forem usadas, as partições enviadas a todos os assinantes serão verificadas quando os dados forem alterados em uma partição. **True** significa que as alterações de partição é otimizadas e somente assinantes com linhas nas partições alteradas são afetados. Ao usar partições pré-computadas, defina *use_partition_groups* à **verdadeiro** e defina *keep_partition_changes* para **false**. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
> [!NOTE]  
>  Se você especificar um valor de **verdadeira** para *keep_partition_changes*, especifique um valor de **1** para o parâmetro do agente de instantâneo **- MaxNetworkOptimization** . Para obter mais informações sobre esse parâmetro, consulte [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md). Para obter informações sobre como especificar parâmetros de agente, consulte [administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
 Com o [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes *keep_partition_changes* deve ser definido como true para assegurar que as exclusões são propagadas corretamente. Quando definido como falso, o assinante pode ter mais linhas do que o esperado.  
  
`[ @allow_subscription_copy = ] 'allow_subscription_copy'` Habilita ou desabilita a capacidade de copiar os bancos de dados de assinatura que assinam essa publicação. *allow_subscription_copy* está **nvarchar (5)** , com um padrão de FALSE. O tamanho do banco de dados de assinatura copiado deve ser menor de 2 gigabytes (GB).  
  
`[ @allow_synctoalternate = ] 'allow_synctoalternate'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @validate_subscriber_info = ] 'validate_subscriber_info'` Lista as funções que são usadas para definir uma partição de assinante dos dados publicados quando filtros de linha com parâmetros são usados. *validate_subscriber_info* está **nvarchar(500)** , com um padrão NULL. Essa informação é usada pelo Agente de Mesclagem para validar a partição do Assinante. Por exemplo, se [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) é usado no filtro de linha com parâmetros, o parâmetro deve ser `@validate_subscriber_info=N'SUSER_SNAME()'`.  
  
> [!NOTE]  
>  Você não deve especificar esse parâmetro, mas sim permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine automaticamente os critérios de filtragem.  
  
`[ @add_to_active_directory = ] 'add_to_active_directory'` Esse parâmetro foi preterido e só tem suporte para a compatibilidade com versões anteriores de scripts. Você não pode mais adicionar informações de publicação ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory.  
  
`[ @max_concurrent_merge = ] maximum_concurrent_merge` O número máximo de processos de mesclagem. *maximum_concurrent_merge* está **int** com um padrão de 0. Um valor de **0** para essa propriedade significa que não há nenhum limite para o número de processos de mesclagem simultâneos em execução em um determinado momento. Essa propriedade define um limite para o número de processos de mesclagem simultâneos que pode ser executado em uma publicação de mesclagem de uma vez. Se houver mais processos de mesclagem agendados ao mesmo tempo do que o valor permitido para execução, os trabalhos em excesso serão enfileirados e esperarão até que o processo de mesclagem em execução no momento seja concluído.  
  
`[ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots` O número máximo de sessões do Snapshot Agent que podem ser executadas simultaneamente para gerar os instantâneos de dados filtrados para partições de assinante. *maximum_concurrent_dynamic_snapshots* está **int** com um padrão de 0. Se **0**, não há nenhum limite para as número sessões de instantâneo. Se houver mais processos de instantâneo agendados ao mesmo tempo do que o valor permitido para execução, os trabalhos em excesso serão enfileirados e esperarão até que o processo de instantâneo em execução no momento seja concluído.  
  
`[ @use_partition_groups = ] 'use_partition_groups'` Especifica que partições pré-computadas devem ser usadas para otimizar o processo de sincronização. *use_partition_groups* está **nvarchar (5)** , e pode ser um destes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**true**|A publicação usa partições pré-computadas.|  
|**false**|A publicação não usa partições pré-computadas.|  
|NULL(default)|O sistema escolhe a estratégia de particionamento.|  
  
 Partições pré-computadas são usadas por padrão. Para evitar o uso de partições de pré-computadas *use_partition_groups* deve ser definida como **falso**. Quando NULL, o sistema decidirá se partições pré-computadas podem ser usadas. Se as pré-calculadas partições não podem ser usadas, em seguida, esse valor efetivamente se torna **falsos** sem gerar erros. Nesses casos, *keep_partition_changes* pode ser definido como **verdadeiro** para fornecer alguma otimização. Para obter mais informações, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) e [otimizar o desempenho de filtro parametrizado com partições pré-computadas](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
`[ @publication_compatibility_level = ] backward_comp_level` Indica a compatibilidade com versões anteriores da publicação. *backward_comp_level* está **nvarchar(6)** , e pode ser um destes valores:  
  
|Valor|Version|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
`[ @replicate_ddl = ] replicate_ddl` Indica se a replicação de esquema tem suporte para a publicação. *replicate_ddl* está **int**, com um padrão de 1. **1** indica que instruções de DDL (linguagem) de definição de dados executadas no publicador são replicadas, e **0** indica que instruções DDL não são replicadas. Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
 O *@replicate_ddl* parâmetro é honrado quando uma instrução DDL adiciona uma coluna. O *@replicate_ddl* parâmetro é ignorado quando uma instrução DDL altera ou remove uma coluna pelos seguintes motivos.  
  
-   Quando uma coluna é descartada, sysarticlecolumns deve ser atualizado para impedir que novas instruções DML incluam a coluna removida que causaria o falha do agente de distribuição. O *@replicate_ddl* parâmetro é ignorado porque a replicação sempre tem que replicar a alteração de esquema.  
  
-   Quando uma coluna é alterada, o tipo de dados de origem ou nulidade podem ter sido alterados, fazendo as instruções DML conterem um valor que pode não ser compatível com a tabela no assinante. Estas instruções DML podem causar falha no agente de distribuição. O *@replicate_ddl* parâmetro é ignorado porque a replicação sempre tem que replicar a alteração de esquema.  
  
-   Quando uma instrução DDL adiciona uma nova coluna, sysarticlecolumns não inclui a nova coluna. Instruções DML não tentarão replicar dados para a nova coluna. O parâmetro é honrado porque replicar ou não replicar o DDL são aceitáveis.  
  
`[ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot'` Indica se os assinantes dessa publicação podem iniciar o processo de instantâneo para gerar o instantâneo filtrado para sua partição de dados. *allow_subscriber_initiated_snapshot* está **nvarchar (5)** , com um padrão de FALSE. **True** indica que os assinantes podem iniciar o processo de instantâneo.  
  
`[ @allow_web_synchronization = ] 'allow_web_synchronization'` Especifica se a publicação está habilitada para sincronização da Web. *allow_web_synchronization* está **nvarchar (5)** , com um padrão de FALSE. **True** Especifica que as assinaturas dessa publicação podem ser sincronizadas pelo HTTPS. Para obter mais informações, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md). Para dar suporte à [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes, você deve especificar **verdadeiro**.  
  
`[ @web_synchronization_url = ] 'web_synchronization_url'` Especifica o valor padrão de URL da Internet usado para sincronização da Web. *web_synchronization_url eu*s **nvarchar(500)** , com um padrão NULL. Define a URL de Internet padrão, se um não for definido explicitamente quando [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) é executado.  
  
`[ @allow_partition_realignment = ] 'allow_partition_realignment'` Determina se exclusões serão enviadas ao assinante quando modificação da linha no publicador faz com que ele altere sua partição. *allow_partition_realignment* está **nvarchar (5)** , com um padrão de TRUE. **True** envia exclusões para o assinante para refletir os resultados de uma alteração de partição, removendo dados que não fazem parte da partição do assinante. **False** deixa os dados de uma partição antiga no assinante, onde as alterações feitas a esses dados no publicador não serão replicadas para esse assinante, mas as alterações feitas no assinante serão replicadas para o publicador. Definindo *allow_partition_realignment* à **falso** é usado para manter os dados em uma assinatura de uma partição antiga quando os dados precisam estar acessíveis para fins históricos.  
  
> [!NOTE]  
>  Os dados permanecem no assinante como resultado da configuração *allow_partition_realignment* à **falso** devem ser tratados como se fosse somente leitura; no entanto, isso não é imposto pelo sistema de replicação.  
  
`[ @retention_period_unit = ] 'retention_period_unit'` Especifica as unidades para a período de retenção definido *retenção*. *retention_period_unit* está **nvarchar (10)** , e pode ser um dos valores a seguir.  
  
|Valor|Version|  
|-----------|-------------|  
|**dia** (padrão)|O período de retenção é especificado em dias.|  
|**week**|O período de retenção é especificado em semanas.|  
|**month**|O período de retenção é especificado em meses.|  
|**year**|O período de retenção é especificado em anos.|  
  
`[ @generation_leveling_threshold = ] generation_leveling_threshold` Especifica o número de alterações que estão contidos em uma geração. Uma geração é uma coleção de alterações que é entregue a um Publicador ou Assinante. *generation_leveling_threshold* está **int**, com um valor padrão de 1000.  
  
`[ @automatic_reinitialization_policy = ] automatic_reinitialization_policy` Especifica se as alterações são carregadas do assinante antes de uma reinicialização automática exigida por uma alteração na publicação, onde um valor de **1** foi especificado para **@force_reinit_subscription** . *automatic_reinitialization_policy* é bit, com um valor padrão de 0. **1** significa que as alterações são carregadas do assinante antes que ocorra uma reinicialização automática.  
  
> [!IMPORTANT]  
>  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
`[ @conflict_logging = ] 'conflict_logging'` Especifica onde os registros de conflito são armazenados. *conflict_logging* está **nvarchar(15)** , e pode ser um dos seguintes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**publisher**|Registros de conflito são armazenados no Publicador.|  
|**Assinante**|Registros de conflito são armazenados no Assinante que causou o conflito. Não há suportada para [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes.|  
|**ambos**|Registros de conflito são armazenados no Publicador e no Assinante.|  
|NULL (padrão)|Define automaticamente de Replication *conflict_logging* ao **ambos** quando o valor *backward_comp_level* é **90RTM** e **publisher** em todos os outros casos.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepublication** é usado em replicação de mesclagem.  
  
 Para listar objetos de publicação no Active Directory usando o **@add_to_active_directory** parâmetro, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto já deve ser criado no Active Directory.  
  
 Se houver várias publicações que publicam ao mesmo objeto de banco de dados, somente publicações com um *replicate_ddl* valor de **1** replicará ALTER TABLE, ALTER VIEW, ALTER PROCEDURE, ALTER FUNCTION e Instruções ALTER TRIGGER DDL. No entanto, uma instrução ALTER TABLE DROP COLUMN DDL será replicada por todas as publicações que estão publicando a coluna cancelada.  
  
 Para [!INCLUDE[ssEW](../../includes/ssew-md.md)] assinantes, o valor da *alternate_snapshot_folder* é usado apenas quando o valor de *snapshot_in_default_folder* é **false**.  
  
 Com replicação DDL habilitada (_replicate_ddl_ **= 1**) para uma publicação, para fazer a DDL de não replicação alterações na publicação [sp_changemergepublication &#40; Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) deve ser primeiro executado para definir *replicate_ddl* para **0**. Depois que as instruções de DDL de não replicação forem emitidas, **sp_changemergepublication** pode ser executado novamente para retroceder a replicação de DDL.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_addmergepublication**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
