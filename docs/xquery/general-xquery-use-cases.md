---
title: Casos de uso gerais de XQuery | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e844425f0c512cfe7c15354bf1aeb100d6104e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004528"
---
# <a name="general-xquery-use-cases"></a>Casos gerais de uso de XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tópico fornece exemplos gerais de uso de XQuery.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>A. Consultar descrições de catálogo para localizar produtos e pesos  
 A consulta a seguir retorna as IDs e os pesos de modelo do produto , se existentes, da descrição do catálogo de produtos. A consulta constrói XML que tenha a seguinte forma:  
  
```  
<Product ProductModelID="...">  
  <Weight>...</Weight>  
</Product>  
```  
  
 Esta é a consulta:  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O **namespace** palavra-chave no prólogo do XQuery define um prefixo de namespace que é usado no corpo da consulta.  
  
-   O corpo da consulta constrói o XML exigido.  
  
-   Na cláusula WHERE, o **exist ()** método é usado para localizar somente as linhas que contêm descrições de catálogo de produtos. Ou seja, o XML que contém o <`ProductDescription`> elemento.  
  
 Esse é o resultado:  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 A consulta a seguir recupera as mesmas informações, mas somente para aqueles modelos de produto cuja descrição de catálogo inclui o peso, o <`Weight`> elemento, nas especificações, o <`Specifications`> elemento. Este exemplo usa WITH XMLNAMESPACES para declarar o prefixo pd e sua associação de namespace. Dessa forma, a associação não é descrita em ambos os **Query ()** método e, na **exist ()** método.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 Na consulta anterior, o **exist ()** método da **xml** tipo de dados na cláusula WHERE verifica para ver se há um <`Weight`> elemento no <`Specifications`> elemento.  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>B. Localizar IDs de modelos de produtos cujas descrições de catálogo incluem ângulo frontal e pequenas fotos  
 A descrição do catálogo de produto XML inclui as imagens de produto, o <`Picture`> elemento. Cada foto tem várias propriedades. Eles incluem o ângulo da foto, o <`Angle`> elemento e o tamanho, o <`Size`> elemento.  
  
 Para modelos de produtos cujas descrições de catálogo incluem ângulo frontal e pequenas fotos, a consulta constrói um XML com o seguinte formato:  
  
```  
< Product ProductModelID="...">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   Na cláusula WHERE, o **exist ()** método é usado para recuperar apenas as linhas que tenham descrições de catálogo de produto com o <`Picture`> elemento.  
  
-   A cláusula WHERE usa o **Value ()** método duas vezes para comparar os valores da <`Size`> e <`Angle`> elementos.  
  
 Este é um resultado parcial:  
  
```  
<p1:Product   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. Criar uma lista simples de produto pares de nome e o recurso de modelo, cada par incluído no \<recursos > elemento  
 Na descrição de catálogo de modelo de produto, o XML inclui várias características de produto. Todos esses recursos estão incluídos no <`Features`> elemento. A consulta usa [construção XML (XQuery)](../xquery/xml-construction-xquery.md) para construir o XML necessário. A expressão nas chaves é substituída pelo resultado.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   $pd / PD/P1:Features/ / * retorna apenas o elemento filhos do nó <`Features`>, mas $pd PD/P1:Features/Node () retorna todos os nós. Isso inclui os nós de elemento, nós de texto, as instruções de processamento e os comentários.  
  
-   Os dois loops FOR geram um produto Cartesiano do qual o nome de produto e a característica individual são retornados.  
  
-   O **ProductName** é um atributo. A construção XML nesta consulta retorna-o como um elemento.  
  
 Este é um resultado parcial:  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. Na descrição de catálogo de um modelo de produto, ID de nome, modelo de modelo de lista do produto e recursos agrupados dentro de um \<produto > elemento  
 Usando as informações armazenadas na descrição de catálogo do modelo de produto, a consulta a seguir lista o nome de modelo do produto, ID do modelo, e recursos agrupados dentro de um \<produto > elemento.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Este é um resultado parcial:  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. Recuperar as descrições de recursos de modelos do produto  
 A consulta a seguir constrói XML que inclui um <`Product`> elemento que tem **Productmodelid**, **ProductModelName** atributos e os primeiros dois recursos de produto. Especificamente, os primeiros dois recursos de produto são os primeiros dois elementos filho da <`Features`> elemento. Se houver mais recursos, ele retornará um <`There-is-more/`> elemento.  
  
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
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O FOR... Return recupera os primeiros dois recursos de produto. O **Position ()** função é usada para localizar a posição dos elementos na sequência.  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. Localizar nomes de elementos na descrição do catálogo de produtos que terminam com "ons"  
 A consulta a seguir pesquisa as descrições de catálogo e retorna todos os elementos de <`ProductDescription`> elemento cujo nome termina com "ões".  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 Este é um resultado parcial:  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. Localizar descrições resumidas que contêm a palavra "Aerodynamic"  
 A consulta a seguir recupera modelos de produto cujas descrições de catálogo contêm a palavra "Aerodinâmico" na descrição sumária:  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 Observe que a consulta SELECT especifica **Query ()** e **Value ()** métodos os **xml** tipo de dados. Portanto, em vez de repetir a declaração namespaces duas vezes em dois prólogos de consulta diferentes, o prefixo pd será usado na consulta e será definido apenas uma vez usando WITH XMLNAMESPACES.  
  
 Observe o seguinte na consulta anterior:  
  
-   A cláusula WHERE é usada para recuperar apenas as linhas onde a descrição de catálogo contém a palavra "Aerodinâmico" no <`Summary`> elemento.  
  
-   O **Contains ()** função é usada para ver se a palavra está incluída no texto.  
  
-   O **Value ()** método o **xml** tipo de dados compara o valor retornado por **Contains ()** como 1.  
  
 Esse é o resultado:  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. Localizar modelos de produtos cujas descrições de catálogo não incluem fotos do modelo do produto  
 A seguinte consulta recupera ProductModelIDs para modelos de produto cujas descrições de catálogo não não incluem um <`Picture`> elemento.  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   Se o **exist ()** método na cláusula WHERE retorna False (0), a ID do modelo de produto é retornada. Caso contrário, não é retornado.  
  
-   Como todas as descrições de produto incluem um <`Picture`> elemento, o conjunto de resultados é vazio neste caso.  
  
## <a name="see-also"></a>Consulte também  
 [XQueries que envolvem hierarquias](../xquery/xqueries-involving-hierarchy.md)   
 [XQueries que envolvem ordem](../xquery/xqueries-involving-order.md)   
 [Xqueries que manipulam dados relacionais](../xquery/xqueries-handling-relational-data.md)   
 [Pesquisa de cadeia de caracteres em XQuery](../xquery/string-search-in-xquery.md)   
 [Manipulando Namespaces em XQuery](../xquery/handling-namespaces-in-xquery.md)   
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
