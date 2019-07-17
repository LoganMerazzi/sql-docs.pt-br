---
title: Introdução ao SSMA para Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA for Oracle, Metadata Explorers
- SSMA for Oracle, Toolbars
ms.assetid: df79664c-972e-4bef-865a-ce609789fee7
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: ef71a9355bc11c4d377f00a44b2b8cd2958f8656
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264454"
---
# <a name="getting-started-with-ssma-for-oracle-oracletosql"></a>Introdução ao SSMA para Oracle (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração (SSMA) para Oracle permite que você rapidamente converter esquemas de banco de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, carregar os esquemas resultantes em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrar dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda você a se familiarizar com a interface de usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
Para usar o SSMA, você primeiro deve instalar o programa cliente SSMA em um computador que pode acessar o banco de dados do Oracle de origem e a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você deve instalar um pacote de extensão e pelo menos um dos provedores do Oracle (OLE DB ou [!INCLUDE[vstecado](../../includes/vstecado_md.md)]) no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses componentes oferecem suporte a migração de dados e a emulação de funções do sistema Oracle. Para obter instruções de instalação, consulte [instalar o SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md).  
  
Para iniciar o SSMA, clique em **inicie**, aponte para **todos os programas**, aponte para  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle**e, em seguida, clique em  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Assistente de migração para o Oracle**.  
  
## <a name="ssma-for-oracle-user-interface"></a>SSMA para Interface de usuário do Oracle  
Depois que o SSMA é instalado, você pode usar o SSMA para migrar bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele ajuda a se familiarizar com a interface de usuário do SSMA antes de começar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![SSMA para UI Oracle](../../ssma/oracle/media/ssma_oracle_ui.jpg "SSMA para UI Oracle")  
  
Para iniciar uma migração, você deve primeiro criar um novo projeto. Em seguida, você se conectar ao banco de dados Oracle. Após uma conexão bem-sucedida, esquemas Oracle aparecerá no Gerenciador de metadados do Oracle. Você pode então objetos do botão direito do mouse no Gerenciador de metadados do Oracle para executar tarefas como criar relatórios que avaliam as conversões para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você também pode executar essas tarefas usando os menus e barras de ferramentas.  
  
Você também deve se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Após uma conexão bem-sucedida, uma hierarquia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados aparecerão no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. Depois de converter esquemas Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, selecione as esquemas convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e, em seguida, sincronizar os esquemas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Depois de sincronizar esquemas convertidas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode retornar ao Gerenciador de metadados do Oracle e migrar dados de esquemas Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados.  
  
Para obter mais informações sobre essas tarefas e como realizá-las, consulte [migração de bancos de dados Oracle para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md).  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações no Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados.  
  
#### <a name="oracle-metadata-explorer"></a>Gerenciador de metadados do Oracle  
Gerenciador de metadados do Oracle mostra informações sobre esquemas Oracle. Usando o Gerenciador de metadados do Oracle, você pode executar as seguintes tarefas:  
  
-   Procure os objetos em cada esquema.  
  
-   Selecionar objetos para a conversão e, em seguida, converter os objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe. Para obter mais informações, consulte [converter esquemas do Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
-   Selecionar tabelas para migração de dados e, em seguida, migrar os dados dessas tabelas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [migrando dados do Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>Gerenciador de metadados do SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados mostra informações sobre uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando você se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA recupera metadados sobre essa instância e o armazena no arquivo de projeto.  
  
Você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados para selecionar objetos de banco de dados Oracle convertidos e, em seguida, sincronizar esses objetos com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Para obter mais informações, consulte [Carregando objetos de banco de dados convertidos no SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados são guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do Oracle, seis guias serão exibida: **Tabela**, **SQL**, **tipo de mapeamento, o relatório**, **propriedades**, e **dados**. O **relatório** guia contém informações somente depois de criar um relatório que contém o objeto selecionado. Se você selecionar uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, três guias serão exibida: **Tabela**, **SQL**, e **dados**.  
  
A maioria das configurações de metadados são somente leitura. No entanto, você pode alterar os metadados a seguir:  
  
-   No Gerenciador de metadados do Oracle, você pode alterar procedimentos e mapeamentos de tipo. Para converter os procedimentos alterados e mapeamentos de tipo, faça as alterações antes de converter esquemas.  
  
-   Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, você pode alterar o [!INCLUDE[tsql](../../includes/tsql-md.md)] para procedimentos armazenados. Para ver essas alterações nas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], faça essas alterações antes de carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas do projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
O projeto contém botões para trabalhar com projetos, conectar-se ao Oracle e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses botões se parecer com os comandos na **arquivo** menu.  
  
#### <a name="migration-toolbar"></a>Barra de ferramentas de migração  
A tabela a seguir mostra a migração de comandos da barra de ferramentas:  
  
|Botão|Função|  
|------|--------|  
|**Criar relatório**|Converte os objetos selecionados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe e, em seguida, cria um relatório que mostra a conversão foi bem-sucedida como.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do Oracle.|  
|**Converter esquema**|Converte os objetos selecionados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do Oracle.|  
|**Migrar dados**|Migra dados do banco de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de executar esse comando, você deve converter esquemas Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas e, em seguida, carregue os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do Oracle.|  
|**Parar**|Interrompe o processo atual.|  
  
### <a name="menus"></a>Menus  
A tabela a seguir mostra os menus do SSMA.  
  
|Menu|Descrição|  
|----|-----------|  
|**Arquivo**|Contém comandos para trabalhar com projetos, conectar-se ao Oracle e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] do painel de detalhes do SQL. Também contém o **gerenciar indicadores** opção, onde você poderá ver uma lista de indicadores atuais. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o **sincronizar metadados Explorers** comando. Que sincroniza os objetos entre o Gerenciador de metadados do Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. Também contém comandos para mostrar e ocultar os **saída** e **lista de erros** painéis e uma opção **Layouts** para gerenciar os Layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios e migrar dados e objetos. Também fornece acesso para o **configurações globais** e **configurações do projeto** caixas de diálogo.|  
|**Testador**|Contém comandos para criar e trabalhar com casos de teste, o repositório e o sistema de gerenciamento de backup.|  
|**Ajuda**|Fornece acesso para ajudar a SSMA e para o **sobre** caixa de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e o painel de lista de erros  
O **exibição** menu fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel de saída mostra mensagens de status do SSMA durante a conversão do objeto de sincronização de objetos e migração de dados.  
  
-   O painel de lista de erros mostra o erro, aviso e mensagens informativas em uma lista classificável.  
  
## <a name="see-also"></a>Consulte também  
[Migração de dados Oracle para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md)  
[Referência da Interface do usuário &#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
