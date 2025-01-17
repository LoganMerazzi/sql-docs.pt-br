---
title: Destino do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdest.f1
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: a0227cd8-6944-4547-87e8-7b2507e26442
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 818f78cd0b38aba0a7201eb28f49eb573ba32672
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770660"
---
# <a name="sql-server-destination"></a>destino do SQL Server
  O destino do SQL Server conecta-se a um banco de dados local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e efetua carregamentos de dados em massa em tabelas e modos de exibição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não é possível usar o destino do SQL Server em pacotes que acessam um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor remoto. Em vez disso, os pacotes devem usar o destino OLE DB. Para obter mais informações, consulte [OLE DB Destination](ole-db-destination.md).  
  
## <a name="permissions"></a>Permissões  
 Usuários que executam pacotes que incluem o destino do SQL Server precisam da permissão "Criar objetos globais". Você pode conceder esta permissão aos usuários usando a ferramenta Política de Segurança Local, aberta no menu **Ferramentas Administrativas** . Se você receber uma mensagem de erro ao executar um pacote que usa o destino do SQL Server, assegure-se de que a conta que executa o pacote tenha a permissão "Criar objetos globais".  
  
## <a name="bulk-inserts"></a>Inserções em massa  
 Se tentar usar o destino do SQL Server para carregar dados em massa em um banco de dados de um SQL Server remoto, você poderá ver uma mensagem de erro semelhante à seguinte: "Um registro OLE DB está disponível. Origem: "Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client" Hresult: 0x80040E14 Descrição: "Não foi possível fazer o carregamento em massa porque o objeto de mapeamento de arquivo SSIS 'Global\DTSQLIMPORT' não pôde ser aberto. Erro de sistema operacional código 2 (O sistema não pode achar o arquivo especificado.). Certifique-se de estar acessando um servidor local via "segurança do Windows."  
  
 O destino do SQL Server oferece a mesma inserção de dados em alta velocidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que a tarefa de Inserção em Massa fornece, porém, usando o destino do SQL Server, você pode aplicar transformações em dados de coluna antes de os dados serem carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para carregar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deve-se considerar o uso do destino do SQL Server em vez do destino do OLE DB.  
  
### <a name="bulk-insert-options"></a>Opções de inserção de massa  
 Se o destino do SQL Server usar um modo de acesso de dados da carga-rápida, você poderá especificar as seguintes opções de carga rápida:  
  
-   Reter valores de identidade do arquivo de dados importado ou usar valores exclusivos atribuídos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Reter valores nulos durante a operação de carregamento em massa.  
  
-   Verificar restrições na tabela de destino ou exibir durante a operação de importação em massa.  
  
-   Adquirir um bloqueio em nível de tabela pela duração da operação de carregamento em massa.  
  
-   Executar disparadores de inserção definidos na tabela de destino durante a operação de carregamento em massa.  
  
-   Especificar o número da primeira linha na entrada a ser carregada durante a operação de inserção em massa.  
  
-   Especificar o número da última linha na entrada a ser carregada durante a operação de inserção em massa.  
  
-   Especificar o número máximo de erros permitidos antes que a operação de inserção em massa seja cancelada. Cada linha que não puder ser importada será contada como um erro.  
  
-   Especificar as colunas na entrada que contêm dados ordenados.  
  
 Para obter mais informações sobre as opções de carregamento em massa, consulte [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
#### <a name="performance-improvements"></a>Melhorias no desempenho  
 Para melhorar o desempenho de uma inserção de massa e o acesso aos dados de tabela durante a operação de inserção em massa, você deve alterar as opções padrão conforme o seguinte:  
  
-   Não verificar restrições na tabela de destino ou exibir durante a operação de importação em massa.  
  
-   Não executar disparadores de inserção definidos na tabela de destino durante a operação de carregamento em massa.  
  
-   Não aplicar um bloqueio à tabela. Desse modo, a tabela permanece disponível para outros usuários e aplicativos durante a operação de inserção em massa.  
  
## <a name="configuration-of-the-sql-server-destination"></a>Configuração do destino do SQL Server  
 É possível configurar o destino do SQL Server das seguintes maneiras:  
  
-   Especificar a tabela ou exibir em qual carregar os dados em massa.  
  
-   Personalizar a operação de carregamento em massa especificando opções como verificar restrições ou não.  
  
-   Especificar se todas as linhas confirmam em um lote ou definem o número de máximo de linhas para confirmar como um lote.  
  
-   Especificar um tempo-limite para a operação de carregamento em massa.  
  
 Esse destino usa um gerenciador de conexões OLE DB para conectar-se a uma fonte de dados e o gerenciador de conexões especifica o provedor OLE DB a ser usado. Para obter mais informações, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
 Um projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também fornece o objeto de fonte de dados do qual se pode criar um administrador de conexão OLE DB. Isto torna as fontes de dados e exibições de fontes de dados disponíveis para o destino do SQL Server.  
  
 O destino do SQL Server tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Destino do SQL Server**, clique em um dos seguintes tópicos:  
  
-   [Editor de Destinos SQL &#40;página Gerenciador de Conexões&#41;](../sql-destination-editor-connection-manager-page.md)  
  
-   [Editor de Destinos SQL &#40;página Mapeamentos&#41;](../sql-destination-editor-mappings-page.md)  
  
-   [Editor de Destinos SQL &#40;página Avançado&#41;](../sql-destination-editor-advanced-page.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas do destino SQL Server](sql-server-destination-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Carregar dados em massa por meio do destino do SQL Server](sql-server-destination.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Carregar dados em massa por meio do destino do SQL Server](sql-server-destination.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo técnico, [You may get "Unable to prepare the SSIS bulk insert for data insertion" error on UAC enabled systems](https://go.microsoft.com/fwlink/?LinkId=199482)(Você pode receber o erro “Não é possível preparar a inserção em massa do SSIS para a inserção de dados” em sistemas habilitados para UAC), em support.microsoft.com.  
  
-   Artigo técnico, [The Data Loading Performance Guide](https://go.microsoft.com/fwlink/?LinkId=233700), em msdn.microsoft.com.  
  
-   Artigo técnico, [Using SQL Server Integration Services to Bulk Load Data](https://go.microsoft.com/fwlink/?LinkId=233701)(Usando o SQL Server Integration Services para carregar dados em massa), em simple-talk.com.  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](data-flow.md)  
  
  
