---
title: Usando transações | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 53f5813aac141c82f87f3bec5164e5d617af6cce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098198"
---
# <a name="using-transactions"></a>Usando transações
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  No SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects), o processamento de transações é feito por meio da conexão com a instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto é referenciado pela <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade do <xref:Microsoft.SqlServer.Management.Smo.Server> objeto quando a conexão é estabelecida. Métodos como <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A>e <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> pertencem à propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
## <a name="see-also"></a>Consulte também  
 [Criando programas SMO](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
