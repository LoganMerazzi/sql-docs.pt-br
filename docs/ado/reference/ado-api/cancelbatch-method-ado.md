---
title: Método CancelBatch (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f1c6a9f57d30b47641b9280e25a97336c28b0496
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920167"
---
# <a name="cancelbatch-method-ado"></a>Método CancelBatch (ADO)
Cancela uma atualização em lotes pendentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Opcional. Uma [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que indica quantos registros o **CancelBatch** método afetará.  
  
## <a name="remarks"></a>Comentários  
 Use o **CancelBatch** método Cancelar todas as atualizações pendentes em um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) no modo de atualização em lotes. Se o **conjunto de registros** está no modo de atualização imediata, chamando **CancelBatch** sem **adAffectCurrent** gera um erro.  
  
 Se você estiver editando o registro atual ou se estiver adicionando um novo registro, quando você chama **CancelBatch**, ADO primeiro chama o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método cancelar qualquer armazenado em cache as alterações. Depois disso, todas as alterações pendentes a **Recordset** são canceladas.  
  
 O registro atual pode ser indeterminável após um **CancelBatch** chamar, especialmente se você estava no processo de adicionar um novo registro. Por esse motivo, é recomendável definir a posição do registro atual em um local conhecido na **conjunto de registros** depois que o **CancelBatch** chamar. Por exemplo, chamar o [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método.  
  
 Se a tentativa de cancelar as atualizações pendentes falhar devido a um conflito com os dados subjacentes (por exemplo, se um registro tiver sido excluído por outro usuário), o provedor retornará avisos para o [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção, mas não para execução do programa. Um erro de tempo de execução ocorre somente se houver conflitos em todos os registros solicitados. Use o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade (**adFilterAffectedRecords**) e o [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade para localizar registros com conflitos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de UpdateBatch e CancelBatch exemplo dos métodos (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Exemplo de UpdateBatch e CancelBatch exemplo dos métodos (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Método Cancel (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propriedade LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
