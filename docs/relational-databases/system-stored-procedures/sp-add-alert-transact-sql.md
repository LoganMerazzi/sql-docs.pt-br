---
title: sp_add_alert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_alert
- sp_add_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b16fe1f29d132b900eeb4c8f450fcdbd66eb22b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942387"
---
# <a name="spaddalert-transact-sql"></a>sp_add_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um alerta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_alert [ @name = ] 'name'   
     [ , [ @message_id = ] message_id ]   
     [ , [ @severity = ] severity ]   
     [ , [ @enabled = ] enabled ]  
     [ , [ @delay_between_responses = ] delay_between_responses ]   
     [ , [ @notification_message = ] 'notification_message' ]   
     [ , [ @include_event_description_in = ] include_event_description_in ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @event_description_keyword = ] 'event_description_keyword_pattern' ]   
     [ , { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ]   
     [ , [ @raise_snmp_trap = ] raise_snmp_trap ]   
     [ , [ @performance_condition = ] 'performance_condition' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` O nome do alerta. O nome é exibido na mensagem de email ou de pager enviada em resposta ao alerta. Ele deve ser exclusivo e pode conter a porcentagem ( **%** ) caracteres. *nome da* está **sysname**, sem padrão.  
  
`[ @message_id = ] message_id` O número de erro de mensagem que define o alerta. (Normalmente corresponde a um número de erro no **sysmessages** tabela.) *message_id* é **int**, com um padrão de **0**. Se *gravidade* é usado para definir o alerta *message_id* deve ser **0** ou nulo.  
  
> [!NOTE]  
>  Somente **sysmessages** erros gravados no log de aplicativo do Microsoft Windows podem fazer com que um alerta seja enviado.  
  
`[ @severity = ] severity` O nível de gravidade (de **1** por meio **25**) que define o alerta. Qualquer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem armazenada em de **sysmessages** tabela enviada para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] log de aplicativo do Windows com a severidade indicada fará com que o alerta seja enviado. *gravidade* está **int**, com um padrão de 0. Se *message_id* é usado para definir o alerta *gravidade* deve ser **0**.  
  
`[ @enabled = ] enabled` Indica o status atual do alerta. *habilitada* está **tinyint**, com um padrão de 1 (habilitado). Se **0**, o alerta não está habilitado e não será acionado.  
  
`[ @delay_between_responses = ] delay_between_responses` O período de espera, em segundos, entre respostas ao alerta. *delay_between_responses*está **int**, com um padrão de **0**, que significa que não haverá nenhuma espera entre as respostas (cada ocorrência do alerta gera uma resposta). A resposta pode acontecer de uma destas maneiras ou de ambas:  
  
-   Uma ou mais notificações enviadas por email ou pager.  
  
-   Um trabalho a ser executado.  
  
 Ao definir esse valor, é possível evitar, por exemplo, que mensagens de email não desejadas sejam enviadas quando um alerta ocorre repetidamente em um curto período.  
  
`[ @notification_message = ] 'notification_message'` É uma mensagem adicional opcional enviada ao operador como parte de email, **net send**, ou notificação de pager. *notification_message* está **nvarchar(512)** , com um padrão NULL. Especificando *notification_message* é útil para adicionar observações especiais como procedimentos corretivos.  
  
`[ @include_event_description_in = ] include_event_description_in` É se a descrição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erro deve ser incluído como parte da mensagem de notificação. *include_event_description_in*está **tinyint**, com um padrão de **5** (email e **net send**) e pode ter um ou mais desses valores combinados com um **Ou** operador lógico.  
  
> [!IMPORTANT]
>  As opções Pager e **net send** serão removidas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Nenhum|  
|**1**|Email|  
|**2**|Pager|  
|**4**|**net send**|  
  
`[ @database_name = ] 'database'` O banco de dados no qual o erro deve ocorrer para o alerta seja acionado. Se *banco de dados*não for fornecido, o alerta será acionado independentemente de onde o erro ocorreu. *banco de dados* está **sysname**. Os nomes entre colchetes ([ ]) não são permitidos. O valor padrão é NULL.  
  
`[ @event_description_keyword = ] 'event_description_keyword_pattern'` A sequência de caracteres que a descrição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erro deve ser semelhantes. Os caracteres correspondentes ao padrão da expressão LIKE do [!INCLUDE[tsql](../../includes/tsql-md.md)] podem ser usados. *event_description_keyword_pattern* está **nvarchar(100)** , com um padrão NULL. Esse parâmetro é útil para filtrar nomes de objeto (por exemplo, **% customer_table %** ).  
  
`[ @job_id = ] job_id` O número de identificação do trabalho a ser executado em resposta a esse alerta. *job_id* está **uniqueidentifier**, com um padrão NULL.  
  
`[ @job_name = ] 'job_name'` O nome do trabalho a ser executado em resposta a esse alerta. *job_name*está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados.  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` Não implementado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0. *raise_snmp_trap* está **tinyint**, com um padrão de 0.  
  
`[ @performance_condition = ] 'performance_condition'` É um valor expressado no formato '*itemcomparatorvalue*'. *performance_condition* está **nvarchar(512)** com um padrão de NULL e consiste nestes elementos.  
  
|Elemento Format|Descrição|  
|--------------------|-----------------|  
|*Item*|Um objeto de desempenho, contador de desempenho ou instância nomeada do contador|  
|*Comparador*|Um destes operadores: >, <, ou =|  
|*Valor*|Valor numérico do contador|  
  
`[ @category_name = ] 'category'` O nome da categoria de alerta. *categoria* está **sysname**, com um padrão NULL.  
  
`[ @wmi_namespace = ] 'wmi_namespace'` O namespace do WMI para consulta de eventos. *wmi_namespace* está **sysname**, com um padrão NULL. Somente namespaces no servidor local possuem suporte.  
  
`[ @wmi_query = ] 'wmi_query'` A consulta que especifica o evento WMI para o alerta. *wmi_query* está **nvarchar(512)** , com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_add_alert** deve ser executado a partir de **msdb** banco de dados.  
  
 Essas são as circunstâncias sob as quais erros/mensagens gerados pelos aplicativos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são enviados ao log de aplicativos do Windows e, assim, podem gerar alertas:  
  
-   Severidade 19 ou superior **sys. messages** erros  
  
-   Qualquer instrução RAISERROR é invocada com a sintaxe WITH LOG  
  
-   Qualquer **sys. messages** erro modificado ou criado usando **sp_altermessage**  
  
-   Qualquer evento registrado usando **xp_logevent**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece um modo gráfico e fácil para gerenciar o sistema de alertas inteiro e é recomendado para configurar uma infraestrutura de alerta.  
  
 Se um alerta não estiver funcionando corretamente, verifique se:  
  
-   O serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está em execução.  
  
-   O evento foi exibido no log de aplicativos do Windows.  
  
-   O alerta está habilitado.  
  
-   Eventos gerados com **xp_logevent** ocorrem no banco de dados mestre. Portanto, **xp_logevent** não dispara um alerta a menos que o **@database_name** para o alerta seja **'mestre'** ou NULL.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, somente membros da função de servidor fixa **sysadmin** podem executar **sp_add_alert**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona um alerta (Alerta de Teste) que executa o trabalho `Back up the AdventureWorks2012 Database` quando é acionado.  
  
> [!NOTE]  
>  Este exemplo supõe que a mensagem 55001 e o trabalho `Back up the AdventureWorks2012 Database` já existam. O exemplo é mostrado somente para fins ilustrativos.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_alert  
    @name = N'Test Alert',  
    @message_id = 55001,   
   @severity = 0,   
   @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
   @job_name = N'Back up the AdventureWorks2012 Database' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
