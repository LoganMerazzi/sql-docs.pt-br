---
title: LockTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ae822794b1b06a975e1cc3cd397b5a5f00036dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918252"
---
# <a name="locktypeenum"></a>LockTypeEnum
Especifica o tipo de bloqueio colocado em registros durante a edição.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|Indica as atualizações em lotes otimista. Necessário para o modo de atualização em lotes.|  
|**adLockOptimistic**|3|Indica o bloqueio otimista, registro por registro. O provedor usa bloqueio otimista, bloqueando registros somente quando você chama o [atualização](../../../ado/reference/ado-api/update-method.md) método.|  
|**adLockPessimistic**|2|Indica o bloqueio pessimista, registro por registro. O provedor faz o que é necessário para garantir o êxito edição de registros, geralmente por bloqueando registros na fonte de dados imediatamente após a edição.|  
|**adLockReadOnly**|1|Indica os registros de somente leitura. Você não pode alterar os dados.|  
|**adLockUnspecified**|-1|Não especifica um tipo de bloqueio. Para clones, o clone é criado com o mesmo tipo de bloqueio do original.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums.LockType.OPTIMISTIC|  
|AdoEnums.LockType.PESSIMISTIC|  
|AdoEnums.LockType.READONLY|  
|AdoEnums.LockType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método Clone (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)|[Propriedade LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)|  
|[Método Open (Conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Evento WillExecute (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|
