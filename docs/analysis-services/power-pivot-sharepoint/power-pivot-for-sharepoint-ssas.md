---
title: Power Pivot para SharePoint (SSAS) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fcfce0a21e66e0ae1e5a440eda0fd32fd7d1964b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68164304"
---
# <a name="power-pivot-for-sharepoint-ssas"></a>Power Pivot para SharePoint (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] fornece a hospedagem de servidor dos dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um farm do SharePoint. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são um modelo de dados analíticos que você cria usando um dos seguintes:  
  
-   O suplemento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do Excel 2010  
  
-   Excel 2013  
  
-   Excel 2016  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2016 | [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013  
  
 O servidor que hospeda esses dados exige o SharePoint, os Serviços do Excel e uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Os dados são carregados no [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para as instâncias do SharePoint, nas quais podem ser atualizados em intervalos agendados usando a funcionalidade de atualização de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que o servidor fornece para as pastas de trabalho do Excel 2010 que o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] fornece para as pastas de trabalho do Excel 2013 e 2016.  
  
## <a name="power-pivot-for-sharepoint-2016"></a>Power Pivot para SharePoint 2016  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] dá suporte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 2016 e Office Online Server o uso de pastas de trabalho do Excel com modelos de dados e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatórios do Power View.  
  
 Excel, dentro do servidor do Office Online inclui a funcionalidade de modelo de dados para habilitar a interação com um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pasta de trabalho no navegador. Você não precisa implantar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para o suplemento do SharePoint 2016 no farm. Você só precisa instalar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] server no [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] modo e registrar o servidor com o servidor do Office Online.  
  
 Implantar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para o suplemento do SharePoint 2016 permite mais funcionalidades e recursos em seu farm do SharePoint. Os recursos adicionais incluem a Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e a Atualização de Dados da Agenda.  
  
 ![Servidor de modo 3 Pivot com o servidor do Office Online de energia do SSAS](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-mode-3server-oos-deploy.png "SSAS do Power Pivot modo 3 Server com o servidor do Office Online")  
  
## <a name="power-pivot-for-sharepoint-2013"></a>Power Pivot para SharePoint 2013  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] oferece suporte ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] uso de Serviços do Excel do SharePoint 2013 de pastas de trabalho do Excel com modelos de dados e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatórios do Power View.  
  
 Os Serviços do Excel no SharePoint 2013 incluem a funcionalidade de modelo de dados para habilitar a interação com uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no navegador. Você não precisa implantar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para o suplemento do SharePoint 2013 no farm. Você só precisará instalar um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint e registrar o servidor nas configurações do **Modelo de Dados** dos Serviços do Excel.  
  
 Implantar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para o suplemento do SharePoint 2013 permite mais funcionalidades e recursos em seu farm do SharePoint. Os recursos adicionais incluem a Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , Atualização de Dados da Agenda e o Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 ![Implantação de servidor de modo 2 do PowerPivot do SSAS](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-mode-2server-deployment.gif "implantação de servidor de modo 2 do PowerPivot do SSAS")  
  
##  <a name="bkmk_RelatedContent"></a> Nesta seção  
 [Administração e configuração de servidor do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Configuração do Power Pivot usando o Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 [Ferramentas de Configuração do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
 [Autenticação e autorização do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md)  
  
 [Configurar regras de integridade do Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)  
  
 [Painel de Gerenciamento Power Pivot e dados de uso](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)  
  
 [Galeria do Power Pivot](http://msdn.microsoft.com/library/2a0db616-e08e-4062-aac8-979f8cad7794)  
  
 [Acesso a dados do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-access.md)  
  
 [Atualização de Dados PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
 [Feeds de dados do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
 [Conexão de modelo semântico de BI &#40;.bism&#41; do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)  
  
 **Nas outras seções**  
  
## <a name="additional-topics"></a>Tópicos adicionais  
 [Atualizar Power Pivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)  
  
 [Instale o Analysis Services no modo do Power Pivot.](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [Referência do PowerShell para Power Pivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)  
  
 [Custos e topologias de licença de exemplo para o Business Intelligence do SQL Server 2016](http://msdn.microsoft.com/library/682b8711-407a-48d1-9807-415d4c24dad6)  
  
## <a name="see-also"></a>Consulte também  
 [Planejamento e Implantação do Power Pivot](http://go.microsoft.com/fwlink/?linkID=220972)   
 [Recuperação de Desastres do Power Pivot para SharePoint](http://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
