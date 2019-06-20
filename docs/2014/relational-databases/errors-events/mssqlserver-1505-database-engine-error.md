---
title: MSSQLSERVER_1505 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1505 (Database Engine error)
ms.assetid: ef4df75d-0f36-4c8b-b36c-e427f65f91ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec0a5700df76134eab8a4fe2278820691dad509e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869684"
---
# <a name="mssqlserver1505"></a>MSSQLSERVER_1505
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1505|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DUP_KEY|  
|Texto da mensagem|A instrução CREATE UNIQUE INDEX foi encerrada porque foi encontrada uma chave duplicada para o nome de objeto '%.*ls' e para o nome de índice '%.\*ls'.  O valor da chave duplicada é %ls.|  
  
## <a name="explanation"></a>Explicação  
 Esse erro ocorre quando você tenta criar um índice exclusivo e mais de uma linha da tabela contém o valor duplicado especificado. Um índice exclusivo é criado quando você cria um índice e especifica a palavra-chave UNIQUE ou quando cria uma restrição UNIQUE. A tabela não pode conter linhas que tenham valores duplicados nas colunas definidas no índice ou na restrição.  
  
 Considere os dados da seguinte tabela **Employee**:  
  
|LastName|FirstName|JobTitle|HireDate|  
|--------------|---------------|--------------|--------------|  
|Walters|Rob|Designer de ferramentas sênior|2004-11-19|  
|Brown|Kevin|Assistente de marketing|NULL|  
|Brown|Jo|Engenheiro de design|NULL|  
|Walters|Rob|Designer de ferramentas|2001-08-09|  
  
 Não é possível criar um índice exclusivo com as combinações de coluna **LastName** ou **LastName** e **FirstName** devido aos valores duplicados nas linhas.  
  
 Menos óbvia é a possibilidade de ocorrer uma violação de exclusividade na coluna **HireDate**. Para fins de indexação, valores NULL são comparados como iguais. Portanto, você não poderá criar um índice exclusivo ou uma restrição exclusiva se os valores de chave forem NULL em mais de uma linha. Considerando os dados acima, não é possível criar um índice exclusivo com base nas combinações de coluna **HireDate** ou **LastName** e **HireDate**.  
  
 A mensagem de erro 1505 retorna a primeira linha que viola a restrição de exclusividade. Pode haver outras linhas duplicadas na tabela. Para encontrar todas as linhas duplicadas, consulte a tabela especificada e use as cláusulas GROUP BY e HAVING para reportar essas linhas. Por exemplo, a consulta a seguir retorna as linhas da tabela **Employee** que têm nomes e sobrenomes duplicados.  
  
 SELECT LastName, FirstName, count(*) FROM dbo.Employee GROUP BY LastName, FirstName HAVING count(\*) > 1;  
  
## <a name="user-action"></a>Ação do usuário  
 Considere as soluções descritas a seguir.  
  
-   Adicione ou remova colunas na definição do índice ou da restrição para criar uma composição exclusiva. No exemplo anterior, adicionar uma coluna **MiddleName** à definição do índice ou da restrição pode resolver o problema de duplicação.  
  
-   Selecione colunas definidas como NOT NULL quando escolher colunas para um índice exclusivo ou para uma restrição exclusiva. Isso elimina a possibilidade de ocorrer uma violação de exclusividade gerada quando mais de uma linha contiver NULL nos valores de chave.  
  
-   Se os valores duplicados forem o resultado de erros de entrada de dados, corrija os dados manualmente e, em seguida, crie o índice ou a restrição. Para obter informações sobre como remover linhas duplicadas de uma tabela, veja o artigo 139444 da base de dados de conhecimento: [Como remover linhas duplicadas de uma tabela no SQL Server](https://support.microsoft.com/kb/139444).  
  
## <a name="see-also"></a>Consulte também  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [Criar índices exclusivos](../indexes/indexes.md)   
 [Criar restrições exclusivas](../tables/create-unique-constraints.md)  
  
  
