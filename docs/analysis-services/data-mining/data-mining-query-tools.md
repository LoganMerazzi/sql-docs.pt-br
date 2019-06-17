---
title: Ferramentas de consulta de mineração de dados | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 697a1c06a2d30d5721c122c557f3e41836335b02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65449945"
---
# <a name="data-mining-query-tools"></a>Ferramentas de Consulta de Mineração de Dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Todas as consultas de mineração de dados são baseadas na linguagem DMX (Extensões DMX). A DMX é usada para criar modelos para todos os tipos de tarefa de aprendizado de máquina, inclusive classificação, análise de risco, geração de recomendações e regressão linear. Você também pode gravar consultas DMX para obter informações sobre os padrões e as estatísticas que foram geradas após processar o modelo.  
  
 Você pode escrever sua própria DMX ou criar uma DMX básica usando uma ferramenta como o **Construtor de Consultas de Previsão** e depois modificá-la. Tanto o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quanto o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornecem ferramentas que o ajudam a criar consultas de previsão em DMX. Este tópico descreve como criar e executar consultas de mineração de dados usando essas ferramentas.  
  
-   [Construtor de Consultas de Previsão](#bkmk_Builder)  
  
-   [Editor de Consultas](#bkmk_QueryEditor)  
  
-   [Modelos DMX](#bkmk_Templates)  
  
-   [Integration Services](#bkmk_SSIS)  
  
-   [Interfaces de programação de aplicativo](#bkmk_API)  
  
##  <a name="bkmk_Builder"></a> Construtor de Consultas de Previsão  
 O Construtor de Consultas de Previsão está incluído na guia **Previsão do Modelo de Mineração** do Designer de Data Mining, que esta disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Ao utilizar o construtor de consultas, você seleciona um modelo de mineração, adiciona um novo caso de dados e funções de previsão. Você pode mudar para o editor de texto para modificar a consulta manualmente ou mudar para o painel **Resultados** para exibir os resultados da consulta.  
  
##  <a name="bkmk_QueryEditor"></a> Editor de Consultas  
 O Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] também permite criar e executar consultas DMX. É possível conectar-se a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e selecionar um banco de dados, colunas de estrutura de mineração e um modelo de mineração. O **Gerenciador de Metadados** contém uma lista de funções de previsão que você pode procurar.  
  
##  <a name="bkmk_Templates"></a> Modelos DMX  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece modelos de consulta interativa DMX que você poderá usar para criar consultas DMX. Se você não vir a lista de modelos, clique em **Exibição** na barra de ferramentas e selecione **Explorador de Modelos**. Para ver todos os modelos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , incluindo modelos para DMX, MDX e XMLA, clique no ícone do cubo.  
  
 Para criar uma consulta usando um modelo, você pode arrastar o modelo em uma janela de consulta aberta ou pode clicar duas vezes no modelo para abrir uma nova conexão e um novo painel de consulta.  
  
 Para ver um exemplo de como criar uma consulta de previsão com base em um modelo, consulte [Criar uma consulta de previsão Singleton com base em um modelo](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md).  
  
> [!WARNING]  
>  O Suplemento de Mineração de Dados para o Microsoft Office Excel também contém vários modelos, junto com um construtor de consultas interativo que pode ajudá-lo a compor instruções DMX complexas. Para usar os modelos, clique em **Consulta**e **Avançado** no Cliente de Mineração de Dados.  
  
##  <a name="bkmk_SSIS"></a> Componentes de mineração de dados do Integration Services  
 É possível também incluir consultas de previsão como parte de um pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . As tarefas e transformações no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a seguir fornecem suporte para a criação e execução de consultas de previsão de DMX e instruções DMX.  
  
|Componente|Descrição|  
|---------------|-----------------|  
|Tarefa Consulta de Mineração de dados|Executa consultas DMX e outras instruções DMX como parte de um fluxo de controle.<br /><br /> O editor de tarefa fornece o Construtor de Consulta de Previsão e uma caixa de texto para modificar a consulta DMX manualmente. Porém, o editor de tarefa não pode validar a consulta em objetos em uma solução do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Portanto, é melhor criar uma consulta dentro do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e, em seguida, colar o texto da instrução ou consulta no editor de tarefa.|  
|Transformação Consulta de Mineração de Dados|Executa uma consulta de previsão dentro de um fluxo de dados, usando os dados fornecidos por uma fonte de fluxo de dados.<br /><br /> O editor de tarefa fornece o Construtor de Consulta de Previsão e uma caixa de texto para modificar a consulta DMX manualmente.<br /><br /> A transformação somente pode ser usada para criar consultas que usam dados no fluxo de dados; ou seja, consultas que usam a sintaxe PREDICTION JOIN. Este componente não pode ser usado para executar consultas de conteúdo ou outros tipos de instruções DMX.|  
  
##  <a name="bkmk_API"></a> Interfaces de programação de aplicativo  
 Você pode criar aplicativos personalizados que executam consultas em relação a modelos de mineração de dados usando uma variedade de linguagens de programação, em combinação com protocolos de servidor como OLE DB ou cliente ADOMD do Analysis Services. Para obter mais informações, consulte [Programação de Data Mining](../../analysis-services/data-mining/data-mining-programming.md).  
  
 Porém, o XMLA constitui o formato de mensagem subjacente para todas as interações com um servidor do Analysis Service. Dentro de uma mensagem de XMLA, as consultas são representadas de maneira diferente dependendo se você está enviando uma consulta de previsão com base em DMX, uma consulta de conteúdo ou uma consulta que recupera metadados modelo usando os conjuntos de linhas de esquema de mineração de dados.  
  
-   O texto de **consultas de previsão** (e todas as outras instruções DMX) é enviado em XMLA usando o método [Método Execute &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute), com a consulta DMX colocada como texto dentro do [Elemento Statement &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) do elemento [Elemento Command &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/command-element-xmla).  
  
-   Para recuperar o **conteúdo modelo** e os **metadados modelo**, como o número de clusters, os atributos usados em árvores de decisão, a data de processamento do modelo e os parâmetros de algoritmo usados ao criar o modelo, você pode usar o método [Método Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) e especificar um dos conjuntos de linhas de esquema de mineração de dados no cabeçalho [Elemento RequestType &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/requesttype-element-xmla). Para restringir o escopo da consulta, insira critérios como restrições dentro do elemento [Elemento RestrictionList &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictionlist-element-xmla).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de DMX &#40;extensões DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md)   
 [Soluções de mineração de dados](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Compreendendo a instrução DMX Select](../../dmx/understanding-the-dmx-select-statement.md)   
 [Estrutura e uso de consultas de previsão DMX](../../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Criar uma consulta de previsão usando o construtor de consultas de previsão](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)   
 [Criar uma consulta DMX no SQL Server Management Studio](../../analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
