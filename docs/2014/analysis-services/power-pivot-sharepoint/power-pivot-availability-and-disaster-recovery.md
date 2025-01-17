---
title: Disponibilidade do PowerPivot e recuperação de desastres (SQL Server 2014) | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4aaf008c-3bcb-4dbf-862c-65747d1a668c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1f975fe18b76c4e748d7d2969d20c53b5818f0c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071326"
---
# <a name="powerpivot-availability-and-disaster-recovery-sql-server-2014"></a>Disponibilidade do PowerPivot e recuperação de desastres (SQL Server 2014)
  Os planos de recuperação de desastres e disponibilidade para [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] dependem principalmente do design do seu farm do SharePoint, o tempo de inatividade aceitável para componentes diferentes, além de ferramentas e práticas recomendadas implementadas para disponibilidade do SharePoint. Este tópico resume as tecnologias e inclui diagramas de topologia de exemplo a serem considerados ao planejar a disponibilidade e a recuperação de desastres para a implantação de um [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **Neste tópico:**  
  
-   [Exemplo de topologia do SharePoint 2013 para alta disponibilidade do PowerPivot](#bkmk_sharepoint2013)  
  
-   [Exemplo de topologia do SharePoint 2010 para alta disponibilidade do PowerPivot](#bkmk_sharepoint2010)  
  
-   [O banco de dados do aplicativo de serviço PowerPivot e as tecnologias de disponibilidade e recuperação do SQL Server](#bkmk_sql_server_technologies)  
  
-   [Links para mais informações](#bkmk_more_resources)  
  
##  <a name="bkmk_sharepoint2013"></a> Exemplo de topologia do SharePoint 2013 para alta disponibilidade do PowerPivot  
 Em uma implantação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013, há mais flexibilidade em como você projeta a disponibilidade do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . No SharePoint 2013, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implantada no modo do SharePoint, também conhecido como o servidor [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , é executado fora do farm do SharePoint e pode ser instalado em servidores separados. Cada instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint é registrado nos serviços do Excel. O serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] compartilhado e o aplicativo de serviço executado em servidores de aplicativos do SharePoint.  
  
 O diagrama a seguir ilustra um exemplo de implantação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013. Este exemplo dá suporte à boa disponibilidade dos serviços do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] e pressupõe que os bancos de dados passam por backup regularmente.  
  
 ![disponibilidade do PowerPivot no 2013](../media/ssas-powerpivot-services-2013.png "disponibilidade do powerpivot no 2013")  
  
-   **(1)** Os servidores front-end da Web. Use o suplemento do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 para instalar os provedores de dados em cada servidor. Para obter mais informações, consulte [instalar ou desinstalar o PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
-   **(2)** O serviço compartilhado do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é executado **em cada** servidor de aplicativos e permite a execução do aplicativo de serviço **entre** servidores de aplicativos. Portanto, se um único servidor de aplicativos ficar offline, o aplicativo [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] ainda estará disponível.  
  
-   **(3)** Os serviços de cálculo do Excel são executados um em cada servidor de aplicativos e permitem que o aplicativo de serviço seja executado em servidores de aplicativos. Portanto, se um único servidor de aplicativos ficar offline, os serviços de cálculo do Excel ainda estarão disponíveis.  
  
-   **(4)**  e **(6)** instâncias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ins modo do SharePoint é executado em servidores fora do farm do SharePoint, isso inclui o serviço do Windows **SQL Server Analysis Services (POWERPIVOT)** . Cada uma dessas instâncias é registrada nos serviços do Excel **(3)** . Os Serviços do Excel gerenciam o balanceamento de carga de solicitações para os servidores [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . A arquitetura do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 permite que você tenha vários servidores para [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para que você possa adicionar facilmente mais instâncias, conforme necessário. Para obter mais informações, consulte [Gerenciar as configurações do modelo de dados dos serviços do Excel (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\).aspx).  
  
-   **(5)** Os bancos de dados do SQL Server usados para o conteúdo, a configuração e os bancos de dados do aplicativo. Isso inclui o banco de dados de aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O seu plano de recuperação de desastres deve incluir a camada de banco de dados. Nesse design, os bancos de dados são executados no mesmo servidor como **(4)** uma das instâncias [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . **(4)** e **(5)** também poderiam estar em servidores diferentes.  
  
-   **(7)** Alguma forma de backup ou redundância de banco de dados do SQL Server.  
  
##  <a name="bkmk_sharepoint2010"></a> Exemplo de topologia do SharePoint 2010 para alta disponibilidade do PowerPivot  
 A arquitetura do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 exige que todos os componentes [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sejam executados nos mesmos servidores de aplicativo do SharePoint. Isso inclui a instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implantada no modo do SharePoint e dois serviços compartilhados comparados com apenas um em uma implantação do SharePoint 2013.  
  
 O diagrama a seguir ilustra um exemplo de implantação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010. Este exemplo dá suporte à boa disponibilidade dos serviços do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] e pressupõe que os bancos de dados passam por backup regularmente.  
  
 ![disponibilidade do PowerPivot no sharepoint 2010](../media/ssas-powerpivot-services-2010.png "disponibilidade do powerpivot no sharepoint 2010")  
  
-   **(1)** Os servidores front-end da Web. Instale os provedores de dados em cada servidor. Para obter mais informações, consulte [Instalar o Provedor OLE DB do Analysis Services nos Servidores SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
-   **(2)**  Dois [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] serviços compartilhados e **(4)** o serviço do Windows **SQL Server Analysis Services (POWERPIVOT)** estão instalados nos servidores de aplicativo do SharePoint.  
  
     O Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é executado **em cada** servidor de aplicativos e permite a execução do aplicativo de serviço **entre** servidores de aplicativos. Se um único servidor de aplicativos ficar offline, o aplicativo de serviço [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] ainda estará disponível.  
  
     Para aumentar a capacidade de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um SharePoint 2010, implantar mais servidores de aplicativos do SharePoint executando o Serviço do Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   **(3)** Os Serviços de Cálculo do Excel são executados em cada servidor de aplicativos e permite que o aplicativo de serviço seja executado em servidores de aplicativos. Portanto, se um único servidor de aplicativos ficar offline, os serviços de cálculo do Excel ainda estarão disponíveis.  
  
-   **(5)** Os bancos de dados do SQL Server usados para o conteúdo, a configuração e os bancos de dados do aplicativo. Isso inclui o banco de dados de aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O seu plano de recuperação de desastres deve incluir a camada de banco de dados.  
  
-   **(6)** Alguma forma de backup ou redundância de banco de dados do SQL Server.  
  
##  <a name="bkmk_sql_server_technologies"></a> O banco de dados do aplicativo de serviço PowerPivot e as tecnologias de disponibilidade e recuperação do SQL Server  
 Incluir o banco de dados de aplicativo de serviço [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] no planejamento de alta disponibilidade do SharePoint. O nome padrão do banco de dados é `DefaultPowerPivotServiceApplicationDB-<GUID>`. Segue um resumo das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tecnologias de disponibilidade e das recomendações quando usadas com o banco de dados [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Para obter mais informações, consulte [Opções com suporte para recuperação de desastres e alta disponibilidade para bancos de dados do SharePoint (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx).  
  
||Comentários|  
|-|--------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] em um farm para disponibilidade.|Com suporte, mas não é recomendado. A recomendação é usar o AlwaysOn em - modo de confirmação síncrona.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] em modo de confirmação síncrona|Suporte e recomendado.|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] espelhamento assíncrono ou envio de logs para outro farm para a recuperação de desastres.|Tem suporte.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] com confirmação assíncrona para a recuperação de desastres|Tem suporte|  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Envio de logs  
  
 Para obter mais informações sobre como planejar um cenário de espera a frio com [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], consulte [Recuperação de desastres do PowerPivot](https://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx).  
  
## <a name="verification"></a>Verificação  
 Para obter orientações e scripts para ajudá-lo a verificar uma [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] implantação antes e depois de um ciclo de recuperação de desastres, consulte [lista de verificação: Usar o PowerShell para verificar o PowerPivot para SharePoint](../instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_more_resources"></a> Links para mais informações  
  
-   [Opções com suporte para recuperação de desastres e alta disponibilidade para bancos de dados do SharePoint (SharePoint 2013)](https://technet.microsoft.com/library/jj841106.aspx)  
  
-   [Plano de recuperação de desastres (SharePoint Server 2010)](https://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)  
  
-   [Microsoft® SQL Server Backup para Microsoft Windows® Azure®Tool](https://www.microsoft.com/download/details.aspx?id=40740)  
  
 **Conteúdo da comunidade**  
  
-   [Gerenciar instâncias de serviço no SharePoint 2013](http://www.petri.co.il/manage-service-instances-sharepoint-2013.htm)  
  
-   [Script de backup do banco de dados SQL Server](http://megaupl0ad.net/free/backup%20database%20sql%20server%20script)  
  
  
