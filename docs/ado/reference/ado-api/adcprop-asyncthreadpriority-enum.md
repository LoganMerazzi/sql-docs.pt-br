---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22a8cd4bb8d1bdddbaaa68e92349d9c728557ac0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921463"
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
Para um RDS [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) de objeto, que especifica a prioridade de execução do thread assíncrona que recupera dados.  
  
 Usar essas constantes com a **conjunto de registros** "**prioridade de Thread em segundo plano**" propriedade dinâmica, que é referenciada no índice ADO para OLE DB de propriedade dinâmica e documentada no [ Microsoft Cursor Service para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|Define a prioridade entre normal e o mais alto.|  
|**adPriorityBelowNormal**|2|Define a prioridade entre mais baixa e normal.|  
|**adPriorityHighest**|5|Define a prioridade para a mais alta possível.|  
|**AdPriorityLowest**|1|Define a prioridade para o nível mais baixo possível.|  
|**adPriorityNormal**|3|Define a prioridade como normal.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
