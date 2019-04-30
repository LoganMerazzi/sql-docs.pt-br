---
title: Método Clear (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e69e7d2d2a66ccb9df0e03f6f77849c502f3bf2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239755"
---
# <a name="clear-method-ado"></a>Método Clear (ADO)
Remove todos os [erro](../../../ado/reference/ado-api/error-object.md) objetos da [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>Comentários  
 Use o **clara** método na [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção para remover todas as existentes [erro](../../../ado/reference/ado-api/error-object.md) objetos da coleção. Quando ocorre um erro, ADO limpa automaticamente o **erros** coleção e a preenche com **erro** objetos com base em um novo erro.  
  
 Algumas propriedades e métodos retornam os avisos que aparecem como **erro** objetos na **erros** coleção, mas não interrompem a execução de um programa. Antes de chamar o [ressincronizar](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos em um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) do objeto; o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto; ou defina o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade em um **Recordset** de objeto, chame o **limpar**método de **erros** coleção. Dessa forma, você pode ler o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade da **erros** avisos retornados de coleção para testar.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Execute, Requery e Clear exemplo dos métodos (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery e Clear exemplo dos métodos (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery e Clear exemplo dos métodos (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método Delete (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Excluir método (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Propriedade de filtro](../../../ado/reference/ado-api/filter-property.md)   
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
