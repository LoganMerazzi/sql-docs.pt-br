---
title: Função Position (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
author: rothja
ms.author: jroth
ms.openlocfilehash: de9f30c3c63030aa956366c222b7cbda94e2becb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038985"
---
# <a name="context-functions---position-xquery"></a>Funções de Contexto – position (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um valor inteiro que indica a posição do item de contexto na sequência de itens que estão sendo processados atualmente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>Comentários  
 Na [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], **fn:position()** só pode ser usado no contexto de um predicado dependente de contexto. Especificamente, ele só pode ser usado entre parênteses ([ ]). A comparação contra essa função não reduz a cardinalidade durante a inferência de tipo estática.  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery contra instâncias XML armazenadas em várias **xml** colunas de tipo a [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>A. Usando a função position() XQuery para recuperar os primeiros dois recursos de produto  
 A consulta a seguir recupera os primeiros dois recursos, os primeiros dois elementos filho da <`Features`> elemento, na descrição de catálogo de modelo de produto. Se houver mais recursos, ele adiciona um <`there-is-more/`> elemento para o resultado.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O **namespace** palavra-chave na [prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define um prefixo de namespace que é usado no corpo da consulta.  
  
-   O corpo da consulta constrói XML que tem um \<produto > elemento com **ProductModelID** e **ProductModelName** atributos e tem recursos de produto retornados como elementos filho.  
  
-   O **Position ()** função é usada no predicado para determinar a posição do \<recursos > elemento filho no contexto. Se ele for o primeiro ou segundo recurso, será retornado.  
  
-   A instrução IF adiciona um \<lá-is-more / > elemento a ser o resultado se houver mais de dois recursos no catálogo de produtos.  
  
-   Como nem todos os modelos de produtos têm as descrições de catálogo armazenadas na tabela, a cláusula WHERE é usada para descartar linhas em que CatalogDescriptions é NULL.  
  
 Este é um resultado parcial:  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções XQuery em Tipos de Dados XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
