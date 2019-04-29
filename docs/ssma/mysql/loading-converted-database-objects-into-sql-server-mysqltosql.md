---
title: Carregando convertidos do banco de dados objetos no SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b2e58eb534088482493e6f36c3841f36644183af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187233"
---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>Carregar objetos de banco de dados convertidos no SQL Server (MySQLToSQL)
Depois de converter bancos de dados MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, você pode carregar os objetos de banco de dados resultante em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode ter o SSMA criar os objetos, ou você pode gerar script dos objetos e executar os scripts por conta própria. Além disso, o SSMA permite atualizar os metadados de destino com o conteúdo real da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados do SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Escolhendo entre sincronização e Scripts  
Se você deseja carregar os objetos de banco de dados convertido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, sem modificações, você pode ter o SSMA criar ou recriar os objetos de banco de dados diretamente. Que método é rápido e fácil, mas não permite a personalização do código Transact-SQL que define o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do SQL Azure.  
  
Se você quiser modificar o Transact-SQL que é usado para criar objetos, ou se você quiser mais controle sobre a criação de objetos, use o SSMA para criar scripts. Você pode, em seguida, modificar esses scripts, criar cada objeto individualmente e até mesmo usar o SQL Server Agent para agendar a criação desses objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Usando o SSMA para sincronizar objetos com o SQL Server  
Para usar o SSMA para criar objetos de banco de dados do SQL Server ou SQL Azure, você seleciona os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure e, em seguida, sincronizar os objetos com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, conforme mostrado no procedimento a seguir. Por padrão, se os objetos já existirem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure e se os metadados do SSMA tem algumas alterações locais ou atualizações para a definição desses objetos muito, o SSMA irá alterar as definições de objeto em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode alterar o comportamento padrão, editando **configurações do projeto**.  
  
> [!NOTE]  
> Você pode selecionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos de banco de dados do SQL Azure que não foram convertidos de bancos de dados MySQL. No entanto, esses objetos não serão recriados ou alterados por SSMA.  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>Para sincronizar objetos com o SQL Server ou SQL Azure  
  
1.  Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure, expanda a parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o nó do SQL Azure e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem processados:  
  
    -   Para sincronizar um banco de dados completo, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para sincronizar ou omitir objetos individuais ou categorias de objetos, marque ou desmarque a caixa de seleção ao lado do objeto ou pasta.  
  
3.  Depois de selecionar os objetos a serem processados no SQL Server ou o Gerenciador de metadados do SQL Azure, clique com botão direito **bancos de dados**e, em seguida, clique em **sincronizar com o banco de dados**.  
  
    Você também pode sincronizar objetos individuais ou as categorias de objetos clicando com botão direito do objeto ou a pasta pai e, em seguida, clicando em **sincronizar com o banco de dados**.  
  
    Depois disso, o SSMA exibirá os **sincronizar com o banco de dados** caixa de diálogo, onde você pode ver dois grupos de itens. No lado esquerdo, o SSMA mostra representados em uma árvore de objetos de banco de dados selecionado. No lado direito, você pode ver uma árvore que representa os mesmos objetos nos metadados do SSMA. Você pode expandir a árvore clicando-se à direita ou esquerda botão ' +'. A direção da sincronização é mostrada na coluna ação colocado entre as duas árvores.  
  
    Um sinal de ação pode estar em três estados:  
  
    -   Uma seta para a esquerda significa que o conteúdo de metadados será salvo no banco de dados (o padrão).  
  
    -   Uma seta para a direita significa que o conteúdo do banco de dados substituirão os metadados do SSMA.  
  
    -   Um sinal cruzado significa que nenhuma ação será tomada.  
  
    -   Clique no sinal de ação para alterar o estado. Sincronização real será executada quando você clica **Okey** botão da **sincronizar com o banco de dados** caixa de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de script  
Para economizar [!INCLUDE[tsql](../../includes/tsql-md.md)] as definições dos objetos de banco de dados convertido, ou alterar as definições de objeto e executar scripts por conta própria, você pode salvar o banco de dados convertido definições de objeto para [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts.  
  
**Para salvar objetos como scripts**  
  
1.  Depois de selecionar os objetos para salvar um script, clique com botão direito **bancos de dados**e, em seguida, clique em **Salvar como Script**.  
  
    Você pode também gerar um script objetos individuais ou as categorias de objetos clicando com botão direito do objeto ou a pasta pai e, em seguida, clicando em **Salvar como Script**.  
  
2.  No **Salvar como** diálogo caixa, localize a pasta onde você deseja salvar o script, digite um nome de arquivo na **nome do arquivo** caixa e, em seguida, [!INCLUDE[clickOK](../../includes/clickok-md.md)] SSMA acrescentará a extensão de nome de arquivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificando Scripts  
Depois de salvar as definições de objeto do SQL Azure ou do SQL Server como um script, você pode usar o SQL Server Management Studio para modificar o script.  
  
**Para modificar um script**  
  
1.  No Management Studio **arquivo** , aponte para **abra**e, em seguida, clique em **arquivo**.  
  
2.  Na caixa de diálogo Abrir, localize e selecione o arquivo de script e, em seguida, clique em **Okey**.  
  
3.  Edite o arquivo de script usando o editor de consultas. Para obter mais informações sobre o editor de consultas, consulte "Editor de comandos e recursos de conveniência" nos Manuais Online do SQL Server.  
  
4.  Para salvar o script, no menu Arquivo, selecione **salvar**.  
  
### <a name="running-scripts"></a>Execução de Scripts  
Você pode executar um script ou instruções individuais, no SQL Server Management Studio.  
  
**Para executar um script**  
  
1.  Sobre o SQL Server Management Studio **arquivo** , aponte para **abra** e, em seguida, clique em **arquivo**.  
  
2.  Na caixa de diálogo Abrir, localize e selecione o arquivo de script e, em seguida, clique em **Okey**.  
  
3.  Para executar o script completo, pressione a **F5** chave.  
  
4.  Para executar um conjunto de instruções, selecione as instruções na janela do editor de consulta e, em seguida, pressione a **F5** chave.  
  
5.  Para obter mais informações sobre como usar o editor de consultas para executar scripts, consulte "Consulta do SQL Server Management Studio Transact-SQL" nos Manuais Online do SQL Server.  
  
6.  Você também pode executar scripts da linha de comando usando o **sqlcmd** utility e no SQL Server Agent. Para obter mais informações sobre **sqlcmd**, consulte "utilitário sqlcmd" nos Manuais Online do SQL Server. Para obter mais informações sobre o SQL Server Agent, consulte "Automatizando tarefas administrativas (SQL Server Agent)" nos Manuais Online do SQL Server.  
  
## <a name="securing-objects-in-sql-server"></a>Protegendo os objetos no SQL Server  
Depois que você carregou os objetos de banco de dados convertidos no SQL Server, é possível conceder e negar permissões nesses objetos. É uma boa ideia fazer isso antes de migrar dados para o SQL Server. Para obter informações sobre como ajudar a proteger objetos no SQL Server, consulte "Considerações para bancos de dados e banco de dados de aplicativos de segurança" nos Manuais Online do SQL Server.  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no processo de migração [migrando dados do MySQL para o SQL Server – BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
