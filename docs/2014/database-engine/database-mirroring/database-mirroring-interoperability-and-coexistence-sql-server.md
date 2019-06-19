---
title: 'Espelhamento de banco de dados: interoperabilidade e coexistência (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2f38e7bac91c4d65e9c6209d693a598466096069
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807248"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>Espelhamento de banco de dados: Interoperabilidade e coexistência (SQL Server)
  O espelhamento de banco de dados pode ser usado com os seguintes recursos ou componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Instâncias de Cluster de Failover do AlwaysOn (SQL Server Failover Clustering)](database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [Change data capture (e controle de alterações)](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [Instantâneos do banco de dados](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
-   [Catálogos de texto completo](database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [Envio de logs](database-mirroring-and-log-shipping-sql-server.md)  
  
-   [Replicação](database-mirroring-and-replication-sql-server.md)  
  
 O espelhamento de banco de dados não interopera com o seguinte:  
  
-   Transações envolvendo todos os bancos de dados/transações distribuídas  
  
     Para obter informações sobre por que não há suporte para essas transações, consulte [Transações envolvendo todos os bancos de dados sem suporte para espelhamento de banco de dados ou Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
