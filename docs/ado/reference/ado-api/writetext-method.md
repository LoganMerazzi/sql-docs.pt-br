---
title: Método WriteText | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64b7d8fd3f2220562e3695d6e31c83261daa2e60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947492"
---
# <a name="writetext-method"></a>Método WriteText
Grava uma cadeia de caracteres de texto especificado para um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Dados*  
 Um **cadeia de caracteres** valor que contém o texto em caracteres a serem gravados.  
  
 *Opções*  
 Opcional. Um [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) valor que especifica se um caractere de separador de linha deve ser gravado no final da cadeia de caracteres especificada.  
  
## <a name="remarks"></a>Comentários  
 Cadeias de caracteres especificadas são gravadas para o **Stream** objeto sem espaços ou caracteres entre cada cadeia de caracteres.  
  
 O atual [posição](../../../ado/reference/ado-api/position-property-ado.md) é definido como o caractere após os dados gravados. O **WriteText** método não trunca o restante dos dados em um fluxo. Se você deseja truncar esses caracteres, chame [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 Se você gravar depois atual [EOS](../../../ado/reference/ado-api/eos-property.md) posição, o [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) da **Stream** aumenta para conter quaisquer caracteres de nova, e **EOS** passará para o novo último byte na **Stream**.  
  
> [!NOTE]
>  O **WriteText** método é usado com fluxos de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) está **adTypeText**). Para fluxos binários (**tipo** é **adTypeBinary**), use [gravar](../../../ado/reference/ado-api/write-method.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Write](../../../ado/reference/ado-api/write-method.md)
