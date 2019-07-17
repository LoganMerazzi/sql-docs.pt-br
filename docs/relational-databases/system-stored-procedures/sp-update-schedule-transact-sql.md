---
title: sp_update_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_schedule
- sp_update_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_schedule
ms.assetid: 97b3119b-e43e-447a-bbfb-0b5499e2fefe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 51e21d189a9302c2dc7b74a013846460e9cb7bc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946649"
---
# <a name="spupdateschedule-transact-sql"></a>sp_update_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as configurações de uma agenda do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_schedule   
    {   [ @schedule_id = ] schedule_id   
      | [ @name = ] 'schedule_name' }  
    [ , [ @new_name = ] new_name ]  
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @schedule_id = ] schedule_id` O identificador da agenda a ser modificada. *schedule_id* está **int**, sem padrão. Qualquer um dos *schedule_id* ou *schedule_name* deve ser especificado.  
  
`[ @name = ] 'schedule_name'` O nome da agenda a ser modificada. *schedule_name*está **sysname**, sem padrão. Qualquer um dos *schedule_id* ou *schedule_name* deve ser especificado.  
  
`[ @new_name = ] new_name` O novo nome para a agenda. *new_name* está **sysname**, com um padrão NULL. Quando *new_name* for NULL, o nome da agenda é alterado.  
  
`[ @enabled = ] enabled` Indica o status atual da agenda. *habilitada*está **tinyint**, com um padrão de **1** (habilitado). Se **0**, o agendamento não está habilitado. Quando o agendamento não está habilitado, nenhum trabalho é executado nele.  
  
`[ @freq_type = ] freq_type` Um valor que indica quando um trabalho a ser executado. *freq_type*está **int**, com um padrão de **0**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Uma vez|  
|**4**|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensalmente|  
|**32**|Mensalmente, relativo a *freq intervalo*|  
|**64**|Executado quando o serviço SQLServerAgent é iniciado|  
|**128**|Executar quando o computador estiver ocioso|  
  
`[ @freq_interval = ] freq_interval` Os dias em que um trabalho é executado. *freq_interval* está **int**, com um padrão de **0**e depende do valor de *freq_type*.  
  
|Valor de *freq_type*|Efeito em *freq_interval*|  
|---------------------------|--------------------------------|  
|**1** (uma vez)|*freq_interval* não é usado.|  
|**4** (diariamente)|Cada *freq_interval* dias.|  
|**8** (Semanalmente)|*freq_interval* é um ou mais dos seguintes (combinado com um **OR** operador lógico):<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **4** = terça-feira<br /><br /> **8** = quarta-feira<br /><br /> **16** = quinta-feira<br /><br /> **32** = sexta-feira<br /><br /> **64** = sábado|  
|**16** (mensalmente)|Sobre o *freq_interval* dia do mês.|  
|**32** (mensal relativo)|*freq_interval* é um dos seguintes:<br /><br /> **1** = domingo<br /><br /> **2** = segunda-feira<br /><br /> **3** = terça-feira<br /><br /> **4** = quarta-feira<br /><br /> **5** = quinta-feira<br /><br /> **6** = sexta-feira<br /><br /> **7** = sábado<br /><br /> **8** = dia<br /><br /> **9** = dia da semana<br /><br /> **10** = dia de fim de semana|  
|**64** (quando o serviço SQLServerAgent é iniciado)|*freq_interval* não é usado.|  
|**128**|*freq_interval* não é usado.|  
  
`[ @freq_subday_type = ] freq_subday_type` Especifica as unidades para *freq_subday_interval * *.* *freq_subday_type*está **int**, com um padrão de **0**, e pode ser um destes valores.  
  
|Valor|Descrição (unidade)|  
|-----------|--------------------------|  
|**0x1**|Na hora especificada|  
|**0x2**|Seconds (segundos)|  
|**0x4**|Minutes (minutos)|  
|**0x8**|Hours (horas)|  
  
`[ @freq_subday_interval = ] freq_subday_interval` O número de *freq_subday_type* períodos ocorrer entre cada execução de um trabalho. *freq_subday_interval*está **int**, com um padrão de **0**.  
  
`[ @freq_relative_interval = ] freq_relative_interval` Ocorrência de um trabalho de *freq_interval* em cada mês, se *freq_interval* está **32** (mensal relativo). *freq_relative_interval*está **int**, com um padrão de **0**, e pode ser um destes valores.  
  
|Valor|Descrição (unidade)|  
|-----------|--------------------------|  
|**1**|First|  
|**2**|Segundo|  
|**4**|Terceiro|  
|**8**|Quarto|  
|**16**|Last|  
  
`[ @freq_recurrence_factor = ] freq_recurrence_factor` O número de semanas ou meses entre execuções agendadas de um trabalho. *freq_recurrence_factor* é usado somente se *freq_type* é **8**, **16**, ou **32**. *freq_recurrence_factor*está **int**, com um padrão de **0**.  
  
`[ @active_start_date = ] active_start_date` A data em que a execução de um trabalho pode começar. *active_start_date*está **int**, com um padrão NULL, que indica a data de hoje. A data é formatada como DDMMAAAA. Se *active_start_date* não for nulo, a data deve ser maior que ou igual a 19900101.  
  
 Depois que a agenda estiver criada, reveja a data de início e confirme se essa é a data correta. Para obter mais informações, consulte a seção "Agendando datas de início" em [criar e anexar agendamentos a trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
`[ @active_end_date = ] active_end_date` A data na qual a execução de um trabalho pode parar. *active_end_date*está **int**, com um padrão de **99991231**, que indica 31 de dezembro de 9999. Formatada como AAAAMMDD.  
  
`[ @active_start_time = ] active_start_time` A hora em qualquer dia entre *active_start_date* e *active_end_date* para iniciar a execução de um trabalho. *active_start_time*está **int**, com um padrão de 000000, que indica 12:00:00: 00 em um relógio de 24 horas e deve ser inserido com o formato HHMMSS.  
  
`[ @active_end_time = ] active_end_time` A hora em qualquer dia entre *active_start_date* e *active_end_date* para terminar a execução de um trabalho. *active_end_time*está **int**, com um padrão de **235959**, que indica a 11:59:59 P.M. em um relógio de 24 horas e deve ser inserido com o formato HHMMSS.  
  
`[ @owner_login_name = ] 'owner_login_name']` O nome da entidade de servidor que possui a agenda. *owner_login_name* está **sysname**, com um padrão NULL, que indica que a agenda é pertence ao criador.  
  
`[ @automatic_post = ] automatic_post` Reservado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Todos os trabalhos que usam a agenda usarão imediatamente as novas configurações. Entretanto, a alteração de uma agenda não para trabalhos que estejam atualmente em execução.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros da **sysadmin** pode modificar uma agenda pertencente a outro usuário.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o status habilitado da agenda `NightlyJobs` para `0` e define o proprietário como `terrid`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_schedule  
    @name = 'NightlyJobs',  
    @enabled = 0,  
    @owner_login_name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar e anexar agendas a trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [Agendar um trabalho](../../ssms/agent/schedule-a-job.md)   
 [Criar uma agenda](../../ssms/agent/create-a-schedule.md)   
 [Procedimentos armazenados do SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
