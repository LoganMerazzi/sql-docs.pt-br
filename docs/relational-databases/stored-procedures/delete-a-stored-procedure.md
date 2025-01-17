---
title: Excluir um procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- removing stored procedures
- stored procedures [SQL Server], deleting
- deleting stored procedures
ms.assetid: 232dbf4d-392a-406f-af3a-579518cd8e46
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5e1b61b44ffcdee0f7449984311f732368578d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934064"
---
# <a name="delete-a-stored-procedure"></a>Excluir um procedimento armazenado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
    
##  <a name="Top"></a> Este tópico descreve como excluir um procedimento armazenado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de começar:**  [Limitações e Restrições](#Restrictions), [Segurança](#Security)  
  
-   **Para excluir um procedimento usando:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Excluir um procedimento pode causar a falha em objetos e scripts dependentes quando os objetos e scripts não são atualizados para refletir a remoção do procedimento. Entretanto, se um novo procedimento com o mesmo nome e o mesmo parâmetro for criado para substituir aquele que foi excluído, os outros objetos que o referenciam ainda serão processados com êxito. Para obter mais informações, veja [Exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer permissão ALTER no esquema ao qual o procedimento pertence ou permissão CONTROL no procedimento.  
  
##  <a name="Procedures"></a> Como excluir um procedimento armazenado  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para excluir um procedimento no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados ao qual pertence o procedimento e expanda **Programação**.  
  
3.  Expanda **Procedimentos Armazenados**, clique com o botão direito do mouse no procedimento a excluir e, depois, clique em **Excluir**.  
  
4.  Para exibir objetos que dependem do procedimento, clique em **Mostrar Dependências**.  
  
5.  Confirme se o procedimento correto está selecionado e, depois, clique em **OK**.  
  
6.  Remova as referências ao procedimento de quaisquer objetos e scripts dependentes.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

###  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para excluir um procedimento no Editor de Consultas**  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de dados**, expanda o banco de dados ao qual o procedimento pertence, ou, da barra de ferramentas, selecione o banco de dados da lista de bancos de dados disponíveis.  
  
3.  No menu Arquivo, clique em **Nova Consulta**.  
  
4.  Obtenha o nome do procedimento armazenado a ser removido no banco de dados atual. No Pesquisador de Objetos, expanda **Programação** e, depois, expanda **Procedimentos Armazenados**. Outra alternativa é executar a instrução a seguir no editor de consultas.  
  
    ```sql  
    SELECT name AS procedure_name   
        ,SCHEMA_NAME(schema_id) AS schema_name  
        ,type_desc  
        ,create_date  
        ,modify_date  
    FROM sys.procedures;  
    ```  
  
5.  Copie e cole o exemplo a seguir no editor de consultas e insira um nome de procedimento armazenado a ser excluído do banco de dados atual.  
  
    ```sql  
    DROP PROCEDURE <stored procedure name>;  
    GO  
    ```  
  
6.  Remova as referências ao procedimento de quaisquer objetos e scripts dependentes.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Modificar um procedimento armazenado](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Renomear um procedimento armazenado](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [Exibir a definição de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  
