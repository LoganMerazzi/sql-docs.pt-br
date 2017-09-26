---
title: "Método (ADOX coleções) Delete | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Views::Delete
- Groups::Delete
- Indexes::raw_Delete
- Columns::raw_Delete
- Tables::Delete
- Keys::Delete
- Users::Delete
- Users::raw_Delete
- Keys::raw_Delete
- Procedures::raw_Delete
- Views::raw_Delete
- Indexes::Delete
- Procedures::Delete
- Groups::raw_Delete
- Tables::raw_Delete
- Columns::Delete
helpviewer_keywords:
- delete method [ADOX]
ms.assetid: e6b6e3a4-8952-4d79-81f4-51019c338374
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 72dd3f6d514b20bb28f9daee6fc16c5c7c346095
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="delete-method-adox-collections"></a>Excluir método (ADOX coleções)
Remove um objeto de uma coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um **Variant** que especifica o nome ou a posição ordinal (índice) do objeto a ser excluído.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o *nome* não existe na coleção.  
  
 Para [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) e [usuários](../../../ado/reference/adox-api/users-collection-adox.md) coleções, ocorrerá um erro se o provedor não oferecer suporte a excluir tabelas ou usuários, respectivamente. Para [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md) e [exibições](../../../ado/reference/adox-api/views-collection-adox.md) coleções, **excluir** falhará se o provedor não oferece suporte a comandos persistentes.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Coleção Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Coleção Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de exemplo de método (VB)-excluir](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Exemplo do método Delete de exibições (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)