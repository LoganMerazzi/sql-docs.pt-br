---
title: sp_redirect_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_redirect_publisher_TSQL
- sp_redirect_publisher
helpviewer_keywords:
- sp_redirect_publisher
ms.assetid: af45e2b2-57fb-4bcd-a58b-e61401fb3b26
author: stevestein
ms.author: sstein
ms.openlocfilehash: cde6f00d16bcff4ee56513f515cf2ecac93a1b5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002513"
---
# <a name="spredirectpublisher-transact-sql"></a>sp_redirect_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Especifica um publicador redirecionado para um par de publicador/banco de dados existente. Se o banco de dados publicador pertencer a um grupo de disponibilidade AlwaysOn, o publicador redirecionado será o nome de ouvinte do grupo de disponibilidade associado ao grupo de disponibilidade.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'` O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que publicou originalmente o banco de dados. *original_publisher* está **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'` O nome do banco de dados que está sendo publicado. *publisher_db* está **sysname**, sem padrão.  
  
`[ @redirected_publisher = ] 'redirected_publisher'` O nome de ouvinte de grupo disponibilidade associado ao grupo de disponibilidade que será o novo publicador. *redirected_publisher* está **sysname**, sem padrão. Quando o ouvinte do grupo de disponibilidade estiver configurado para a porta não padrão, especifique o número da porta junto com o nome do ouvinte, por exemplo, `'Listenername,51433'`  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_redirect_publisher** é usado para permitir que um publicador de replicação seja redirecionado para a réplica primária atual de um grupo de disponibilidade AlwaysOn associando o par publicador/banco de dados com o ouvinte do grupo de disponibilidade. Execute **sp_redirect_publisher** depois que o ouvinte do AG for configurado para o grupo de disponibilidade que contém o banco de dados publicado.  
  
 Se o banco de dados de publicação no publicador original for removido de um grupo de disponibilidade na réplica primária, execute **sp_redirect_publisher** sem especificar um valor para o *@redirected_publisher* parâmetro a remover o redirecionamento para o par publicador/banco de dados. Para obter mais informações sobre como redirecionar o publicador quando, consulte [mantendo um banco de dados de publicação AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Chamador deve ser um membro do **sysadmin** função de servidor fixa, o **db_owner** função fixa de banco de dados para o banco de dados de distribuição ou membro de uma lista de acesso da publicação para uma publicação definida associado com o banco de dados do publicador.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
