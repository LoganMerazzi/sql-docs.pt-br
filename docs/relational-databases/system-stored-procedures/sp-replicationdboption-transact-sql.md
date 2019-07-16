---
title: sp_replicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e8285713df1fb17b2e82dcfa6edac0fd6db5500a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950667"
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define uma opção de banco de dados de replicação para o banco de dados especificado. Esse procedimento armazenado é executado no Publicador ou no Assinante, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@dbname=** ] **'***dbname***'**  
 É o banco de dados para o qual a opção de banco de dados de replicação está sendo definida. *DB_NAME* está **sysname**, sem padrão.  
  
 [ **@optname=** ] **'***optname***'**  
 É a opção de banco de dados de replicação a ser habilitada ou desabilitada. *optname* está **sysname**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**publicação de mesclagem**|O banco de dados pode ser usado para publicações de mesclagem.|  
|**Publicar**|O banco de dados pode ser usado para outros tipos de publicação.|  
|**Inscrever-se**|O banco de dados é um banco de dados de assinatura.|  
|**sincronizar com backup**|O banco de dados está habilitado para backup coordenado. Para obter mais informações, consulte [habilitar Backups coordenados para replicação transacional &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).|  
  
`[ @value = ] 'value'` É se deseja habilitar ou desabilitar a opção de banco de dados de replicação. *valor* está **sysname**e pode ser **verdadeira** ou **false**. Quando esse valor é **falsos** e *optname* é **publicação de mesclagem**, as assinaturas para o banco de dados publicado de mesclagem também serão descartadas.  
  
`[ @ignore_distributor = ] ignore_distributor` Indica se esse procedimento armazenado é executado sem se conectar ao distribuidor. *ignore_distributor* está **bit**, com um padrão de **0**, significando que o distribuidor deve ser conectado ao e atualizada com o novo status do banco de dados de publicação. O valor **1** só deve ser especificado se o distribuidor estiver inacessível e **sp_replicationdboption** está sendo usado para desabilitar a publicação.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replicationdboption** é usado em replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
 Esse procedimento cria ou descarta tabelas do sistema de replicação específicas, contas de segurança, e assim por diante, que depende das opções fornecidas. Configura a categoria correspondente bit na **sysdatabases** tabela do sistema e cria as tabelas de sistema necessários.  
  
 Para desabilitar a publicação, o banco de dados de publicação deve estar online. Se um instantâneo do banco de dados existir para o banco de dados de publicação, deverá ser descartado antes de desabilitar a publicação. O instantâneo do banco de dados é uma cópia offline somente leitura de um banco de dados e não está relacionado a um instantâneo de replicação. Para obter mais informações, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** pode executar a função de servidor fixa **sp_replicationdboption**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Excluir uma publicação](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.sysdatabases &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
