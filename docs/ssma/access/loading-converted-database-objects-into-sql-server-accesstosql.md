---
title: Carregando convertidos do banco de dados objetos no SQL Server (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, loading converted objects into SQL Azure
- Access databases, loading converted objects into SQL Server
- data, securing
- loading objects into SQL Azure
- loading objects into SQL Server
- migrating objects into SQL Azure
- migrating objects into SQL Server
- moving objects into SQL Azure
- moving objects into SQL Server
- schemas, loading into SQL Azure
- schemas, loading into SQL Server
- scripting converted objects
- securing data
- SQL Azure, loading objects into
- SQL Server, loading objects into
- synchronizing metadata with SQL Azure
- synchronizing metadata with SQL Server
- uploading objects into SQL Azure
- uploading objects into SQL Server
ms.assetid: 4e854eee-b10c-4f0b-9d9e-d92416e6f2ba
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9ab56815fa36f23a15bc646c69094c3ca2f5fa3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299253"
---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>Carregando convertidos do banco de dados objetos no SQL Server (AccessToSQL)
Depois de converter objetos de banco de dados de acesso à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, você pode carregar os objetos de banco de dados resultante em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode ter o SSMA criar os objetos, ou você pode gerar script dos objetos e executar os scripts por conta própria. Além disso, o SSMA permite atualizar os metadados de destino com o conteúdo real da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados do SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Escolhendo entre sincronização e Scripts  
Se você deseja carregar os objetos de banco de dados convertido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, sem modificações, você pode ter o SSMA criar ou recriar os objetos de banco de dados diretamente. Esse método é rápido e fácil, mas não permite a personalização do [!INCLUDE[tsql](../../includes/tsql-md.md)] código que define o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do SQL Azure, diferentes procedimentos armazenados.  
  
Se você quiser modificar o [!INCLUDE[tsql](../../includes/tsql-md.md)] que é usado para criar objetos, ou se você quiser mais controle sobre a criação de objetos, use o SSMA para criar scripts. Você pode, em seguida, modificar esses scripts, criar cada objeto individualmente e até mesmo usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar a criação desses objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Usando o SSMA para sincronizar objetos com o SQL Server  
Usar o SSMA para criar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos de banco de dados do SQL Azure, selecione os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure e, em seguida, sincronizar os objetos com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, conforme mostrado no procedimento a seguir. Por padrão, se os objetos já existirem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure e se os metadados do SSMA tem algumas alterações locais ou atualizações para a definição desses objetos muito, o SSMA irá alterar as definições de objeto em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode alterar o comportamento padrão, editando **configurações do projeto**.  
  
> [!NOTE]  
> Você pode selecionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos de banco de dados do SQL Azure que não foram convertidos de bancos de dados do Access. No entanto, o SSMA não recriar nem alterar esses objetos.  
  
**Para sincronizar objetos com o SQL Server ou SQL Azure**  
  
1.  Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure, expanda a parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o nó do SQL Azure e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem processados:  
  
    -   Para sincronizar um banco de dados completo, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para sincronizar ou omitir objetos individuais ou categorias de objetos, marque ou desmarque a caixa de seleção ao lado do objeto ou pasta.  
  
3.  Depois de selecionar os objetos a serem processados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure, clique com botão direito **bancos de dados**e, em seguida, clique em **sincronizar com o banco de dados**.  
  
    Você também pode sincronizar objetos individuais ou as categorias de objetos clicando com botão direito do objeto ou a pasta pai e, em seguida, clicando em **sincronizar com o banco de dados**.  
  
    Depois disso, o SSMA exibirá os **sincronizar com o banco de dados** caixa de diálogo, onde você pode ver dois grupos de itens. No lado esquerdo, o SSMA mostra representados em uma árvore de objetos de banco de dados selecionado. No lado direito, você pode ver uma árvore que representa os mesmos objetos nos metadados do SSMA. Você pode expandir a árvore clicando-se à direita ou esquerda botão ' +'. A direção da sincronização é mostrada na coluna ação colocado entre as duas árvores.  
  
    Um sinal de ação pode estar em três estados:  
  
    -   Uma seta para a esquerda significa que o conteúdo de metadados será salvo no banco de dados (o padrão).  
  
    -   Uma seta para a direita significa que o conteúdo do banco de dados substituirão os metadados do SSMA.  
  
    -   Um sinal cruzado significa que nenhuma ação será tomada.  
  
    Clique no sinal de ação para alterar o estado. Sincronização real será executada quando você clica **Okey** botão da **sincronizar com o banco de dados** caixa de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de script  
Se você quiser economizar [!INCLUDE[tsql](../../includes/tsql-md.md)] definições de objetos convertidos do banco de dados, ou se quiser alterar as definições de objeto e executar scripts por conta própria, você pode salvar definições de objeto para o banco de dados convertido [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts.  
  
**Para salvar um ou mais objetos em um script**  
  
1.  Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, expanda o nó superior (o nome do servidor) e, em seguida, expanda **bancos de dados**.  
  
2.  Siga um ou mais destes procedimentos:  
  
    -   Para criar o script de um banco de dados completo, selecione a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para executar scripts ou omitir exibições individuais, expanda o banco de dados, expanda **modos de exibição**e, em seguida, selecione ou desmarque a caixa de seleção ao lado do modo de exibição.  
  
    -   Para executar scripts ou omitir tabelas individuais, expanda o banco de dados, expanda **tabelas**e, em seguida, selecione ou desmarque a caixa de seleção ao lado da tabela.  
  
    -   Para executar scripts ou omitir índices individuais para uma tabela, expanda a tabela, expanda **índices**e, em seguida, selecione ou desmarque o índice.  
  
3.  Clique com botão direito **bancos de dados** e selecione **Salvar como Script**.  
  
    Você também pode gerar o script de objetos individuais. Para criar o script de um objeto, independentemente de qual objetos selecionados, o objeto com o botão direito e selecione **Salvar como Script**.  
  
4.  No **Salvar como** diálogo caixa, localize a pasta onde você deseja salvar o script, digite um nome de arquivo na **nome do arquivo** caixa e, em seguida, clique em **Okey**.  
  
    O SSMA acrescentará a extensão de nome de arquivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificando Scripts  
Depois de salvar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou definições de objeto do SQL Azure como um script, você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para modificar o script.  
  
**Para modificar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **arquivo** , aponte para **abra**e, em seguida, clique em **arquivo**.  
  
2.  No **aberto** caixa de diálogo, localize e selecione o arquivo de script e, em seguida, clique em **Okey**.  
  
3.  Edite o arquivo de script usando o editor de consultas.  
  
    Para obter mais informações sobre o editor de consultas, consulte "Editor de comandos e recursos de conveniência" no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
4.  Para salvar o script, no menu Arquivo, selecione **salvar**.  
  
### <a name="running-scripts"></a>Execução de Scripts  
Você pode executar um script ou instruções individuais, em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Para executar um script**  
  
1.  Sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **arquivo** , aponte para **abra** e, em seguida, clique em **arquivo**.  
  
2.  No **aberto** caixa de diálogo, localize e selecione o arquivo de script e, em seguida, clique em **Okey**.  
  
3.  Para executar o script completo, pressione a **F5** chave.  
  
4.  Para executar um conjunto de instruções, selecione as instruções na janela do editor de consulta e, em seguida, pressione a **F5** chave.  
  
Para obter mais informações sobre como usar o editor de consultas para executar scripts, consulte " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta" no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
Você também pode executar scripts da linha de comando usando o **sqlcmd** utilitário e de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Para obter mais informações sobre **sqlcmd**, consulte "utilitário sqlcmd" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte "automatizar tarefas administrativas ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente)" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="securing-objects-in-sql-server"></a>Protegendo os objetos no SQL Server  
Depois que você carregou os objetos de banco de dados convertido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível conceder e negar permissões nesses objetos. É uma boa ideia fazer isso antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre como ajudar a proteger objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte "Considerações para bancos de dados e banco de dados de aplicativos de segurança" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no processo de migração [migrar dados para o SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
