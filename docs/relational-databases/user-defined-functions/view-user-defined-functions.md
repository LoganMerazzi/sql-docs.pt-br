---
title: Exibir funções definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.udfproperties.general.f1
- sql13.swb.functionproperties.general.f1
helpviewer_keywords:
- displaying user-defined functions
- viewing user-defined functions
- user-defined functions [SQL Server], viewing
- status information [SQL Server], user-defined functions
ms.assetid: a45dfab5-6384-4311-b935-2e23a70c5c10
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8390690ebbdef66d0a5c754e7a0e5db2f31437de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123518"
---
# <a name="view-user-defined-functions"></a>Exibir funções definidas pelo usuário
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Você pode obter informações sobre a definição ou as propriedades de uma função definida pelo usuário no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Talvez seja necessário observar a definição da função para entender como seus dados são derivados das tabelas de origem, ou consultar os dados definidos pela função.  
  
> [!IMPORTANT]  
>  Se você alterar o nome de um objeto referenciado por uma função, deverá modificar essa função, de modo que seu texto reflita o novo nome. Portanto, antes de renomear um objeto, exiba primeiramente as dependências do objeto para determinar se alguma função é afetada pela mudança proposta.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para obter informações sobre uma função usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 O uso de **sys.sql_expression_dependencies** para localizar todas as dependências em uma função exige a permissão VIEW DEFINITION no banco de dados e a permissão SELECT em **sys.sql_expression_dependencies** no banco de dados. As definições de objeto de sistema, como as retornadas em OBJECT_DEFINITION, são publicamente visíveis.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-show-a-user-defined-functions-properties"></a>Para mostrar as propriedades de uma função definida pelo usuário  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição ao lado do banco de dados que contém a função na qual você deseja ver as propriedades e clique no sinal de adição para expandir a pasta **Programabilidade** .  
  
2.  Clique no sinal de adição para expandir a pasta **Funções** .  
  
3.  Clique no sinal de adição para expandir a pasta que contém a função na qual você deseja exibir as propriedades:  
  
    -   Table-valued Function  
  
    -   Função de valor escalar  
  
    -   Função de agregação  
  
4.  Clique com o botão direito do mouse na função da qual você deseja ver as propriedades e selecione **Propriedades**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     The following properties appear in the **Function Properties -** _function_name_ dialog box.  
  
     **Database**  
     The name of the database containing this function.  
  
     **Server**  
     The name of the current server instance.  
  
     **User**  
     The name of the user of this connection.  
  
     **Created date**  
     Displays the date the function was created.  
  
     **Execute As**  
     Execution context for the function.  
  
     **Name**  
     The name of the current function.  
  
     **Schema**  
     Displays the schema that owns the function.  
  
     **System object**  
     Indicates whether the function is a system object. Values are True and False.  
  
     **ANSI NULLs**  
     Indicates if the object was created with the ANSI NULLs option.  
  
     **Encrypted**  
     Indicates whether the function is encrypted. Values are True and False.  
  
     **Function Type**  
     The type of user defined function.  
  
     **Quoted identifier**  
     Indicates if the object was created with the quoted identifier option.  
  
     **Schema bound**  
     Indicates whether the function is schema-bound. Values are True and False. For information about schema-bound functions, see the SCHEMABINDING section of [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-get-the-definition-and-properties-of-a-function"></a>Para obter a definição e as propriedades de uma função  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole um dos exemplos a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the function name, definition, and relevant properties  
    SELECT sm.object_id,   
       OBJECT_NAME(sm.object_id) AS object_name,   
       o.type,   
       o.type_desc,   
       sm.definition,  
       sm.uses_ansi_nulls,  
       sm.uses_quoted_identifier,  
       sm.is_schema_bound,  
       sm.execute_as_principal_id  
    -- using the two system tables sys.sql_modules and sys.objects  
    FROM sys.sql_modules AS sm  
    JOIN sys.objects AS o ON sm.object_id = o.object_id  
    -- from the function 'dbo.ufnGetProductDealerPrice'  
    WHERE sm.object_id = OBJECT_ID('dbo.ufnGetProductDealerPrice')  
    ORDER BY o.type;  
    GO  
  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the definition of the function dbo.ufnGetProductDealerPrice  
    SELECT OBJECT_DEFINITION (OBJECT_ID('dbo.ufnGetProductDealerPrice')) AS ObjectDefinition;  
    GO  
    ```  
  
 Para obter mais informações, veja [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) e [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md).  
  
#### <a name="to-get-the-dependencies-of-a-function"></a>Para obter as dependências de uma função  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get all of the dependency information  
    SELECT OBJECT_NAME(sed.referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(sed.referencing_id, sed.referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        sed.referencing_class_desc, sed.referenced_class_desc,  
        sed.referenced_server_name, sed.referenced_database_name, sed.referenced_schema_name,  
        sed.referenced_entity_name,   
        COALESCE(COL_NAME(sed.referenced_id, sed.referenced_minor_id), '(n/a)') AS referenced_column_name,  
        sed.is_caller_dependent, sed.is_ambiguous  
    -- from the two system tables sys.sql_expression_dependencies and sys.object  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    -- on the function dbo.ufnGetProductDealerPrice  
    WHERE sed.referencing_id = OBJECT_ID('dbo.ufnGetProductDealerPrice');  
    GO  
    ```  
  
 Para obter mais informações, veja [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) e [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
  
