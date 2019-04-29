---
title: sp_helpreplfailovermode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f733740b062983f14379f71a48b77f73392aceae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62865278"
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe o modo de failover atual de uma assinatura. Esse procedimento armazenado é executado no Assinante, em qualquer banco de dados. Para obter mais informações sobre modos de failover, consulte [assinaturas atualizáveis para replicação transacional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` É o nome do publicador que está participando da atualização desse assinante. *Publisher* está **sysname**, sem padrão. O Publicador já deve estar configurado para publicação.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados de publicação. *publisher_db* está **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'` É o nome da publicação que está participando da atualização desse assinante. *publicação*está **sysname**, sem padrão.  
  
`[ @failover_mode_id = ] 'failover_mode_id' OUTPUT` Retorna o valor inteiro do modo de failover e é um **saída** parâmetro. *failover_mode_id* é um **tinyint** com um padrão de **0**. Ele retorna **0** para atualização imediata e **1** de atualização enfileirada.  
  
 [**@failover_mode=**] **'***failover_mode***'OUTPUT**  
 Retorna o modo no qual são feitas modificações de dados no Assinante. *failover_mode* é um **nvarchar (10)** com um padrão NULL. É um **saída** parâmetro.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**immediate**|Atualização imediata: as atualizações feitas no Assinante são imediatamente propagadas no Publicador, usando 2PC (protocolo de confirmação de duas fases).|  
|**queued**|Atualização enfileirada: atualizações feitas no Assinante são armazenadas em uma fila.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpreplfailovermode** é usado em replicação de instantâneo ou replicação transacional para quais assinaturas são habilitadas para atualização imediata com atualização enfileirada como failover, em caso de falha.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_helpreplfailovermode**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
