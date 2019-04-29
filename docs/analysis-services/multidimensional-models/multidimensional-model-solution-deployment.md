---
title: Implantação de solução de modelo multidimensional | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3aba02dfe34f91b12a98f4d557bdb2dc516b1b1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042462"
---
# <a name="multidimensional-model-solution-deployment"></a>Implantação de solução de modelo multidimensional
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Depois de você ter concluído o desenvolvimento de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , poderá implantar o banco de dados em um servidor do Analysis Services. O Analysis Services fornece seis métodos de implantação possíveis que podem ser usados para mover o banco de dados para um servidor de teste ou produção. Os métodos estão listados aqui em ordem de eficiência: Automatização do AMO, XMLA, Assistente para implantação, utilitário de implantação, sincronize o assistente, Backup e restauração.  
  
 Este tópico inclui as seguintes seções:  
  
 [Métodos de implantação](#bkmk_meth)  
  
 [Considerações de implantação](#bkmk_considerations)  
  
 [Tarefas relacionadas](#bkmk_rel)  
  
##  <a name="bkmk_meth"></a> Métodos de implantação  
  
|Método|Descrição|Link|  
|------------|-----------------|----------|  
|**Usando Automação AMO (Objetos de Gerenciamento de Análise)**|AMO fornece uma interface programática para o conjunto completo de comandos definidos para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], incluindo comandos que podem ser usados para implantação de solução. Como uma abordagem para implantação de solução, a automação AMO é a mais flexível, mas também a que exige um esforço de programação.  Uma vantagem importante para usar AMO é que você pode usar o SQL Server Agent com o aplicativo AMO para executar a implantação em uma programação predefinida.|[Desenvolvendo com AMO &#40;Objetos de Gerenciamento de Análise&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|**XMLA**|Use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerar um script XMLA dos metadados de um banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, em seguida, executar esse script em outro servidor para recriar o banco de dados inicial. Os scripts XMLA são gerados facilmente no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ao definir o processo de implantação e, em seguida, codificá-lo e salvá-lo como um script XMLA. Quando o script XMLA está em um arquivo salvo, é possível executá-lo de acordo com uma programação ou inseri-lo em um aplicativo que se conecta diretamente em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> Também é possível executar scripts XMLA em uma base predefinida com o SQL Server Agent, mas não haverá a mesma flexibilidade do AMO. O AMO fornece uma amplitude maior de funcionalidade hospedando o espectro completo de comandos administrativos.|[Implantar soluções de modelo usando XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**Assistente para Implantação**|Use o Assistente para Implantação para usar os arquivos de saída do XMLA gerados por um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implantar os metadados do projeto em um servidor de destino. Com o Assistente para Implantação, é possível implantar diretamente a partir do arquivo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , conforme criado pelo diretório de saída do construtor de projetos.<br /><br /> A vantagem principal de usar o Assistente de Implantação do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é conveniência. Da mesma maneira que você pode salvar um script XMLA para usar posteriormente no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], pode salvar scripts do Assistente de Implantação. O Assistente para Implantação pode ser executado de modo interativo e no prompt de comando utilizando o Utilitário de Implantação.|[Deploy Model Solutions Using the Deployment Wizard](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**Utilitário de Implantação**|O utilitário de Implantação permite iniciar o mecanismo de implantação do Analysis Services de um prompt de comando.|[Implantar soluções modelo com o Utilitário de Implantação](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**Assistente para Sincronizar Banco de Dados**|Use o Assistente para Sincronizar Bancos de Dados para sincronizar os metadados e os dados entre quaisquer dois bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .<br /><br /> O Assistente para Sincronizar pode ser usado para copiar os dados e os metadados de um servidor de origem em um servidor de destino. Se o servidor de destino não tiver uma cópia do banco de dados que você deseja implantar, um novo banco de dados é copiado para o servidor de destino. Se o servidor de destino já tiver uma cópia do mesmo banco de dados, o banco de dados no servidor de destino será atualizado para usar os metadados e os dados no banco de dados de origem.|[Sincronizar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)|  
|**Backup e restauração**|O backup oferece a abordagem mais simples para transferir bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Na caixa de diálogo **Backup** , é possível definir a configuração das opções e, em seguida, executar o backup na própria caixa de diálogo. Se preferir, crie um script que pode ser salvo e executado com a frequência necessária.<br /><br /> O backup e a restauração não são usados com tanta frequência como os outros métodos, mas podem ajudar a concluir rapidamente uma implantação com requisitos mínimos de infraestrutura.|[Backup e restauração de bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_considerations"></a> Considerações de implantação  
 Antes de você implantar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , considere quais dessas perguntas aplicam-se à sua solução e, em seguida, examine o link relacionado para conhecer as maneiras de tratar o problema:  
  
|Consideração|Link para mais informações|  
|-------------------|------------------------------|  
|Que recursos de hardware e software são necessários para essa solução?|[Requisitos e considerações sobre a implantação do Analysis Services](../../analysis-services/multidimensional-models/requirements-and-considerations-for-analysis-services-deployment.md)|  
|Como serão implantados os objetos relacionados que estão fora do escopo do projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , como pacotes, relatórios ou esquemas de banco de dados relacional do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ?||  
|Como os dados serão carregados e atualizados no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implantado?<br /><br /> Como os metadados (como cálculos) serão atualizados no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implantado?|[Métodos de implantação](#bkmk_meth) neste tópico.|  
|Deseja conceder aos usuários acesso aos dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pela Internet?|[Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|  
|Deseja fornecer acesso de consulta contínuo aos dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ?|[Requisitos e considerações sobre a implantação do Analysis Services](../../analysis-services/multidimensional-models/requirements-and-considerations-for-analysis-services-deployment.md)|  
|Deseja implantar objetos em um ambiente distribuído usando objetos vinculados ou partições remotas?|[Criar e gerenciar uma partição local&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md), [Criar e gerenciar uma partição remota&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md) e [Grupos de medidas vinculados](../../analysis-services/multidimensional-models/linked-measure-groups.md).|  
|Como os dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] serão protegidos?|[Autorizando o acesso a objetos e operações &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)|  
  
##  <a name="bkmk_rel"></a> Tarefas relacionadas  
 [Requisitos e considerações sobre a implantação do Analysis Services](../../analysis-services/multidimensional-models/requirements-and-considerations-for-analysis-services-deployment.md)  
  
 [Implantar soluções de modelo usando XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)  
  
 [Implantar soluções de modelo usando o Assistente de implantação](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
 [Implantar soluções de modelo com o Utilitário de Implantação](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  
