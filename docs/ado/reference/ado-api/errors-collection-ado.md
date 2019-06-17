---
title: Coleção Errors (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 109b7ff83e6b3f722560dae0a034c4bf37da137f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719273"
---
# <a name="errors-collection-ado"></a>Coleção Errors (ADO)
Contém todos os [erro](../../../ado/reference/ado-api/error-object.md) objetos criados em resposta a uma única falha de provedor.  
  
## <a name="remarks"></a>Comentários  
 Qualquer operação que envolva objetos ADO pode gerar um ou mais erros do provedor. Conforme cada erro ocorrer, um ou mais **erro** objetos podem ser colocados na **erros** coleção dos [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Quando outra operação ADO gera um erro, o **erros** coleção estiver desmarcada e o novo conjunto de **erro** objetos podem ser colocados no **erros** coleção.  
  
 Cada **erro** objeto representa um erro de provedor específico, não um erro do ADO. Erros ADO são expostos para o mecanismo de tratamento de exceções de tempo de execução. Por exemplo, no Microsoft Visual Basic, a ocorrência de um erro específico de ADO irá disparar uma [onError](../../../ado/reference/rds-api/onerror-event-rds.md) evento e aparece na **Err** objeto.  
  
 Operações de ADO que não geram um erro não têm nenhum efeito o **erros** coleção. Use o [desmarque](../../../ado/reference/ado-api/clear-method-ado.md) método limpar manualmente as **erros** coleção.  
  
 O conjunto de **erro** objetos na **erros** coleção descreve todos os erros que ocorreram em resposta a uma única instrução. Enumeração de erros específicos na **erros** coleção permite que suas rotinas de tratamento de erros determinar a causa e origem de um erro com mais precisão e tomar as medidas apropriadas para recuperar.  
  
 Algumas propriedades e métodos retornam os avisos que aparecem como **erro** objetos na **erros** coleção, mas não interrompem a execução de um programa. Antes de chamar o [ressincronizar](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos em um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método em um **Conexão** de objeto, ou definir a [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade em um **Recordset** de objeto, chame o **limpar**método de **erros** coleção. Dessa forma, você pode ler o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade da **erros** avisos retornados de coleção para testar.  
  
> [!NOTE]
>  Consulte a **erro** tópico de objeto para obter uma explicação mais detalhada da maneira como uma única operação de ADO pode gerar vários erros.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades de coleção de erros](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)   
 [Apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
