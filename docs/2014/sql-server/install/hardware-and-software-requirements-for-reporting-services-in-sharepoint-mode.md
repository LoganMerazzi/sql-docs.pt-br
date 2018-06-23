---
title: Requisitos de hardware e Software para o Reporting Services no modo do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ed91877d-4f74-4266-a932-b824b4810c99
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 6b02fd6592ce8b57900bf3c8e5558a6b3cfacc86
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116521"
---
# <a name="hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode"></a>Requisitos de hardware e software para o Reporting Services no modo do SharePoint
  Este tópico descreve os pré-requisitos, requisitos de hardware e considerações de instalação para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que é executado no modo do SharePoint. Como o modo SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requer um servidor do SharePoint, a maioria dos requisitos são baseados no ambiente do SharePoint. Para servidores de relatório no modo nativo, o seu hardware deve atender aos requisitos mínimos de hardware e software para executar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   [Pré-requisitos](#bkmk_prereq)  
  
-   [Requisitos de banco de dados do servidor de relatório](#bkmk_report_server_database)  
  
-   [Requisitos do Power View](#bkmk_powerview)  
  
-   [Mais informações](#bkmk_more_information)  
  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
  
-   Para instalações locais, a conta registrada durante a instalação do SharePoint e do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] precisa ser membro do grupo de administradores no sistema operacional local. A conta de instalação não precisa ser membro do grupo de administradores de farm do SharePoint.  
  
     Para obter mais informações, consulte [Permissões de conta e configurações de segurança no SharePoint 2013](http://technet.microsoft.com/library/cc678863.aspx).  
  
-   O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que é executado no modo do SharePoint exige o SharePoint Server. Para obter mais informações sobre os requisitos e as configurações do SharePoint, consulte o seguinte:  
  
    -   [Requisitos de hardware e software (SharePoint 2013)](http://go.microsoft.com/fwlink/p/?LinkId=256365) (http://go.microsoft.com/fwlink/p/?LinkId=256365)  
  
    -   [Gerenciamento e dimensionamento de capacidade do SharePoint Server 2013](http://technet.microsoft.com/library/cc261700.aspx)  
  
    -   [Requisitos de software para business intelligence (SharePoint 2013)](http://go.microsoft.com/fwlink/p/?LinkId=256367)  
  
    -   [Requisitos de hardware e de software (SharePoint Server 2010)](http://technet.microsoft.com/library/cc262485\(v=office.14\))  
  
    -   [Gerenciamento e dimensionamento de capacidade do SharePoint Server 2010](http://technet.microsoft.com/library/cc261700.aspx\(v=office.14\))  
  
-   Se você quiser atualizar uma instalação existente do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
-   Verifique se o serviço **Administração do SharePoint 2013** foi iniciado no Windows Server Manager.  
  
###  <a name="bkmk_report_server_database"></a> Requisitos de banco de dados do servidor de relatório  
  
-   Os produtos e as tecnologias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e do SharePoint usam bancos de dados relacionais do SQL Server para armazenar dados de aplicativo.  
  
-   O [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] requer uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] de uma edição compatível do SQL Server. Para obter mais informações sobre requisitos de hardware e software, consulte [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Os produtos do SharePoint poderão usar uma instância de banco de dados existente. Se uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não estiver instalada, a Instalação dos Produtos do SharePoint instalará o SQL Server Express Edition para os bancos de dados de aplicativo do SharePoint.  
  
-   A instância do servidor de relatório não pode usar o SQL Server Express Edition para seu banco de dados. No entanto, a instância do SQL Server Express Edition instalada pelo produto ou tecnologia do SharePoint pode existir lado a lado com outras edições do Mecanismo de Banco de Dados.  
  
##  <a name="bkmk_powerview"></a> [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] Requisitos  
 Analise a [documentação do Power View](http://office.microsoft.com/excel-help/power-view-explore-visualize-and-present-your-data-HA102835634.aspx) mais atualizada em Office.Microsoft.com. O [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] é um recurso do Microsoft Excel 2013 e faz parte do suplemento [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services para Microsoft SharePoint Server 2010 e 2013 Enterprise Editions.  
  
##  <a name="bkmk_more_information"></a> Mais informações  
 Para obter informações sobre as alterações do SharePoint, consulte [alterações do SharePoint 2010 para o SharePoint 2013](http://technet.microsoft.com/library/ff607742\(office.15\).aspx) (http://technet.microsoft.com/en-us/library/ff607742(office.15).aspx).  
  
 [Notas de Versão do SQL Server 2014](http://go.microsoft.com/fwlink/?LinkID=296445).  
  
  