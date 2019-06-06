---
title: Nome de propriedade (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::PutName
- _Table::GetName
- _Key::Name
- _Key::get_Name
- _Column::GetName
- _Index::Name
- _Index::put_Name
- _Column::PutName
- _Key::put_Name
- _Table::put_Name
- _User25::PutName
- _Index::get_Name
- _Column::get_Name
- _Group25::Name
- _Group25::get_Name
- _Column::Name
- _User25::get_Name
- _Table::Name
- _Group25::GetName
- _Index::PutName
- _Column::put_Name
- _Key::GetName
- _Table::get_Name
- _User25::Name
- _User25::put_Name
- _Index::GetName
- _User25::GetName
helpviewer_keywords:
- Name property [ADOX]
ms.assetid: 81b92baf-b6b9-4f4e-9f33-4503795518cd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7f7b61dd2c1dc5899852234d23148969dad9c3dc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706380"
---
# <a name="name-property-adox"></a>Propriedade Name (ADOX)
Indica o nome do objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor.  
  
## <a name="remarks"></a>Comentários  
 Nomes não precisam ser exclusivos dentro de uma coleção.  
  
 O **nome** propriedade é leitura/gravação na [coluna](../../../ado/reference/adox-api/column-object-adox.md), [grupo](../../../ado/reference/adox-api/group-object-adox.md), [chave](../../../ado/reference/adox-api/key-object-adox.md), [índice](../../../ado/reference/adox-api/index-object-adox.md), [ Tabela](../../../ado/reference/adox-api/table-object-adox.md), e [usuário](../../../ado/reference/adox-api/user-object-adox.md) objetos. O **nome** propriedade é somente leitura no [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md), [procedimento](../../../ado/reference/adox-api/procedure-object-adox.md), e [exibição](../../../ado/reference/adox-api/view-object-adox.md) objetos.  
  
 Para objetos de leitura/gravação (**coluna**, **grupo**, **chave**, **índice**, **tabela** e  **Usuário** objetos), o valor padrão é uma cadeia de caracteres vazia ("").  
  
> [!NOTE]
>  Para chaves, essa propriedade é somente leitura no **chave** já está anexados a uma coleção de objetos. Para tabelas, essa propriedade é somente leitura para **tabela** já está anexados a uma coleção de objetos.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Objeto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)|  
|[Objeto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)|[Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|[Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Columns and Tables Append métodos, exemplo da propriedade Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo das propriedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
