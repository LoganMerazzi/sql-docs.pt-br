---
title: dbo. server_quotas (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 90df7425c7265db141d393b774728a8fe2662061
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033043"
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **IMPORTANTE:** Isso se aplica ao  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 apenas!**  
>   
>  Esse recurso está em um estado de visualização. Não usa uma dependência na implementação específica desse recurso porque o recurso pode ser alterado ou removido em uma versão futura.  
  
 Retorna os tipos de quota de bancos de dados disponíveis no servidor.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|O tipo de quota para o servidor. O tipo **Premium_database** é equivalente a bancos de dados com uma reserva de recursos.|  
|quota_value|**int**|O número do tipo de quota permitido no servidor.|  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível para todas as funções de usuário com permissões para se conectar ao virtual **mestre** banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando bancos de dados Premium](https://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
