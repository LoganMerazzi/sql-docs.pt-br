---
title: Introdução ao SQL Server Management Studio para Business Intelligence | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab38a4465ec03415f9c1d903419ccbe2b07e6a86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63015898"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>Introdução ao SQL Server Management Studio para Business Intelligence
  Para acessar, configurar, gerenciar e administrar o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], use o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Embora essas três tecnologias de business intelligence dependam do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], as tarefas administrativas associadas a cada tecnologia são ligeiramente diferentes.  
  
> [!NOTE]  
>  Para criar e modificar soluções [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , use [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], não [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] é um ambiente de desenvolvimento baseado no [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>Gerenciando as soluções do Analysis Services com o SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite gerenciar objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , como executar backups e processar objetos.  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] fornece um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Script no qual é possível desenvolver e salvar scripts gravados em MDX (expressões MDX), DMX (extensões DMX) e XMLA (XML for Analysis). Use os projetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Script para executar tarefas de gerenciamento ou recriar objetos, como bancos de dados e cubos, nas instâncias do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Por exemplo, você pode desenvolver um script XMLA em um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Script que cria novos objetos diretamente em uma instância existente do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Os projetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Script podem ser salvos como parte de uma solução e integrados ao controle do código fonte.  
  
 Para obter mais informações sobre como usar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], consulte [projeto de Scripts do Analysis Services no SQL Server Management Studio](../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>Gerenciando as soluções do Integration Services com o SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite usar o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para gerenciar pacotes e monitorar os pacotes em execução. Você também pode usar o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para organizar os pacotes em pastas, executar pacotes, importar e exportar pacotes, migrar pacotes DTS e atualizar pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>Gerenciando os projetos do Reporting Services com o SQL Server Management Studio  
 Use o SQL Server Management Studio para habilitar recursos do Reporting Services, administrar o servidor e os bancos de dados e gerenciar funções e trabalhos.  
  
 Você pode gerenciar agendas compartilhadas usando a pasta Agendas Compartilhadas e gerenciar bancos de dados do servidor de relatórios (ReportServer, ReportServerTempdb). Você também pode criar uma função RSExecRole no banco de dados Mestre do sistema ao mover um banco de dados de servidor de relatórios para um Mecanismo de Banco de Dados do SQL Server novo ou diferente ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]). Para obter mais informações sobre essas tarefas, consulte os seguintes tópicos:  
  
-   [Reporting Services no SQL Server Management Studio &#40;SSRS&#41;](../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
-   [Administrar um banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../reporting-services/report-server/report-server-database-ssrs-native-mode.md)  
  
-   [Criar o RSExecRole](../reporting-services/security/create-the-rsexecrole.md)  
  
 Você também pode gerenciar o servidor habilitando e configurando vários recursos, definindo padrões de servidor e gerenciando funções e trabalhos. Para obter mais informações sobre essas tarefas, consulte os seguintes tópicos:  
  
-   [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../reporting-services/tools/set-report-server-properties-management-studio.md)  
  
-   [Criar, excluir ou modificar uma função &#40;Management Studio&#41;](../reporting-services/security/role-definitions-create-delete-or-modify.md)  
  
-   [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criação de modelos multidimensionais usando o SSDT &#40;SQL Server Data Tools&#41;](../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [O Reporting Services no SQL Server Data Tools &#40;SSDT&#41;](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
  
