---
title: MSdynamicsnapshotjobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
author: stevestein
ms.author: sstein
ms.openlocfilehash: f8822b0e7c56fe109a251365050f5aed9cdef178
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907363"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdynamicsnapshotjobs** tabela rastreia as informações de filtro de linha com parâmetros aplicadas para gerar um instantâneo de dados filtrados. Essa tabela é armazenada nos bancos de dados da publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|A ID do trabalho de instantâneo de dados filtrado.|  
|**name**|**sysname**|O nome do trabalho de instantâneo de dados filtrado.|  
|**pubid**|**uniqueidentifier**|O número de identificação exclusivo desta publicação.|  
|**job_id**|**uniqueidentifier**|A ID do trabalho do SQL Server Agent no distribuidor.|  
|**agent_id**|**int**|A ID do SQL Server Agent.|  
|**dynamic_filter_login**|**sysname**|O valor usado para avaliar a [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) função em filtros de linha com parâmetros definidos para a publicação.|  
|**dynamic_filter_hostname**|**sysname**|O valor usado para avaliar a [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) função em filtros de linha com parâmetros definidos para a publicação.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|O caminho da pasta onde os arquivos de instantâneo serão lidos se um instantâneo de dados filtrado for usado.|  
|**partition_id**|**int**|A ID da partição de dados à qual o trabalho pertence.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
