---
title: Propriedade NumericScale (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords:
- NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16fdefcb06d2b1b90dfc3da39aaf6b1c9659debc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965741"
---
# <a name="numericscale-property-adox"></a>Propriedade NumericScale (ADOX)
Indica a escala de um valor numérico na coluna.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define e retorna um **bytes** valor que é a escala de valores de dados na coluna quando o [tipo](../../../ado/reference/adox-api/type-property-column-adox.md) é de propriedade **adNumeric** ou **adDecimal**. **NumericScale** é ignorado para todos os outros tipos de dados.  
  
## <a name="remarks"></a>Comentários  
 O valor padrão é zero (0).  
  
 **NumericScale** é somente leitura para [coluna](../../../ado/reference/adox-api/column-object-adox.md) já está anexados a uma coleção de objetos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de código ADOX: NumericScale e exemplo de propriedades Precision (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Propriedade Type (Column) (ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
