---
title: XQueries que envolvem hierarquias | Microsoft Docs
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
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
author: rothja
ms.author: jroth
ms.openlocfilehash: 8aa762af8e08c72f7f00369219771c371ce39aac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946102"
---
# <a name="xqueries-involving-hierarchy"></a>XQueries que envolvem hierarquias
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A maioria dos **xml** colunas de tipo a **AdventureWorks** banco de dados são documentos semiestruturados. Portanto, os documentos armazenados em cada linha podem parecer diferentes. Os exemplos de consulta neste tópico ilustram como extrair informações desses vários documentos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. Nos documentos de instruções de fabricação, recuperar os locais de centro de trabalho junto com a primeira etapa de fabricação nesses locais  
 Para o modelo de produto 7, a consulta constrói XML que inclui o <`ManuInstr`> elemento, com **ProductModelID** e **ProductModelName** atributos e um ou mais <`Location`> elementos filho.  
  
 Cada <`Location`> elemento tem seu próprio conjunto de atributos e um <`step`> elemento filho. Isso <`step`> elemento filho é a primeira etapa de fabricação no local de centro de trabalho.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   \<ManuInstr  ProdModelID = "{sql:column("Production.ProductModel.ProductModelID") }"   
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
            {   
              for $wc in //AWMI:root/AWMI:Location  
              return  
                <Location>  
                 {$wc/@* }  
                 <step1> { string( ($wc//AWMI:step)[1] ) } </step1>  
                </Location>  
            }  
          </ManuInstr>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O **namespace** palavra-chave na [prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define um prefixo de namespace. Esse prefixo é usado mais tarde no corpo da consulta.  
  
-   As chaves agem como tokens de troca de contexto,{) e (}, e são usadas para alternar a consulta da construção XML para avaliação de consulta.  
  
-   O **SQL: Column** é usado para incluir um valor relacional no XML que está sendo construído.  
  
-   Para construir o <`Location`> elemento, $wc/@* recupera todos os atributos de localização de centro trabalho.  
  
-   O **String ()** função retorna o valor de cadeia de caracteres da <`step`> elemento.  
  
 Este é um resultado parcial:  
  
```xml
<ManuInstr ProdModelID="7" ProductModelName="HL Touring Frame">  
   <Location LocationID="10" SetupHours="0.5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
     <step1>Insert aluminum sheet MS-2341 into the T-85A   
             framing tool.</step1>  
   </Location>  
   <Location LocationID="20" SetupHours="0.15"   
            MachineHours="2" LaborHours="1.75" LotSize="1">  
      <step1>Assemble all frame components following   
             blueprint 1299.</step1>  
   </Location>  
...  
</ManuInstr>   
```  
  
### <a name="b-find-all-telephone-numbers-in-the-additionalcontactinfo-column"></a>B. Localizar todos os números de telefone na coluna AdditionalContactInfo  
 A consulta a seguir recupera os números de telefone adicionais para um contato de cliente específico pesquisando a hierarquia inteira para o <`telephoneNumber`> elemento. Porque o <`telephoneNumber`> elemento pode aparecer em qualquer lugar na hierarquia, a consulta usa o operador descendente e auto-operador (/ /) na pesquisa.  
  
```sql
SELECT AdditionalContactInfo.query('  
 declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 Esse é o resultado:  
  
```xml
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 Para recuperar apenas os números de telefone de nível superior, especificamente o <`telephoneNumber`> elementos filho de <`AdditionalContactInfo`>, a expressão FOR na consulta muda para  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`.  
  
## <a name="see-also"></a>Confira também  
 [Fundamentos de XQuery](../xquery/xquery-basics.md)   
 [Construção XML &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
