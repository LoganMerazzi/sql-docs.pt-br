---
title: "Exibições de coleção (ADOX) | Microsoft Docs"
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
- Catalog::Views
- Views
helpviewer_keywords:
- Views collection [ADOX]
ms.assetid: a55d380c-2b7b-4b57-af74-8ba0b3de0db9
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d8c15a8add685bf62faa307fc420f51a8c547776
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="views-collection-adox"></a>Coleção de exibições (ADOX)
Contém todos os [exibição](../../../ado/reference/adox-api/view-object-adox.md) objetos de um catálogo.  
  
## <a name="remarks"></a>Comentários  
 O [Append](../../../ado/reference/adox-api/append-method-adox-views.md) método para um **exibições** coleção é exclusiva para ADOX. Você pode:  
  
-   Adicionar uma nova exibição à coleção com o **Append** método.  
  
 As propriedades e os métodos restantes são padrão para coleções de ADO. Você pode:  
  
-   Acessar uma exibição da coleção com o [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Retorna o número de modos de exibição contidos na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Remover um modo de exibição da coleção com o [excluir](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Atualizar os objetos na coleção para refletir o esquema de banco de dados atual com o [atualização](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Views](../../../ado/reference/adox-api/views-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de coleções de campos (VB) e modos de exibição](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Exibições de acrescentar o exemplo de método (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Coleção de modos de exibição, o exemplo da propriedade CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Exemplo de método (VB)-excluir exibições](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Exemplo de método (VB) de atualização de modos de exibição](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)