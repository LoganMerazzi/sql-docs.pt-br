---
title: sys.service_message_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
author: stevestein
ms.author: sstein
ms.openlocfilehash: 560ee8a4ccc03f747df2b475394af092db589e7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078746"
---
# <a name="sysservicemessagetypes-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta exibição do catálogo contém uma linha por tipo de mensagem registrado no agente de serviços.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome de tipo de mensagem, exclusivo no banco de dados. Não é NULLABLE.|  
|**message_type_id**|**int**|Identificador do tipo de mensagem, exclusivo no banco de dados. Não é NULLABLE.|  
|**principal_id**|**int**|Identificador para a entidade de banco de dados que possui este tipo de mensagem. É NULLABLE.|  
|**validation**|**char(2)**|Validação feita pelo Broker antes de enviar mensagens desse tipo. Não é NULLABLE. Um dos seguintes:<br /><br /> N = Nenhum<br /><br /> X = XML<br /><br /> E = vazio|  
|**validation_desc**|**nvarchar(60)**|Descrição da validação feita pelo Broker antes de enviar mensagens desse tipo. É NULLABLE. Um dos seguintes:<br /><br /> Nenhuma<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|Para validação que usa um esquema de XML, o identificador para a coleção de esquema usada.<br /><br /> Caso contrário, NULL.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
