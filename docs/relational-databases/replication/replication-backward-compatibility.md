---
title: Compatibilidade com versões anteriores de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, backward compatibility
- backward compatibility [SQL Server replication]
- merge replication backward compatibility [SQL Server replication]
- replication [SQL Server], backward compatibility
- backward compatibility [SQL Server], replication
- snapshot replication [SQL Server], backward compatibility
- compatibility [SQL Server replication]
ms.assetid: 091c51dc-8b32-4b4f-847e-b317456c8394
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6b21412bfb6555dbe9c45d411f0b1e7292e79e2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046704"
---
# <a name="replication-backward-compatibility"></a>Compatibilidade com versões anteriores de replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

É importante compreender a compatibilidade com versões anteriores se você está atualizando ou tem mais de uma versão do SQL Server em uma topologia de replicação. 

As regras gerais são: 

-   Um Distribuidor pode ser de qualquer versão, desde que ela seja maior ou igual à do Publicador (em muitos casos, o Distribuidor tem a mesma instância que o Publicador).    
-   Um Publicador pode ser de qualquer versão, contanto que ela seja menor ou igual à versão do Distribuidor.    
-   A versão de assinante depende do tipo de publicação:    
    - Um Assinante de uma publicação transacional pode ser de qualquer uma das duas versões do Publicador. Por exemplo: um publicador do SQL Server 2012 (11.x) pode ter assinantes do SQL Server 2014 (12.x) e SQL Server 2016 (13.x); e um publicador do SQL Server 2016 (13.x) pode ter assinantes do SQL Server 2014 (12.x) e SQL Server 2012 (11.x).     
    - Um assinante de uma publicação de mesclagem pode ser todas as versões iguais ou anteriores à versão do publicador com suporte, de acordo com o ciclo de vida de suporte das versões.  


## <a name="replication-matrix"></a>Matriz de replicação
[!INCLUDE[repl matrix](../../includes/replication-compat-matrix.md)]


## <a name="additional-resources"></a>Recursos adicionais
 [Recursos preteridos na Replicação do SQL Server](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)  
 Os recursos de replicação que foram retidos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para compatibilidade com versões anteriores, mas que serão removidos em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Alterações significativas na replicação do SQL Server](../../relational-databases/replication/breaking-changes-in-sql-server-replication.md)  
 Alterações de recurso da replicação que podem exigir alterações para aplicativos. 

 [Atualizar bancos de dados replicados](../../database-engine/install-windows/upgrade-replicated-databases.md)  
 Etapas e considerações ao atualizar o SQL Server que participa de uma topologia de replicação. 
  
  
