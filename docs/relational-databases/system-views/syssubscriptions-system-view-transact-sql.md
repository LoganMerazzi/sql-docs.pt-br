---
title: syssubscriptions (exibição do sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3a50ce1b42c8963aac0bc152e08c6d39eec73eb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094783"
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions (Exibição de sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **syssubscriptions** exibição expõe informações de assinatura. Essa exibição é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|A ID exclusiva de um artigo assinado.|  
|**srvid**|**smallint**|A ID de servidor do Assinante.|  
|**dest_db**|**sysname**|O nome do banco de dados de assinatura.|  
|**status**|**tinyint**|O status da assinatura:<br /><br /> **0** = inativo.<br /><br /> **1** = assinado.<br /><br /> **2** = ativo.|  
|**sync_type**|**tinyint**|O tipo de sincronização inicial:<br /><br /> **1** = automatic.<br /><br /> **2** = none.|  
|**login_name**|**sysname**|O nome de logon usado ao conectar ao Publicador para adicionar a assinatura.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> **0** = push - o agente de distribuição é executado no distribuidor.<br /><br /> **1** = pull - o agente de distribuição é executado no assinante.|  
|**distribution_jobid**|**binary(16)**|Identifica o trabalho do Distribution Agent usado para sincronizar a assinatura.|  
|**timestmap**|**timestamp**|A data e hora em que a assinatura foi criada.|  
|**update_mode**|**tinyint**|O modo de atualização:<br /><br /> **0** = somente leitura.<br /><br /> **1** = atualização imediata.|  
|**loopback_detection**|**bit**|Aplica-se a assinaturas que fazem parte de uma topologia de replicação transacional bidirecional. A detecção de loopback determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante:<br /><br /> **0** = envia de volta.<br /><br /> **1** = não envia de volta.|  
|**queued_reinit**|**bit**|Especifica se o artigo é marcado para inicialização ou reinicialização. Um valor de **1** Especifica que o artigo subscrito está marcado para inicialização ou reinicialização.|  
|**nosync_type**|**tinyint**|O tipo de inicialização de assinatura :<br /><br /> **0** = automático (instantâneo)<br /><br /> **1** = somente suporte de replicação<br /><br /> **2** = inicializar com backup<br /><br /> **3** = inicializar do número de sequência de log (LSN)<br /><br /> Para obter mais informações, consulte o **@sync_type** parâmetro [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).<br /><br /> **3** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|O nome do Assinante.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
