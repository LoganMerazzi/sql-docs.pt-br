---
title: ObjectStateEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 41b72647af357bc73eb3e9a2f8c3063f2275f6a6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707182"
---
# <a name="objectstateenum"></a>ObjectStateEnum
Especifica se um objeto é aberto ou fechado, conectando a uma fonte de dados, executar um comando ou a recuperação de dados.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|Indica que o objeto está fechado.|  
|**adStateOpen**|1|Indica que o objeto está aberto.|  
|**adStateConnecting**|2|Indica que o objeto está se conectando.|  
|**adStateExecuting**|4|Indica que o objeto está executando um comando.|  
|**adStateFetching**|8|Indica que as linhas do objeto estão sendo recuperadas.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Propriedade State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[Propriedade State (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
