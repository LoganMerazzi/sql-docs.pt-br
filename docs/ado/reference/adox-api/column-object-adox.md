---
title: Objeto Column (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7dcec7e665fec8ea1eb1e1dff8d08bb59ee92133
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708018"
---
# <a name="column-object-adox"></a>Objeto Column (ADOX)
Representa uma coluna de uma tabela, índice ou chave.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria um novo **coluna**:  
  
 `Dim obj As New Column`  
  
 Com as propriedades e coleções de uma **coluna** do objeto, você pode:  
  
-   Identificar a coluna com o [nome da propriedade (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Especifique o tipo de dados da coluna com o [propriedade Type (Key) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md) propriedade.  
  
-   Determinar se a coluna for de comprimento fixo ou se ele pode conter valores nulos com o [atributos de propriedade (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md) propriedade.  
  
-   Especifique o tamanho máximo da coluna com o [propriedade DefinedSize (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md) propriedade.  
  
-   Para obter valores de dados numéricos, especifique a escala com o [Propriedade NumericScale (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md) propriedade.  
  
-   Para obter o valor de dados numérico, especifique a precisão máxima com o [propriedade Precision (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md) propriedade.  
  
-   Especifique o [catálogo de objeto (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md) que possui a coluna com o [propriedade ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) propriedade.  
  
-   Para colunas de chave, especifique o nome da coluna relacionada na tabela relacionada com a [propriedade RelatedColumn (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md) propriedade.  
  
-   Para colunas de índice, especificar se a ordem de classificação é crescente ou decrescente com o [propriedade SortOrder (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md) propriedade.  
  
-   Acessar propriedades específicas do provedor com o [coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
> [!NOTE]
>  Nem todas as propriedades de **coluna** objetos podem ser suportados por seu provedor de dados. Um erro ocorrerá se você tiver definido um valor para uma propriedade que o provedor não dá suporte. Para o novo **coluna** objetos, ocorrerá um erro quando o objeto é acrescentado à coleção. Para objetos existentes, o erro ocorrerá quando a configuração da propriedade.  
>   
>  Ao criar **coluna** objetos, a existência de um valor padrão adequado para uma propriedade opcional não garante que o provedor oferece suporte à propriedade. Para obter mais informações sobre as propriedades que o provedor oferece suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Column](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Columns and Tables Append métodos, exemplo da propriedade Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Close da Conexão, exemplo da propriedade Table Type (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo das propriedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo de código ADOX: NumericScale e exemplo de propriedades Precision (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Exemplo da propriedade SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
