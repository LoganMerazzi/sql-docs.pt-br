---
title: WillChangeRecord e RecordChangeComplete eventos (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b72e7f1a2e69b23f9c696a5ce544153a5a0e8a3e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord e RecordChangeComplete eventos (ADO)
O **WillChangeRecord** evento é chamado antes de um ou mais registros (linhas) [registros](../../../ado/reference/ado-api/recordset-object-ado.md) alterar. O **RecordChangeComplete** evento é chamado depois que um ou mais registros de alteração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *adReason*  
 Um [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md) valor que especifica o motivo para esse evento. Seu valor pode ser **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, ou **adRsnFirstChange**.  
  
 *cRecords*  
 Um **longo** valor que indica o número de registros de alteração (afetado).  
  
 *pError*  
 Um [erro](../../../ado/reference/ado-api/error-object.md) objeto. Descreve o erro ocorrido se o valor de *adStatus* é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status.  
  
 Quando **WillChangeRecord** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida. Ele é definido como **adStatusCantDeny** se esse evento não é possível solicitar o cancelamento da operação pendente.  
  
 Quando **RecordChangeComplete** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, ou para **adStatusErrorsOccurred** se a operação falhou.  
  
 Antes de **WillChangeRecord** retorna, defina este parâmetro como **adStatusCancel** a solicitação de cancelamento da operação que causou este evento ou definir esse parâmetro como ** adStatusUnwantedEvent** para impedir que as notificações subsequentes.  
  
 Antes de **RecordChangeComplete** retorna, defina este parâmetro como **adStatusUnwantedEvent** para impedir que as notificações subsequentes.  
  
 *pRecordset*  
 Um **registros** objeto. O **registros** para que esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Um **WillChangeRecord** ou **RecordChangeComplete** evento pode ocorrer para o primeiro campo alterado em uma linha devido ao seguinte **registros** operações: [ Atualização](../../../ado/reference/ado-api/update-method.md), [excluir](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md), [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), e [ CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). O valor da **registros** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) determina quais operações fazer com que os eventos ocorra.  
  
 Durante o **WillChangeRecord** evento, o **registros** [filtro](../../../ado/reference/ado-api/filter-property.md) está definida como **adFilterAffectedRecords**. Você não pode alterar essa propriedade ao processar o evento.  
  
 Você deve definir o **adStatus** parâmetro **adStatusUnwantedEvent** para cada possível **adReason** valor pare completamente a notificação de eventos para qualquer evento que inclui um **adReason** parâmetro.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)