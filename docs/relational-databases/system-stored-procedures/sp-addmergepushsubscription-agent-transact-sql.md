---
title: sp_addmergepushsubscription_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepushsubscription_agent_TSQL
- sp_addmergepushsubscription_agent
helpviewer_keywords:
- sp_addmergepushsubscription_agent
ms.assetid: 808a1925-be46-4999-8d69-b3a83010ec81
author: stevestein
ms.author: sstein
ms.openlocfilehash: e24659cc7880a5df34aa451c5051e77b8a4c59d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117950"
---
# <a name="spaddmergepushsubscriptionagent-transact-sql"></a>sp_addmergepushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um novo trabalho de agente para agendar sincronização de uma assinatura push para uma publicação de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergepushsubscription_agent [ @publication =] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password = ] 'subscriber_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
`[ @subscriber = ] 'subscriber'` É o nome do assinante. *assinante* está **sysname**, com um padrão NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'` É o nome do banco de dados de assinatura. *subscriber_db* está **sysname**, com um padrão NULL.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode` É o modo de segurança a ser usado ao se conectar a um assinante na sincronização. *subscriber_security_mode* está **int**, com um padrão de 1. Se **0**, especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. Se **1**, especifica a autenticação do Windows.  
  
`[ @subscriber_login = ] 'subscriber_login'` É o logon do assinante a ser usado ao se conectar a um assinante na sincronização. *subscriber_login* será necessária se *subscriber_security_mode* é definido como **0**. *subscriber_login* está **sysname**, com um padrão NULL.  
  
`[ @subscriber_password = ] 'subscriber_password'` É a senha do assinante para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. *subscriber_password* será necessária se *subscriber_security_mode* é definido como **0**. *subscriber_password* está **sysname**, com um padrão NULL. Se uma senha de assinante for usada, será criptografada automaticamente.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @publisher_security_mode = ] publisher_security_mode` É o modo de segurança a ser usado ao se conectar a um publicador na sincronização. *publisher_security_mode* está **int**, com um padrão de 1. Se **0**, especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. Se **1**, especifica a autenticação do Windows.  
  
`[ @publisher_login = ] 'publisher_login'` É o logon a ser usado ao se conectar a um publicador na sincronização. *publisher_login* está **sysname**, com um padrão NULL.  
  
`[ @publisher_password = ] 'publisher_password'` É a senha usada ao conectar-se ao publicador. *publisher_password* está **sysname**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @job_login = ] 'job_login'` É o logon para a conta do Windows sob a qual o agente é executado. *job_login* está **nvarchar(257)** , com um valor padrão de NULL. Essa conta do Windows é sempre usada para conexões do agente com o Distribuidor e para conexões com o Assinante e o Publicador ao usar a autenticação integrada do Windows.  
  
`[ @job_password = ] 'job_password'` É a senha para a conta do Windows sob a qual o agente é executado. *job_password* está **sysname**, sem padrão.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @job_name = ] 'job_name'` É o nome de um trabalho de agente existente. *job_name* está **sysname**, com um valor padrão de NULL. Esse parâmetro só é especificado quando a assinatura é sincronizada usando um trabalho existente em vez de um trabalho recém-criado (o padrão). Se você não for um membro do **sysadmin** função de servidor fixa, você deve especificar *job_login* e *job_password* quando você especifica *job_name*.  
  
`[ @frequency_type = ] frequency_type` É a frequência de agendamento do Merge Agent. *frequency_type* está **int**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Sob Demanda|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Relativo ao mês|  
|**64**|Iniciar automaticamente|  
|**128**|Recorrente|  
|NULL (padrão)||  
  
> [!NOTE]  
>  Especificando um valor de **64** faz com que o Merge Agent para executar em modo contínuo. Isso corresponde à configuração de **-contínua** parâmetro para o agente. Para obter mais informações, consulte [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
`[ @frequency_interval = ] frequency_interval` Os dias em que o Merge Agent é executado. *frequency_interval* está **int**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Segunda-feira|  
|**3**|Terça-feira|  
|**4**|Quarta-feira|  
|**5**|Quinta-feira|  
|**6**|Sexta-feira|  
|**7**|Sábado|  
|**8**|Day|  
|**9**|Dias da semana|  
|**10**|Dias de fim de semana|  
|NULL (padrão)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` É a data do Merge Agent. Esse parâmetro é usado quando *frequency_type* é definido como **32** (mensal relativo). *frequency_relative_interval* está **int**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
|NULL (padrão)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* está **int**, com um padrão NULL.  
  
`[ @frequency_subday = ] frequency_subday` É a frequência de reagendamento durante o período definido. *frequency_subday* está **int**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4**|Minuto|  
|**8**|Hora|  
|NULL (padrão)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` É o intervalo de *frequency_subday*. *frequency_subday_interval* está **int**, com um padrão NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` É a hora do dia quando o Merge Agent é o primeiro agendada, formatada como HHMMSS. *active_start_time_of_day* está **int**, com um padrão NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` É a hora do dia em que o Merge Agent deixa de ser agendado, formatada como HHMMSS. *active_end_time_of_day* está **int**, com um padrão NULL.  
  
`[ @active_start_date = ] active_start_date` É a data quando o Merge Agent é primeiro agendada, formatada como AAAAMMDD. *active_start_date* está **int**, com um padrão NULL.  
  
`[ @active_end_date = ] active_end_date` É a data em que o Merge Agent deixa de ser agendado, formatada como AAAAMMDD. *active_end_date* está **int**, com um padrão NULL.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` Especifica se a assinatura pode ser sincronizada por meio do Gerenciador de sincronização do Windows. *enabled_for_syncmgr* está **nvarchar (5)** , com um padrão de FALSE. Se **falsos**, a assinatura não está registrada com o Gerenciador de sincronização. Se **verdadeira**, a assinatura é registrada com o Gerenciador de sincronização e será sincronizada sem iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepushsubscription_agent** é usado em replicação de mesclagem e usa funcionalidade semelhante a [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md).  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepushsubscript_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_addmergepushsubscription_agent**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
