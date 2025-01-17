---
title: Conectar ao Servidor (Oracle), Propriedades da Conexão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.oracleconnection.connectionprops.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 479b0d562ffb78bc0003ca320eea0a85ab172430
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721685"
---
# <a name="connect-to-server-oracle-connection-properties"></a>Conectar ao Servidor (Oracle), Propriedades da Conexão
  Use a guia **Propriedades de Conexão** da caixa de diálogo **Conectar ao Servidor** para especificar uma opção de publicação **Gateway** ou **Completa**. Depois que um Publicador é identificado, essa opção não pode ser alterada sem descartar e reconfigurar o Publicador. Para obter mais informações, consulte [Configure an Oracle Publisher](non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
## <a name="options"></a>Opções  
 **Tipo de Publicador**  
 Selecione **Gateway** ou **Completa**. A opção **Completa** é projetada para fornecer publicações transacionais e de instantâneo com o conjunto completo de recursos com suporte para publicações Oracle. A opção **Gateway** fornece otimizações de projeto específicas para aprimorar o desempenho de casos em que a replicação serve como um gateway entre sistemas. A opção **Gateway** não poderá ser usada se você planejar publicar a mesma tabela em várias publicações transacionais. Uma tabela pode aparecer no máximo em uma publicação transacional e em qualquer número de publicações de instantâneo se você selecionar **Gateway**.  
  
 **Tempo Limite**  
 Especifique por quanto tempo o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distribuidor deve tentar se conectar ao Editor Oracle antes da ocorrência de um erro de tempo limite.  
  
## <a name="see-also"></a>Consulte também  
 [Glossário de termos para publicações Oracle](non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Performance Tuning for Oracle Publishers](non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
