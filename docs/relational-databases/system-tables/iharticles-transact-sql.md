---
title: IHarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHarticles
- IHarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHarticles system table
ms.assetid: 773ef9b7-c993-4629-9516-70c47b9dcf65
author: stevestein
ms.author: sstein
ms.openlocfilehash: 45278a6d9501b75b624e11bbeb11d24d10e482c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056215"
---
# <a name="iharticles-transact-sql"></a>IHarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHarticles** tabela do sistema contém uma linha para cada artigo que está sendo replicado de um publicador não SQL Server usando o distribuidor atual. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|A coluna de identidade que fornece um número de ID exclusivo para o artigo.|  
|**name**|**sysname**|O nome associado ao artigo, exclusivo dentro da publicação.|  
|**publication_id**|**smallint**|A ID da publicação à qual o artigo pertence.|  
|**table_id**|**int**|A ID da tabela publicada de [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md).|  
|**publisher_id**|**smallint**|A ID do publicador não SQL Server.|  
|**creation_script**|**nvarchar(255)**|O script de esquema para o artigo.|  
|**del_cmd**|**nvarchar(255)**|O tipo de comando de replicação usado ao replicar exclusões com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**filter**|**int**|Esta coluna não é usada e só é incluída para tornar a [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) modo de exibição da **IHarticles** tabela compatível com o [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) exibição usada para SQL Server (de artigos [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**filter_clause**|**ntext**|A cláusula WHERE do artigo, usada para filtragem horizontal e gravação de um Transact-SQL padrão que pode ser interpretado por um Editor não SQL.|  
|**ins_cmd**|**nvarchar(255)**|O tipo de comando de replicação usado ao replicar inserções com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**pre_creation_cmd**|**tinyint**|O comando a ser executado antes que o instantâneo inicial seja aplicado quando um objeto com o mesmo nome já existir no Assinante.<br /><br /> **0** = nenhum - um comando não é executado.<br /><br /> **1** = DROP - descartar a tabela de destino.<br /><br /> **2** = DELETE - excluir dados da tabela de destino.<br /><br /> **3** = TRUNCATE - truncar a tabela de destino.|  
|**status**|**tinyint**|O bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **0** = sem propriedades adicionais.<br /><br /> **1** = ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções com parâmetros.<br /><br /> Por exemplo, um artigo ativo que usa instruções com parâmetros teria um valor 17 nessa coluna. Um valor 0 significa que o artigo está inativo e nenhuma propriedade adicional está definida.|  
|**type**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo com base em log.|  
|**upd_cmd**|**nvarchar(255)**|O tipo de comando de replicação usado ao replicar atualizações com artigos de tabela. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**schema_option**|**binary(8)**|O bitmap da opção schema generation para o artigo determinado, que pode ser o resultado OR lógico bit a bit de um ou mais desses valores:<br /><br /> **0x00** = desabilitar geração de script pelo Snapshot Agent e usar o CreationScript fornecido.<br /><br /> **0x01** = gerar a criação do objeto (CREATE TABLE, CREATE PROCEDURE e assim por diante).<br /><br /> **0x10** = gerar um índice clusterizado correspondente.<br /><br /> **0x40** = gerar os índices não clusterizados correspondentes.<br /><br /> **0x80** = incluir integridade referencial declarada nas chaves primárias.<br /><br /> **0x1000** = replica agrupamento em nível de coluna. Observação: Essa opção é definida por padrão para Publicadores Oracle para habilitar comparações diferenciam maiusculas de minúsculas.<br /><br /> **0x4000** = replicar chaves exclusivas definidas em um artigo de tabela.<br /><br /> **0x8000** = replicar uma chave primária e chaves exclusivas em uma tabela do artigo como restrições usando instruções ALTER TABLE.|  
|**dest_owner**|**sysname**|O proprietário da tabela no banco de dados de destino.|  
|**dest_table**|**sysname**|O nome da tabela de destino.|  
|**tablespace_name**|**nvarchar(255)**|Identifica o espaço de tabela usado pela tabela de log para o artigo.|  
|**objid**|**int**|Esta coluna não é usada e só é incluída para tornar a [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) modo de exibição da **IHarticles** tabela compatível com o [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) exibição usada para SQL Server (de artigos [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**sync_objid**|**int**|Esta coluna não é usada e só é incluída para tornar a [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) modo de exibição da **IHarticles** tabela compatível com o [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) exibição usada para SQL Server (de artigos [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**description**|**nvarchar(255)**|A entrada descritiva para o artigo.|  
|**publisher_status**|**int**|É usado para indicar se o modo de exibição que define o artigo publicado foi definido chamando [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md).<br /><br /> **0** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) foi chamado.<br /><br /> **1** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) não foi chamado.|  
|**article_view_owner**|**nvarchar(255)**|O proprietário do objeto de sincronização no Publicador usado pelo Log Reader Agent.|  
|**article_view**|**nvarchar(255)**|O objeto de sincronização no Publicador usado pelo Log Reader Agent.|  
|**ins_scripting_proc**|**int**|Esta coluna não é usada e só é incluída para tornar a [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) modo de exibição da **IHarticles** tabela compatível com o [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) exibição usada para SQL Server (de artigos [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**del_scripting_proc**|**int**|Esta coluna não é usada e só é incluída para tornar a [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) modo de exibição da **IHarticles** tabela compatível com o [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) exibição usada para SQL Server (de artigos [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**upd_scripting_proc**|**int**|Esta coluna não é usada e só é incluída para tornar a [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) modo de exibição da **IHarticles** tabela compatível com o [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) exibição usada para SQL Server (de artigos [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**custom_script**|**int**|Esta coluna não é usada e só é incluída para tornar a [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) modo de exibição da **IHarticles** tabela compatível com o [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) exibição usada para SQL Server (de artigos [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**fire_triggers_on_snapshot**|**bit**|Esta coluna não é usada e só é incluída para tornar a [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) modo de exibição da **IHarticles** tabela compatível com o [sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md) exibição usada para SQL Server (de artigos [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)).|  
|**instance_id**|**int**|Identifica a instância atual do log de artigo para a tabela publicada.|  
|**use_default_datatypes**|**bit**|Indica se o artigo usa mapeamentos de tipo de dados padrão; um valor de **1** indica que os mapeamentos de tipo de dados padrão são usados.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)  
  
  
