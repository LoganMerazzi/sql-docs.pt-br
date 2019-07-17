---
title: Arquitetura lógica (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b6b33ffbf59cf05bc5455d3daac437e9e79407c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165607"
---
# <a name="understanding-microsoft-olap-logical-architecture"></a>Noções básicas da arquitetura lógica do Microsoft OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usa componentes cliente e servidor para fornecer processamento analítico online (OLAP) e funcionalidade de mineração de dados para aplicativos de business intelligence:  
  
-   O componente de servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é implementado como um serviço do Microsoft Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dá suporte a várias instâncias no mesmo computador, com cada instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementado como uma instância separada do serviço do Windows.  
  
-   Os clientes comunicam-se com o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usando o XMLA padrão público, um protocolo baseado em SOAP para emissão de comandos e recebimento de respostas, expostos como um serviço Web. Os modelos de objeto de cliente são também fornecidos por XMLA e podem ser acessados pelo uso de um provedor gerenciado, como ADOMD.NET ou um provedor OLE DB.  
  
-   Comandos de consulta podem ser emitidos usando as seguintes linguagens: SQL; Expressões MDX (multidimensional), uma linguagem de consulta padrão do setor para análise; ou extensões DMX (Data Mining), uma linguagem de consulta padrão do setor orientada para mineração de dados. O ASSL (Analysis Services Scripting Language) também pode ser usado para gerenciar objetos de banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] também oferece suporte a um mecanismo de cubo local, permitindo que aplicativos em clientes desconectados naveguem em dados multidimensionais armazenados localmente. Para obter mais informações, consulte [requisitos de arquitetura de cliente para o desenvolvimento do Analysis Services](../../../analysis-services/multidimensional-models/olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>Nesta seção  
 **Visão geral da arquitetura lógica**  
 [Visão geral da arquitetura lógica &#40;Analysis Services - dados multidimensionais&#41;](../../../analysis-services/multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **Objetos de servidor**  
 [Objetos de servidor &#40;Analysis Services - dados multidimensionais&#41;](../../../analysis-services/multidimensional-models/olap-logical/server-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de banco de dados**  
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos de dimensão**  
 [Objetos de dimensão &#40;Analysis Services - dados multidimensionais&#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Objetos Cube**  
 [Objetos de cubo &#40;Analysis Services - dados multidimensionais&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **Segurança de acesso do usuário**  
 [Arquitetura de segurança de acesso do usuário](http://msdn.microsoft.com/library/71b44e10-2bd0-44f7-8de9-7c8f5b7ac082)  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre a arquitetura Microsoft OLAP](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [Arquitetura física &#40;Analysis Services - dados multidimensionais&#41;](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
