---
title: Cálculos (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 738816e3-0e1d-44a5-8d1b-81068dce8ac0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b19dce00f95559aec77c8d02c86631faadc466b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757574"
---
# <a name="calculations-ssas-tabular"></a>Cálculos (SSAS tabular)
  Depois de importar dados para o modelo, será possível adicionar cálculos para agregar, filtrar, estender, combinar e proteger esses dados. Os modelos tabulares usam o DAX (Data Analysis Expressions), uma linguagem de fórmula para criar cálculos personalizados. Nos modelos de tabela, os cálculos que você cria usando fórmulas DAX são usados em *Colunas Calculadas*, *Medidas*e *Filtros de Linha*.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Noções básicas sobre DAX em modelos de tabela &#40;SSAS de Tabela&#41;](understanding-dax-in-tabular-models-ssas-tabular.md)|Descreve a linguagem de fórmula DAX usada para criar cálculos para colunas calculadas, medidas e filtros de linha em modelos de tabela.|  
|[Compatibilidade de fórmulas no modo DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|Descreve as diferenças, lista as funções que não têm suporte no modo DirectQuery e lista as funções com suporte, mas que poderiam retornar resultados diferentes.|  
|[Expressões de análise de dados &#40;DAX&#41; referência](https://msdn.microsoft.com/library/gg413422(v=sql.120).aspx)|Esta seção fornece descrições detalhadas de sintaxe DAX, operadores e funções.|  
  
> [!NOTE]  
>  Esta seção não contém tarefas passo a passo para criar cálculos. Como os cálculos são especificados em colunas calculadas, medidas e filtros de linha (em funções), as instruções sobre onde criar fórmulas DAX são fornecidas em tarefas relacionadas a esses recursos. Para obter mais informações, consulte [Criar uma coluna calculada &#40;SSAS de Tabela&#41;](ssas-calculated-columns-create-a-calculated-column.md), [Criar e gerenciar medidas &#40;SSAS de Tabela&#41;](measures-ssas-tabular.md) e [Criar e gerenciar funções &#40;SSAS de Tabela&#41;](roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Apesar de o DAX também poder ser usado para consultar um modelo de tabela, tópicos desta seção destacam especificamente o uso de fórmulas DAX para criar cálculos.  
  
  
