---
title: Tipos de dimensão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- time dimensions [Analysis Services]
- quantitative dimensions [Analysis Services]
- BillOfMaterials dimension [Analysis Services]
- geography dimensions
- utility dimensions [Analysis Services]
- channel dimensions
- dimensions [Analysis Services], types
- products dimensions [Analysis Services]
- account dimensions [Analysis Services]
- organization dimensions
- currency dimensions [Analysis Services]
- rates dimensions
- promotion dimensions
- scenario dimensions [Analysis Services]
- customers dimensions [Analysis Services]
- Type property
ms.assetid: bd3195da-e762-4c98-b643-34c76e842343
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbe1c8932c082ce537cd5dc3f2b12d98c05c3811
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62728552"
---
# <a name="dimension-types"></a>Tipos de dimensão
  A configuração da propriedade `Type` fornece informações sobre os conteúdos de uma dimensão para servidor e aplicativos cliente. Em alguns casos, a configuração `Type` fornece somente orientação para aplicativos cliente e é opcional. Em outros casos, como as dimensões `Accounts` ou `Time`, as configurações de propriedade `Type` da dimensão e seus atributos determinam comportamentos específicos baseados em servidor e podem ser necessários para implantar determinados comportamentos no cubo. Por exemplo, a propriedade `Type` de uma dimensão pode ser configurada como `Accounts` para indicar a aplicativos cliente que a dimensão padrão contém atributos de conta. Para obter mais informações sobre o tempo, conta e dimensões de moeda, consulte [criar uma dimensão de tipo de data](../multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [criar uma conta de Finanças de dimensão de tipo de pai-filho](../multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), e [criar uma moeda tipo de dimensão](../multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 A configuração padrão para o tipo de dimensão é `Regular` que não faz nenhuma suposição sobre o conteúdo da dimensão. Essa é a configuração padrão para todas as dimensões quando você define inicialmente uma dimensão a menos que você especifique`Time` ao definir a dimensão usando o Assistente de Dimensão. Você também deve deixar o `Regular` como o tipo de dimensão, se o Assistente de Dimensão não oferecer um tipo de dimensão apropriado.  
  
## <a name="available-dimension-types"></a>Tipos de dimensão disponíveis  
 A tabela a seguir descreve os tipos de dimensão disponíveis no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Tipo de dimensão|Descrição|  
|--------------------|-----------------|  
|Regular|Uma dimensão cujo tipo não foi definido como um tipo de dimensão especial.|  
|Time|Uma dimensão cujos atributos representam períodos, como anos, semestres, trimestres, meses e dias.|  
|Organização|Uma dimensão cujos atributos representam informações organizacionais, como funcionários ou subsidiárias.|  
|Geografia|Uma dimensão cujos atributos representam informações geográficas, como cidades ou códigos postais.|  
|BillOfMaterials|Uma dimensão cujos atributos representam informações de estoque ou manufatura, como listas de peças para produtos.|  
|Contas|Uma dimensão cujos atributos representam um plano de contas para fins de geração de relatórios financeiros.|  
|Customers|Uma dimensão cujos atributos representam informações do cliente ou de contato.|  
|Products|Uma dimensão cujos atributos representam informações de produto.|  
|Cenário|Uma dimensão cujos atributos representam informações de planejamento ou de análise estratégica.|  
|Quantitative|Uma dimensão cujos atributos representam informações quantitativas.|  
|Utilitário|Uma dimensão cujos atributos representam informações diversas.|  
|Currency|Este tipo de dimensão contém dados e metadados de moeda.|  
|Rates|Uma dimensão cujos atributos representam informações de taxa de moeda.|  
|Canal|Uma dimensão cujos atributos representam informações de canal.|  
|Promoção|Uma dimensão cujos atributos representam informações de promoções de marketing.|  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma dimensão usando uma tabela existente](../multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
