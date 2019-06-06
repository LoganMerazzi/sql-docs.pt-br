---
title: Objeto (ADO MD) de dimensão | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f69acfa84272e73bcafb370eb85c6a14614a367c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709439"
---
# <a name="dimension-object-ado-md"></a>Objeto Dimension (ADO MD)
Representa uma das dimensões de um cubo multidimensional, que contém uma ou mais hierarquias de membros.  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um **dimensão** do objeto, você pode fazer o seguinte:  
  
-   Identificar o **dimensão** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propriedades.  
  
-   Retornar uma cadeia de caracteres significativa que descreve o **dimensão** com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Retornar o [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) objetos que compõem o **dimensão** com o [hierarquias](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) coleção.  
  
-   Use o padrão ADO [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção para obter informações adicionais sobre o **dimensão** objeto.  
  
 O **propriedades** coleção contém propriedades fornecidos pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades reais pode diferir dependendo após a implementação do provedor. Consulte a documentação do seu provedor para obter uma lista completa de propriedades disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual pertence este cubo.|  
|CubeName|O nome do cubo.|  
|DefaultHierarchy|O nome exclusivo da hierarquia padrão.|  
|Descrição|Uma descrição significativa do cubo.|  
|DimensionCaption|Um rótulo ou legenda associada à dimensão.|  
|DimensionCardinality|O número de membros na dimensão.|  
|DimensionGUID|O GUID da dimensão.|  
|DimensionName|O nome da dimensão.|  
|DimensionOrdinal|O número ordinal da dimensão entre o grupo de dimensões que formam o cubo.|  
|DimensionType|O tipo de dimensão.|  
|DimensionUniqueName|O nome não ambíguo da dimensão.|  
|SchemaName|O nome do esquema ao qual pertence este cubo.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Coleção de dimensões (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Coleção hierarquias (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
