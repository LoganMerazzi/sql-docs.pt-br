---
title: STAsText (tipo de dados geography) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STAsText (geography Data Type)
- STAsText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText method
ms.assetid: d3d2635d-ca6c-4205-9d6c-eb939ee314fd
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f29024f7ac82979771fc897a9efc6860af08a9a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stastext-geography-data-type"></a>STAsText (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a representação de texto do Open Geospatial Consortium (OGC) conhecido (WKT) de um **geografia** instância. Esse texto não conterá nenhum valor Z (elevação) ou M (medida) executado pela instância.  
  
 Isso **geografia** método dá suporte ao tipo de dados **FullGlobe** instâncias ou a instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de retorno: **nvarchar (max)**  
  
 Tipo de retorno CLR: **SqlChars**  
  
## <a name="remarks"></a>Comentários  
 O tipo OGC de uma **geografia** instância pode ser determinada invocando [stgeometrytype ()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
 Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o conjunto de possíveis resultados retornados no servidor foi estendido para **FullGlobe** instâncias.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STAsText()` para criar um `LineString``geography` da instância de (-122.360, 47.656) a (-122.343, -47.656) de texto. Em seguida, retorna o resultado em texto.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Consulte também  
 [Métodos do OGC em instâncias de Geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  