---
title: Propriedade (ADO Stream) size | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e52d05cdbc0fe0ca397c3a7b417fec72703b8e1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916937"
---
# <a name="size-property-ado-stream"></a>Propriedade Size (Fluxo do ADO)
Indica o tamanho do fluxo no número de bytes.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **longo** valor que especifica o tamanho do fluxo no número de bytes. O valor padrão é o tamanho do fluxo ou -1 se o tamanho do fluxo não for conhecido.  
  
## <a name="remarks"></a>Comentários  
 **Tamanho** pode ser usado apenas com aberto [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
> [!NOTE]
>  Qualquer número de bits pode ser armazenado em uma **Stream** objeto, limitado apenas pelos recursos do sistema. Se o **Stream** contém bits maior do que pode ser representado por uma **longo** valor, **tamanho** será truncado e, portanto, não representar com exatidão o comprimento do **Stream**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Size (Parâmetro ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
