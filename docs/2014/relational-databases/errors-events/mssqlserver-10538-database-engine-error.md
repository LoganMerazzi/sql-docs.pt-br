---
title: MSSQLSERVER_10538 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa6bce659e20fb80f013539049cc1b99e3e0b4c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870636"
---
# <a name="mssqlserver10538"></a>MSSQLSERVER_10538
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10538|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_INVALID_PLANGUIDE_HANDLE|  
|Texto da mensagem|Não foi possível encontrar o guia de plano porque a ID do guia de plano especificada é NULL ou inválida ou você não tem permissão no objeto referenciado pelo guia de plano. Verifique se a ID do guia de plano é válida, se a sessão atual está definida com o contexto de banco de dados correto e se você tem a permissão ALTER DATABASE ou ALTER no objeto referenciado pelo guia de plano.|  
  
## <a name="explanation"></a>Explicação  
 A ID do plano de guia especificado é NULL ou inválida ou você não tem permissão no objeto referenciado pelo guia de plano.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se a ID do guia de plano é válida, se a sessão atual está definida com o contexto de banco de dados correto e se você tem a permissão ALTER DATABASE ou ALTER no objeto referenciado pelo guia de plano.  
  
## <a name="see-also"></a>Consulte também  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guias de plano](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
