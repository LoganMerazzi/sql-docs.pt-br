---
title: Modificar conexões que usam protocolos de rede Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk ou NWLink IPX SPX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- network protocols [SQL Server], modifying connections
- SPP [SQL Server]
- NWLink IPX/SPX [SQL Server]
- connections [SQL Server]
- AppleTalk [SQL Server]
- Sequenced Packet Protocol [SQL Server]
- Multiprotocol Net-Library [SQL Server]
- Banyan VINES Sequenced Package Protocol [SQL Server]
- IPX/SPX [SQL Server]
- protocols [SQL Server], modifying connections
- RPC [SQL Server]
ms.assetid: 5c5ae453-cc5b-4898-95c7-ad34157b1f60
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cdbcaa39e3d9630bd4ea50919f31cdbb15a36d14
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093895"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>Modificar conexões que usam protocolo de rede Banyan VINES SPP (Sequenced Packet Protocol), Multiprotocol, AppleTalk ou NWLink IPX/SPX
  O Supervisor de Atualização detectou protocolos de conectividade cliente/servidor para os quais não há suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Os aplicativos cliente que usam protocolo de rede Banyan VINES SPP, Multiprotocol, AppleTalk ou NWLink IPX/SPX devem conectar-se usando um protocolo para o qual há suporte.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não oferece suporte aos protocolos de rede Banyan VINES SPP, Multiprotocol, AppleTalk e NWLink IPX/SPX. Os clientes que se conectavam anteriormente usando esses protocolos devem selecionar um protocolo diferente.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Altere as configurações dos aplicativos cliente para que usem um protocolo para o qual há suporte ao conectar-se com o servidor. Se você tiver uma instalação de alias que use protocolos sem-suporte, esse alias deve ser modificado para que use protocolos para os quais há suporte.  
  
 Se sua conexão de aplicativo de cadeia de caracteres especificamente usa ou carrega um desses protocolos, por qualquer rede especificando = DBMSRPCN para RPC, NETWORK = DBMSADSN para Appletalk ou NETWORK = DBMSVINN para a propriedade Banyan VINES, ou usando um prefixo explícito como "spx: *servidor \ instância*"para SPX," bv:*server*"para Banyan VINES," adsp:*servidor*"para AppleTalk, ou" rpc:*server*"para vários protocolos, em seguida, você deve modificar seu aplicativo para usar um dos protocolos com suporte.  
  
 Para obter mais informações, consulte ‘Escolhendo um protocolo de rede’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
