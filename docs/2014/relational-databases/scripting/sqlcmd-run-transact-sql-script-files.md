---
title: Executar arquivos de script Transact-SQL usando sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0a55800ff1d707ce191d373a7348bf744ce5886
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063672"
---
# <a name="run-transact-sql-script-files-using-sqlcmd"></a>Executar arquivos de script Transact-SQL usando sqlcmd
  Você pode usar `sqlcmd` para executar um arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)]. Um arquivo de script do [!INCLUDE[tsql](../../includes/tsql-md.md)] é um arquivo de texto que contém uma combinação de instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)], comandos e variáveis de script do `sqlcmd`.  
  
 Para criar um arquivo simples de script do [!INCLUDE[tsql](../../includes/tsql-md.md)] usando o Bloco de Notas, siga estas etapas:  
  
1.  Clique em **Iniciar**, selecione **Todos os Programas**, vá até **Acessórios**e, depois, clique em **Bloco de Notas**.  
  
2.  Copie e cole o seguinte código do [!INCLUDE[tsql](../../includes/tsql-md.md)] no Bloco de Notas:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT p.FirstName + ' ' + p.LastName AS 'Employee Name',  
    a.AddressLine1, a.AddressLine2 , a.City, a.PostalCode   
    FROM Person.Person AS p   
       INNER JOIN HumanResources.Employee AS e   
            ON p.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.BusinessEntityAddress bea   
            ON bea.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.Address AS a   
            ON a.AddressID = bea.AddressID;  
    GO  
    ```  
  
3.  Salve o arquivo como **myScript.sql** na unidade C.  
  
### <a name="to-run-the-script-file"></a>Para executar o arquivo de script  
  
1.  Abra uma janela do prompt de comando.  
  
2.  Na janela do prompt de comando, digite: `sqlcmd -S myServer\instanceName -i C:\myScript.sql`  
  
3.  Pressione ENTER.  
  
 Uma lista de nomes e endereços de funcionários do [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] é escrita na janela do prompt de comando.  
  
### <a name="to-save-this-output-to-a-text-file"></a>Para salvar essa saída em um arquivo de texto  
  
1.  Abra uma janela do prompt de comando.  
  
2.  Na janela do prompt de comando, digite: `sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt`  
  
3.  Pressione ENTER.  
  
 Nenhuma saída é retornada na janela de prompt de comando. Em vez disso, a saída é enviada ao arquivo EmpAdds.txt. Você pode verificar essa saída abrindo o arquivo EmpAdds.txt.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o utilitário sqlcmd](sqlcmd-start-the-utility.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)  
  
  
