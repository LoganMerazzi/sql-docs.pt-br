---
title: Propriedade MarshalOptions (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0212f3b4cb663bd56adaa1bdbc3ab6675c3ce888
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932279"
---
# <a name="marshaloptions-property-ado"></a>Propriedade MarshalOptions (ADO)
Indica quais registros da [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) devem ser empacotados de volta para o servidor.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um [MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md) valor. O valor padrão é **adMarshalAll**.  
  
## <a name="remarks"></a>Comentários  
 Ao usar um cliente [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), registros que foram modificados no cliente são gravados de volta na camada intermediária ou o servidor Web por meio de uma técnica chamada de empacotamento, o processo de empacotamento e método de interface de envio parâmetros entre os limites de thread ou processo. Definindo o **MarshalOptions** propriedade pode melhorar o desempenho quando os dados remotos modificados tem o marshaling realizados para a atualização para o servidor Web ou de camada intermediária.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** essa propriedade é usada somente em um lado do cliente **conjunto de registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade MarshalOptions (VB)](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [Exemplo da propriedade MarshalOptions (VC++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   
