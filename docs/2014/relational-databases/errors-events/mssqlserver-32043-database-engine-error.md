---
title: MSSQLSERVER_32043 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6d58b712528de5f3f5b22317cc85e4ff74105a6e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010897"
---
# <a name="mssqlserver32043"></a>MSSQLSERVER_32043
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|32043|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum32043|  
|Texto da mensagem|O alerta de 'log não restaurado' foi ativado. O valor atual '%d' ultrapassa o limite '%d'.|  
  
## <a name="explanation"></a>Explicação  
 Esse evento de espelhamento de banco de dados é emitido na instância do servidor espelho para indicar que a quantidade de logs não restaurados alcançou um valor do limite especificado pelo usuário. Normalmente, esse evento acontece porque o desempenho do sistema foi alterado. A largura da banda entre os dois sistemas diminuiu ou a carga aumentou.  
  
 Um log não restaurado é um log que foi recebido pela instância do servidor espelho e foi gravado no disco, mas está aguardando para ser restaurado no banco de dados espelho. A quantidade de logs não restaurados em KB (quilobytes) é uma métrica de desempenho que pode ajudar a avaliar o tempo atual de failover. O tempo necessário para aplicar o log não restaurado é o fator principal no tempo de failover, além de um curto período adicional necessário para restaurar o banco de dados e fazer com que ele fique online.  
  
> [!NOTE]  
>  Em um failover automático, o tempo necessário para que o sistema perceba a falha é independente do tempo de failover.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique a causa nas cargas das instâncias do servidor principal e espelho, bem como nas respectivas conexões de rede.  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Usar os limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  