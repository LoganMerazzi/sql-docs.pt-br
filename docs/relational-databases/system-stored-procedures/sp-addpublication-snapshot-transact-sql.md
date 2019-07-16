---
title: sp_addpublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4fbba559eceae58483419c0f1e3826b9db79bef5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061827"
---
# <a name="spaddpublicationsnapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Cria o Agente de Instantâneo para a publicação especificada. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
`[ @frequency_type = ] frequency_type` É a frequência com a qual o Snapshot Agent é executado. *frequency_type* está **int**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez.|  
|**4** (padrão)|Diariamente.|  
|**8**|Semanalmente.|  
|**16**|Mensalmente.|  
|**32**|Mensalmente, relativo ao intervalo de frequência.|  
|**64**|Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent inicia.|  
|**128**|Executar quando o computador estiver ocioso|  
  
`[ @frequency_interval = ] frequency_interval` É o valor a ser aplicado à frequência definida *frequency_type*. *frequency_interval* está **int**, e pode ser um dos valores a seguir.  
  
|Valor de frequency_type|Efeito em frequency_interval|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval* não é usado.|  
|**4** (padrão)|Cada *frequency_interval* dias, com um padrão de diariamente.|  
|**8**|*frequency_interval* é um ou mais dos seguintes (combinado com um [ &#124; (Bitwise OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md) operador lógico):<br /><br /> **1** = domingo&#124;<br /><br /> **2** = segunda-feira&#124;<br /><br /> **4** = terça-feira&#124;<br /><br /> **8** = quarta-feira&#124;<br /><br /> **16** = quinta-feira&#124;<br /><br /> **32** = sexta-feira&#124;<br /><br /> **64** = sábado|  
|**16**|Sobre o *frequency_interval* dia do mês.|  
|**32**|*frequency_interval* é um dos seguintes:<br /><br /> **1** = domingo&#124;<br /><br /> **2** = segunda-feira&#124;<br /><br /> **3** = terça-feira&#124;<br /><br /> **4** = quarta-feira&#124;<br /><br /> **5** = quinta-feira&#124;<br /><br /> **6** = sexta-feira&#124;<br /><br /> **7** = sábado&#124;<br /><br /> **8** = dia&#124;<br /><br /> **9** = dia da semana&#124;<br /><br /> **10** = dia de fim de semana|  
|**64**|*frequency_interval* não é usado.|  
|**128**|*frequency_interval* não é usado.|  
  
`[ @frequency_subday = ] frequency_subday` É a unidade para *freq_subday_interval*. *frequency_subday* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**2**|Segundo|  
|**4** (padrão)|Minuto|  
|**8**|Hora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` É o intervalo de *frequency_subday*. *frequency_subday_interval* está **int**, com um padrão de 5, que significa que a cada 5 minutos.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` É a data em que o Snapshot Agent é executado. *frequency_relative_interval* está **int**, com um padrão de 1.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` É o fator de recorrência usado pelo *frequency_type*. *frequency_recurrence_factor* está **int**, com um padrão de 0.  
  
`[ @active_start_date = ] active_start_date` É a data quando o agente de instantâneo é primeiro agendada, formatada como AAAAMMDD. *active_start_date* está **int**, com um padrão de 0.  
  
`[ @active_end_date = ] active_end_date` É a data em que o Snapshot Agent deixa de ser agendado, formatada como AAAAMMDD. *active_end_date* está **int**, com um padrão de 99991231, que significa 31 de dezembro de 9999.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` É a hora do dia quando o agente de instantâneo é o primeiro agendada, formatada como HHMMSS. *active_start_time_of_day* está **int**, com um padrão de 0.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` É a hora do dia em que o Snapshot Agent deixa de ser agendado, formatada como HHMMSS. *active_end_time_of_day* está **int**, com um padrão de 235959, que significa que 11:59:59 P.M. medida em um relógio de 24 horas.  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'` É o nome de um nome de trabalho do agente de instantâneo existente se um trabalho existente estiver sendo usado. *snapshot_agent_name* está **nvarchar(100)** com um valor padrão de NULL. Esse parâmetro é para uso interno e não deve ser especificado ao criar uma nova publicação. Se *snapshot_agent_name* for especificado, então *job_login* e *job_password* deve ser NULL.  
  
`[ @publisher_security_mode = ] publisher_security_mode` É o modo de segurança usado pelo agente ao se conectar ao publicador. *publisher_security_mode* está **smallint**, com um padrão de 1. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, e **1** Especifica a autenticação do Windows. Um valor de **0** deve ser especificado para não - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` É o logon usado ao conectar-se ao publicador. *publisher_login* está **sysname**, com um padrão NULL. *publisher_login* deve ser especificado quando *publisher_security_mode* é **0**. Se *publisher_login* for NULL e *publisher_security_mode* está **1**, em seguida, a conta especificada na *job_login* será usado quando conectar-se ao publicador.  
  
`[ @publisher_password = ] 'publisher_password'` É a senha usada ao conectar-se ao publicador. *publisher_password* está **sysname**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para ajudar a melhorar a segurança, recomendamos que você forneça nomes de login e senhas em tempo de execução.  
  
`[ @job_login = ] 'job_login'` É o logon para a conta sob a qual o agente é executado. No banco de dados de instância gerenciada do SQL, use uma conta do SQL Server. *job_login* está **nvarchar(257)** , com um padrão NULL. Essa conta sempre é usada para conexões do agente para o distribuidor. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo.  
  
> [!NOTE]
>  Para não - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores, isso deve ser o mesmo logon especificado em [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md).  
  
`[ @job_password = ] 'job_password'` É a senha para a conta do Windows sob a qual o agente é executado. *job_password* está **sysname**, sem padrão. Você deve fornecer esse parâmetro ao criar um novo trabalho do Agente de Instantâneo.  
  
> [!IMPORTANT]  
>  Não armazene informações de autenticação em arquivos de script. Para ajudar a melhorar a segurança, recomendamos que você forneça nomes de login e senhas em tempo de execução.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *Publisher* não deve ser usado durante a criação de um agente de instantâneo em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addpublication_snapshot** é usado em replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_addpublication_snapshot**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Criar e aplicar o instantâneo](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
