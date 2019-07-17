---
title: Objetos (Analysis Services - dados multidimensionais) do banco de dados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c7b9bab0da5b00e77696217974dee5eb5d1d522
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165635"
---
# <a name="database-objects-analysis-services---multidimensional-data"></a>Objetos de banco de dados (Analysis Services – Dados Multidimensionais)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância contém assemblies para uso com o processamento analítico online (OLAP) e mineração de dados e objetos de banco de dados.  
  
-   Os bancos de dados contêm objetos OLAP e dados de mineração, como fontes de dados, exibições de fonte de dados, cubos, medidas, grupos de medidas, dimensões, atributos, hierarquias, estruturas de mineração de dados, modelos de mineração de dados e funções.  
  
-   Os assemblies contêm funções definidas pelo usuário que ampliam a funcionalidade de funções intrínsecas, fornecidas com as linguagens MDX e extensões de mineração de dados (DMX).  
  
 O objeto <xref:Microsoft.AnalysisServices.Database> é o contêiner de todos os objetos de dados necessários para um projeto de business intelligence (como cubos OLAP, dimensões e estruturas de mineração de dados) e seus objetos de suporte (como <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.Account> e <xref:Microsoft.AnalysisServices.Role>).  
  
 Um objeto <xref:Microsoft.AnalysisServices.Database> fornece acesso a objetos e atributos incluindo o seguinte:  
  
-   Todos os cubos que você pode acessar, como uma coleção.  
  
-   Todas as dimensões que você pode acessar, como uma coleção.  
  
-   Todas as estruturas de mineração que você pode acessar, como uma coleção.  
  
-   Todas as fontes de dados e exibições de fonte de dados, como duas coleções.  
  
-   Todas as funções e permissões de banco de dados, como duas coleções.  
  
-   O valor da ordenação para o banco de dados.  
  
-   O tamanho estimado do banco de dados.  
  
-   O valor do idioma do banco de dados.  
  
-   A configuração visível do banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos seguintes descrevem objetos compartilhados por recursos OLAP e mineração de dados no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Fontes de dados em modelos multidimensionais](../../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)|Descreve uma fonte de dados no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Exibições de fontes de dados em modelos multidimensionais](../../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)|Descreve um modelo de dados lógico baseado em uma ou mais fontes de dados, no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Cubos em modelos multidimensionais](../../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)|Descreve cubos e objetos de cubo, incluindo medidas, grupos de medidas, relações de uso de dimensão, cálculos indicadores de desempenho principais, ações, traduções, partições e perspectivas.|  
|[Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|Descreve dimensões e objetos de dimensão, inclusive atributos, relações de atributo, hierarquias, níveis e membros.|  
|[Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](../../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)|Descreve estruturas e objetos de mineração de dados, inclusive modelos de mineração de dados.|  
|[Funções de Segurança &#40;Analysis Services – Dados Multidimensionais&#41;](../../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)|Descreve uma função, o mecanismo de segurança usado para controlar o acesso a objetos no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Gerenciamento de assemblies de modelo multidimensional](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)|Descreve um assembly, uma coleção de funções definidas pelo usuário e usada para ampliar as linguagens MDX e DMX, no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados com suporte &#40;SSAS – Multidimensional&#41;](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [Soluções de modelo multidimensional](../../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [Soluções de mineração de dados](../../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
