---
title: STAsText (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsText (geography Data Type)
- STAsText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText method
ms.assetid: d3d2635d-ca6c-4205-9d6c-eb939ee314fd
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 08a71fb36be4754a09e9d092dfa3120688bb499e
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936191"
---
# <a name="stastext-geography-data-type"></a>STAsText (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de **geography**. Esse texto não conterá nenhum valor Z (elevação) ou M (medida) executado pela instância.  
  
 Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de retorno CLR: **SqlChars**  
  
## <a name="remarks"></a>Remarks  
 O tipo OGC de uma instância de **geography** pode ser determinado com a invocação de [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
 No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o conjunto de possíveis resultados retornado no servidor foi estendido para instâncias **FullGlobe**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STAsText()` para criar uma instância de `LineString``geography` de (-122.360, 47.656) a (-122.343, -47.656) com base no texto. Em seguida, retorna o resultado em texto.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
