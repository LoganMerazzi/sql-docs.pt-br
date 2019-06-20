---
title: sp_articlefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 698a5941bc8e9920942e7ec7c962144b4ab24b62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62998288"
---
# <a name="sparticlefilter-transact-sql"></a>sp_articlefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Filtra dados que são publicados com base em um artigo de tabela. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_articlefilter [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @filter_name = ] 'filter_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação que contém o artigo. *publicação* está **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo. *artigo* está **sysname**, sem padrão.  
  
`[ @filter_name = ] 'filter_name'` É o nome do procedimento armazenado de filtro a ser criado a partir de *filter_name*. *filter_name* está **nvarchar(386)** , com um padrão NULL. Você deve especificar um nome exclusivo para o filtro de artigo.  
  
`[ @filter_clause = ] 'filter_clause'` É uma restrição cláusula (WHERE) que define um filtro horizontal. Ao inserir a cláusula de restrição, omita a palavra-chave onde. *filter_clause* está **ntext**, com um padrão NULL.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Confirma que a ação tomada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** Especifica que as alterações no artigo podem invalidar o instantâneo ser inválida e se houver assinaturas existentes que exigem um novo instantâneo, dará permissão para o instantâneo existente seja marcado como obsoleto e um novo instantâneo seja gerado.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` Reconhece que a ação tomada por esse procedimento armazenado pode requerer que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit**, com um padrão de **0**.  
  
 **0** Especifica que as alterações no artigo não causa uma necessidade das assinaturas sejam reinicializadas. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas sejam reiniciadas, ocorrerá um erro e nenhuma alteração é feita.  
  
 **1** Especifica que as alterações no artigo faz com que as assinaturas existentes sejam reinicializadas e dá permissão para que ocorra a reinicialização da assinatura.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser usado com um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_articlefilter** é usado em replicação de instantâneo e replicação transacional.  
  
 Executando **sp_articlefilter** para um artigo com as assinaturas existentes requer que as assinaturas sejam reinicializadas.  
  
 **sp_articlefilter** cria o filtro, insere a ID do procedimento armazenado de filtro na **filtro** coluna o [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabela e, em seguida, Insere o texto da cláusula de restrição na **filter_clause** coluna.  
  
 Para criar um artigo com um filtro horizontal, execute [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) sem nenhum *filtro* parâmetro. Execute **sp_articlefilter**, fornecendo todos os parâmetros incluindo *filter_clause*e, em seguida, execute [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md), fornecendo todos os parâmetros incluindo idênticas *filter_clause*. Se o filtro já existe e se o **tipo** na **sysarticles** está **1** (artigo com base em log), o filtro anterior será excluído e um novo filtro é criado.  
  
 Se *filter_name* e *filter_clause* não forem fornecidos, o filtro anterior será excluído e a ID do filtro é definida como **0**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_articlefilter**.  
  
## <a name="see-also"></a>Consulte também  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir e modificar um filtro de linha estático](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
