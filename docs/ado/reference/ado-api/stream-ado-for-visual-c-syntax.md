---
title: Stream (sintaxe do ADO para Visual C++) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- Stream collection [ADO]
ms.assetid: dddcceef-9296-4fb3-8eca-94b17d0148de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77da08e1d6ead2ad5777f41113a1ed164a7fb5da
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062614"
---
# <a name="stream-ado-for-visual-c-syntax"></a>Fluxo (Sintaxe do ADO para Visual C++)
## <a name="methods"></a>Métodos  
  
```  
Cancel(void)  
Close(void)  
CopyTo(_ADOStream *DestStream, LONG CharNumber = -1)  
Flush(void)  
LoadFromFile(BSTR FileName)  
Open(VARIANT Source, ConnectModeEnum Mode, StreamOpenOptionsEnum Options, BSTR UserName, BSTR Password)  
Read(long NumBytes, VARIANT *pVal)  
ReadText(long NumChars, BSTR *pbstr)  
SaveToFile(BSTR FileName, SaveOptionsEnum Options = adSaveCreateNotExist)  
SetEOS(void)  
SkipLine(void)  
Write(VARIANT Buffer)  
WriteText(BSTR Data, StreamWriteEnum Options = adWriteChar)  
```  
  
## <a name="properties"></a>Propriedades  
  
```  
get_Charset(BSTR *pbstrCharset)  
put_Charset(BSTR Charset)  
get_EOS(VARIANT_BOOL *pEOS)  
get_LineSeparator(LineSeparatorEnum *pLS)  
put_LineSeparator(LineSeparatorEnum LineSeparator)  
get_Mode(ConnectModeEnum *pMode)  
put_Mode(ConnectModeEnum Mode)  
get_Position(LONG *pPos)  
put_Position(LONG Position)  
get_Size(LONG *pSize)  
get_State(ObjectStateEnum *pState)  
get_Type(StreamTypeEnum *pType)  
put_Type(StreamTypeEnum Type)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
