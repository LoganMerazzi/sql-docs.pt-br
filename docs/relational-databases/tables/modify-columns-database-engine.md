---
title: Modificar colunas (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- column data types [SQL Server]
- data types [SQL Server], columns
ms.assetid: b67b95c5-61ef-4bd8-9a3e-1640eb7583ac
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93cbdf74f8917492a2007d48ad27863440869092
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62693278"
---
# <a name="modify-columns-database-engine"></a>Modificar colunas (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode modificar o tipo de dados de uma coluna no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!WARNING]  
>  Modificar o tipo de dados de uma coluna que já contenha dados pode resultar na perda permanente de dados quando os dados existentes forem convertidos para o novo tipo. Além disso, códigos e aplicativos que dependem da coluna modificada podem falhar. Isso inclui consultas, exibições, procedimentos armazenados, funções definidas pelo usuário e aplicativos clientes. Observe que essas falhas ocorrerão em cascata. Por exemplo, um procedimento armazenado que chama uma função definida pelo usuário que dependa da coluna modificada pode falhar. Considere cuidadosamente todas as alterações que você pretende realizar em uma coluna antes fazê-las.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar o tipo de dados de uma coluna usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>Para modificar o tipo de dados de uma coluna  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela com as colunas cuja escala você deseja alterar e clique em **Design**.  
  
2.  Selecione a coluna cujo tipo de dados você pretende modificar.  
  
3.  Na guia **Propriedades da Coluna** , clique na célula de grade da propriedade **Tipo de Dados** e selecione o novo tipo de dados na lista suspensa.  
  
4.  No menu **Arquivo** , clique em **Salvar**_table name_.  
  
> [!NOTE]  
>  Quando o tipo de dados de uma coluna é modificado, o Designer de Tabela aplica o comprimento padrão do tipo de dados que foi selecionado, até mesmo quando outro já tiver sido especificado. Defina sempre o comprimento do tipo de dados do valor desejado após especificar o tipo de dados.  
  
> [!WARNING]  
>  Se você tentar modificar o tipo de dados de uma coluna relacionada a outras tabelas, o Designer de Tabela solicitará que você confirme se a alteração deve ser feita nas colunas das outras tabelas também.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>Para modificar o tipo de dados de uma coluna  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    CREATE TABLE dbo.doc_exy (column_a INT ) ;  
    GO  
    INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
    GO  
    ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
    GO  
  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
