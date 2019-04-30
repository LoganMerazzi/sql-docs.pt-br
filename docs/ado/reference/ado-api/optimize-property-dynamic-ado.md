---
title: Otimizar a propriedade dinâmica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d461d0fad834dfc3c3c6f22ec64cc4987eca6fa5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240041"
---
# <a name="optimize-property-dynamic-ado"></a>Otimizar a propriedade dinâmica (ADO)
Especifica se um índice deve ser criado em uma [campo](../../../ado/reference/ado-api/field-object.md).  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **Boolean** valor que indica se um índice deve ser criado.  
  
## <a name="remarks"></a>Comentários  
 Um índice pode melhorar o desempenho de operações que encontrar ou classificar valores em uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). O índice é interno ao ADO; Você não pode acessar ou usá-lo em seu aplicativo explicitamente.  
  
 Para criar um índice em um campo, defina as **otimizar** propriedade **verdadeiro**. Para excluir o índice, defina essa propriedade como **falsos**.  
  
 **Otimizar** uma propriedade dinâmica que é acrescentada ao [campo](../../../ado/reference/ado-api/field-object.md) objeto [as propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) estiver definida como **adUseClient**.  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Otimizar o exemplo da propriedade (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Otimizar o exemplo da propriedade (VC + +)](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [Propriedade de filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Método Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Propriedade Sort](../../../ado/reference/ado-api/sort-property.md)
