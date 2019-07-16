---
title: Preparado propriedade (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee7a94a06aa574c84c01cb8b9d05ebfcdf327d44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917597"
---
# <a name="prepared-property-ado"></a>Propriedade Prepared (ADO)
Indica se é necessário salvar uma versão compilada de um [comando](../../../ado/reference/ado-api/command-object-ado.md) antes da execução.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **Boolean** valor que, se definido como **verdadeiro**, indica que o comando deve ser preparado.  
  
## <a name="remarks"></a>Comentários  
 Use o **preparado** propriedade para que o provedor de salvar uma versão preparada (ou compilada) de consulta especificada na [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade antes de um [comando](../../../ado/reference/ado-api/command-object-ado.md) do objeto primeira execução. Isso pode causar lentidão na execução de um comando primeiro, mas depois que o provedor compila um comando, o provedor usará a versão compilada do comando para qualquer execuções subsequentes, o que resultarão em desempenho aprimorado.  
  
 Se a propriedade for **falsos**, o provedor executará o **comando** objeto diretamente sem criar uma versão compilada.  
  
 Se o provedor não der suporte a preparação de comando, ele pode retornar um erro quando essa propriedade é definida como **verdadeira**. Se o provedor não retornar um erro, ele simplesmente ignora a solicitação para preparar o comando e define o **preparado** propriedade **falso**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade PREPARED (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Exemplo da propriedade Prepared (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
