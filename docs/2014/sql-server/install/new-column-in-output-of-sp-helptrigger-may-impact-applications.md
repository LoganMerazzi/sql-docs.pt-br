---
title: Nova coluna na saída de sp_helptrigger pode impactar os aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- sp_helptrigger
ms.assetid: b7c42a8f-f2e0-4fa3-b046-3cf39c854c47
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c7ad878072f8139cc95d6dc34c01f5f48835774a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59581653"
---
# <a name="new-column-in-output-of-sphelptrigger-may-impact-applications"></a>Coluna nova no resultado do sp_helptrigger pode impactar nos aplicativos
  procedimento armazenado do trigger_schemaias a última coluna no conjunto de resultados retornada pelo sistema, sp_helptrigger.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Para obter informações sobre gatilhos definidos em uma tabela particular, consulte a exibição do catálogo sys.triggers.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Revise o uso de aplicativos sp_helptrigger. Talvez seja necessário modificar seus aplicativos para acomodar a coluna adicional. Como alternativa, você pode usar a exibição do catálogo sys.triggers.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
