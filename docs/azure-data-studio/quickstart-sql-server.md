---
title: 'Início Rápido: Conectar e consultar o SQL Server'
titleSuffix: Azure Data Studio
description: Neste início rápido mostra como usar o Studio de dados do Azure para se conectar ao SQL Server e executar uma consulta
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.openlocfilehash: 4117d8c16e96252f792e14d282d285527008874f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959390"
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>Início Rápido: Conectar e consultar usando SQL Server [!INCLUDE[name-sos](../includes/name-sos-short.md)]
Neste início rápido mostra como usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para se conectar ao SQL Server e, em seguida, usar instruções Transact-SQL (T-SQL) para criar o *TutorialDB* usados em [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriais.

## <a name="prerequisites"></a>Prerequisites

Para concluir este início rápido, você precisa [!INCLUDE[name-sos](../includes/name-sos-short.md)]e o acesso a um SQL Server.

- [Instale [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Se você não tiver acesso a um SQL Server, selecione sua plataforma nos links a seguir (certifique-se de lembrar seu logon do SQL e uma senha!):
- [Windows – Baixar o SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)
- [macOS – Baixar o SQL Server 2017 no Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)
- [Linux - Download SQL Server 2017 Developer Edition](https://docs.microsoft.com/sql/linux/sql-server-linux-overview#install) -você só precisará seguir as etapas até *criar e consultar dados*.


## <a name="connect-to-a-sql-server"></a>Conectar a um SQL Server

   
1. Inicie **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** .
1. Na primeira vez que você executar [!INCLUDE[name-sos](../includes/name-sos-short.md)] as **boas-vindas** deve abrir a página. Se você não vir as **bem-vindo** página, selecione **ajudar** > **boas-vindas**. Selecione **nova Conexão** para abrir o **Conexão** painel:
   
   ![Novo ícone de Conexão](media/quickstart-sql-server/new-connection-icon.png)

1. Este artigo usa *logon do SQL*, mas *autenticação do Windows* tem suporte. Preencha os campos da seguinte maneira:
 
    - **Nome do servidor:** localhost
    - **Tipo de autenticação:** Logon do SQL  
    - **Nome de usuário:** Nome de usuário para o SQL Server  
    - **Senha:** Senha para o SQL Server  
    - **Nome do banco de dados:** deixe esse campo em branco 
    - **Grupo de servidores:** \<Default\>  

   ![Nova tela de Conexão](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>Criar um banco de dados

As seguintes etapas criam um banco de dados denominado **TutorialDB**:

1. Clique com botão direito no seu servidor **localhost**e selecione **nova consulta.**
1. Cole o trecho a seguir na janela de consulta: 

   ```sql
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
      CREATE DATABASE [TutorialDB];
   GO
   IF SERVERPROPERTY('ProductVersion') > '12'
       ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON;
   GO
   ```
1. Para executar a consulta, clique em **executar** .

Depois que a consulta for concluída, o novo **TutorialDB** aparece na lista de bancos de dados. Se você não estiver visível, clique com botão direito do **bancos de dados** nó e selecione **atualizar**.


## <a name="create-a-table"></a>Criar uma tabela

O editor de consultas ainda está conectado para o *mestre* banco de dados, mas podemos deseja criar uma tabela na *TutorialDB* banco de dados. 

1. Alterar o contexto de conexão para **TutorialDB**:

   ![Contexto de alteração](media/quickstart-sql-server/change-context.png)



1. Cole o trecho a seguir na janela de consulta e clique em **executar**:

   > [!NOTE]
   > Você pode anexá-lo para ou substituir a consulta anterior no editor. Observe que clicar em **executar** executa somente a consulta selecionada. Se nada estiver selecionado, clicando em **executar** executa todas as consultas no editor.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
      DROP TABLE dbo.Customers;
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
       CustomerId  int NOT NULL PRIMARY KEY, -- primary key column
       Name        nvarchar(50) NOT NULL,
       Location    nvarchar(50) NOT NULL,
       Email       nvarchar(50) NOT NULL
   );
   GO
   ```

Depois que a consulta for concluída, o novo **clientes** tabela aparece na lista de tabelas. Talvez seja necessário com o botão direito do **TutorialDB > tabelas** nó e selecione **atualizar**.

## <a name="insert-rows"></a>Inserir linhas

- Cole o trecho a seguir na janela de consulta e clique em **executar**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId], [Name], [Location], [Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```



## <a name="view-the-data-returned-by-a-query"></a>Exibir os dados retornados por uma consulta
1. Cole o trecho a seguir na janela de consulta e clique em **executar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Os resultados da consulta são exibidos:

   ![Selecione resultados](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>Próximas etapas
Agora que você se conectou com êxito ao SQL Server e executar uma consulta, experimente o [tutorial do editor de código](tutorial-sql-editor.md).


