---
title: Armazenamento de dimensão | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3d739bd19cd5be1f9b6167acbf104f569fc517ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209247"
---
# <a name="dimensions---storage"></a>Dimensões – Armazenamento
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  As dimensões no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dão suporte a dois modos de armazenamento:  
  
-   OLAP relacional (ROLAP)  
  
-   OLAP multidimensional (MOLAP)  
  
 O modo de armazenamento determina o local e a forma dos dados de uma dimensão. O MOLAP é o modo de armazenamento padrão para dimensões. **Tópicos relacionados:** [modos de armazenamento de partição e processamento](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
## <a name="molap"></a>MOLAP  
 Dados de uma dimensão que usam MOLAP são armazenados em uma estrutura multidimensional na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Essa estrutura multidimensional é criada e populada quando a dimensão é processada. As dimensões MOLAP fornecem melhores desempenho de consulta do que de dimensões ROLAP.  
  
## <a name="rolap"></a>ROLAP  
 Dados de uma dimensão que usa ROLAP são armazenados nas tabelas usadas para definir a dimensão. O modo de armazenamento ROLAP pode ser usado para oferecer suporte para grandes dimensões sem duplicar grandes quantidades de dados, mas diminuindo o desempenho da consulta. Como a dimensão depende diretamente das tabelas na exibição de fonte de dados, usados para definir a dimensão, o modo de armazenamento ROLAP também oferece suporte ao OLAP em tempo real.  
  
> [!IMPORTANT]  
>  Se a dimensão usa o modo de armazenamento ROLAP e a dimensão está incluída em um cubo que usa o armazenamento MOLAP, qualquer alteração de esquema na tabela de origem deve ser seguida por processamento imediato do cubo. Se não fizer isso, poderá gerar resultados inconsistentes quando consultar o cubo. **Tópico relacionado:** [automatizar Analysis Services tarefas administrativas com SSIS](../../analysis-services/instances/automate-analysis-services-administrative-tasks-with-ssis.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modos e processamento de armazenamento de partição](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  
