---
title: Usar os métodos value() e nodes() com OPENXML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- OpenXML method [XML in SQL Server]
- value method [XML in SQL Server]
- nodes method [XML in SQL Server]
ms.assetid: c73dbe55-d685-42eb-b0ee-9f3c5b9d97f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a511e977975ad0e23c9cf553de000b32bad24e69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039142"
---
# <a name="use-the-value-and-nodes-methods-with-openxml"></a>Usar os métodos value() e nodes() com OPENXML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  É possível usar vários métodos **value()** em tipo de dados **xml** em uma cláusula **SELECT** para gerar um conjunto de linhas de valores extraídos. O método **nodes()** produz uma referência interna para cada nó selecionado que pode ser usado para consulta adicional. A combinação dos métodos **nodes()** e **value()** pode ser mais eficiente para gerar o conjunto de linhas quando ele tem várias colunas e, talvez, quando as expressões de caminho usadas em sua geração são complexas.  
  
 O método **nodes()** produz instâncias de um tipo de dados **xml** especial, cada uma das quais tem seu contexto definido como um nó selecionado diferente. Esse tipo de instância XML dá suporte aos métodos **query()** , **value()** , **nodes()** e **exist()** e pode ser usado em agregações **count(\*)** . Todos os outros usos provocam um erro.  
  
## <a name="example-using-nodes"></a>Exemplo: Usando nodes()  
 Assuma que você deseja extrair os nomes e sobrenomes de autores e o nome não é "David". Além disso, você deseja extrair essas informações como um conjunto de linhas que contém duas colunas, FirstName e LastName. Usando os métodos **nodes()** e **value()** , isso pode ser feito da seguinte forma:  
  
```  
SELECT nref.value('(first-name/text())[1]', 'nvarchar(50)') FirstName,  
       nref.value('(last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T CROSS APPLY xCol.nodes('//author') AS R(nref)  
WHERE  nref.exist('first-name[. != "David"]') = 1  
```  
  
 Nesse exemplo, `nodes('//author')` produz um conjunto de linhas de referências a elementos `<author>` para cada instância XML. Os nomes e sobrenomes de autores são obtidos avaliando métodos **value()** em relação a essas referências.  
  
 O SQL Server 2000 fornece a capacidade de gerar um conjunto de linhas de uma instância XML usando **OpenXml()** . É possível especificar o esquema relacional do conjunto de linhas e como valores dentro da instância XML mapeiam para colunas no conjunto de linhas.  
  
## <a name="example-using-openxml-on-the-xml-data-type"></a>Exemplo: Usando OpenXml() no tipo de dados xml  
 A consulta do exemplo anterior pode ser reescrita usando **OpenXml()** conforme mostrado a seguir. Isso é feito criando um cursor que lê cada instância XML em uma variável XML e, em seguida, aplica OpenXML a ela:  
  
```  
DECLARE name_cursor CURSOR  
FOR  
   SELECT xCol   
   FROM   T  
OPEN name_cursor  
DECLARE @xmlVal XML  
DECLARE @idoc int  
FETCH NEXT FROM name_cursor INTO @xmlVal  
  
WHILE (@@FETCH_STATUS = 0)  
BEGIN  
   EXEC sp_xml_preparedocument @idoc OUTPUT, @xmlVal  
   SELECT   *  
   FROM   OPENXML (@idoc, '//author')  
          WITH (FirstName  varchar(50) 'first-name',  
                LastName   varchar(50) 'last-name') R  
   WHERE  R.FirstName != 'David'  
  
   EXEC sp_xml_removedocument @idoc  
   FETCH NEXT FROM name_cursor INTO @xmlVal  
END  
CLOSE name_cursor  
DEALLOCATE name_cursor   
```  
  
 **OpenXml()** cria uma representação na memória e usa tabelas de trabalho em vez do processador de consultas. Ele conta com o processador do XPath versão 1.0 do MSXML versão 3.0 em vez do mecanismo de XQuery. As tabelas de trabalho não são compartilhadas entre várias chamadas para **OpenXml()** , mesmo na mesma instância XML. Isto limita sua escalabilidade. **OpenXml()** permite acessar um formato de tabela de borda para os dados XML quando a cláusula WITH não está especificada. Além disso, ele permite usar o valor XML restante em uma coluna de "estouro" separada.  
  
 A combinação das funções **nodes()** e **value()** usa índices XML de maneira efetiva. Como resultado, essa combinação pode exibir mais escalabilidade que o **OpenXml**.  
  
## <a name="see-also"></a>Consulte Também  
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
