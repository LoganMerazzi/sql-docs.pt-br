---
title: OPENROWSET (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8be3fe8cbf30121ec2895f59306c925a422d5c39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938121"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;consulta de fonte de dados&gt; -OPENROWSET
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Substitui uma consulta de dados de origem por uma consulta a um provedor externo. As instruções INSERT, SELECT FROM PREDICTION JOIN e SELECT FROM NATURAL PREDICTION JOIN oferecem suporte a **OPENROWSET**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>Argumentos  
 *provider_name*  
 Nome de um provedor de OLE DB.  
  
 *provider_string*  
 Cadeia de conexão OLE DB para o provedor especificado.  
  
 *query_syntax*  
 Sintaxe de consulta que retorna um conjunto de linhas.  
  
## <a name="remarks"></a>Comentários  
 O provedor de mineração de dados estabelecerá uma conexão para o objeto de fonte de dados usando *provider_name* e *provider_string,* e executará a consulta especificada no *query_syntax* para recuperar o conjunto de linhas de dados de origem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir pode ser usado em uma instrução PREDICTION JOIN para recuperar dados do banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], usando uma instrução [!INCLUDE[tsql](../includes/tsql-md.md)] SELECT.  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>Consulte também  
 [&#60;consulta de fonte de dados&#62;](../dmx/source-data-query.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
