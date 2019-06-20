---
title: sp_help_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c809679694811d23b01dee426aa1afdd7d5cf06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63017824"
---
# <a name="sphelptargetserver-transact-sql"></a>sp_help_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista todos os servidores de destino.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'server_name'` O nome do servidor para o qual retornar informações. *nome_do_servidor* está **nvarchar (30)**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se *nome_do_servidor* não for especificado, **sp_help_targetserver** retorna este conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Número de identificação do servidor.|  
|**server_name**|**nvarchar(30)**|Nome de servidor.|  
|**location**|**nvarchar(200)**|Localização do servidor especificado.|  
|**time_zone_adjustment**|**int**|Ajuste de fuso horário, em horas, com base na hora de Greenwich (GMT).|  
|**enlist_date**|**datetime**|Data do alistamento do servidor especificado.|  
|**last_poll_date**|**datetime**|Data da última vez em que o servidor foi  sondado para trabalhos.|  
|**status**|**int**|Status do servidor especificado.|  
|**unread_instructions**|**int**|Indica se o servidor tem ordens não lidas. Se todas as linhas tiverem sido baixadas, esta coluna é **0**.|  
|**local_time**|**datetime**|Data e hora locais do servidor de destino, baseadas na hora local do servidor de destino até a última sondagem do servidor mestre.|  
|**enlisted_by_nt_user**|**nvarchar(100)**|Usuário de Microsoft Windows que inscreveu o servidor de destino.|  
|**poll_interval**|**int**|Frequência em segundos com que o servidor de destino sonda o serviço Master SQLServer Agent para baixar trabalhos e carregar o status dos trabalhos.|  
  
## <a name="permissions"></a>Permissões  
 Para executar este procedimento armazenado, o usuário deve ser um membro da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>A. Listando informações para todos os servidores de destino registrados  
 O exemplo a seguir lista as informações de todos os servidores de destino registrados.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. Listando informações de um servidor de destino específico.  
 O exemplo a seguir lista as informações do servidor de destino `SEATTLE2`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_delete_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [dbo.sysdownloadlist &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
