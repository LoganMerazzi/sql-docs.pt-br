---
title: Eventos ConnectComplete e Disconnect (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Disconnect
- Connection::ConnectComplete
- ConnectComplete
- Connection::Disconnect
helpviewer_keywords:
- Disconnect event [ADO]
- ConnectComplete event [ADO]
ms.assetid: 568f5252-d069-4d99-a01b-2ada87ad1304
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 448270ddf0e8cd7efb5ec39a93d4ff993360730e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919575"
---
# <a name="connectcomplete-and-disconnect-events-ado"></a>Eventos ConnectComplete e Disconnect (ADO)
O **eventos ConnectComplete** evento é chamado depois que uma conexão é iniciado. O **desconectar** evento é chamado após o término de uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ConnectComplete pError, adStatus, pConnection  
Disconnect adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pError*  
 Uma [erro](../../../ado/reference/ado-api/error-object.md) objeto. Ele descreve o erro ocorrido se o valor de *adStatus* é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Uma [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor que sempre retorna **adStatusOK**.  
  
 Quando **eventos ConnectComplete** é chamado, esse parâmetro é definido como **adStatusCancel** se um **WillConnect** evento solicitou o cancelamento da conexão pendente.  
  
 Antes de retorna de um evento, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes. No entanto, fechar e reabrir o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) faz com que esses eventos ocorra novamente.  
  
 *pConnection*  
 O **Conexão** de objeto para o qual este evento se aplica.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
