---
title: Banco de dados de servidor de relatório não está configurado (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 38c18c948ea8c30817bdeb49b00a2334b2fd3d4a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057564"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>O banco de dados do servidor de relatório não está configurado (Supervisor de Atualização)
  A atualização está bloqueada devido a uma configuração incompleta do servidor de relatório. O banco de dados do servidor de relatório não está configurado.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 A Instalação só pode atualizar uma instância do servidor de relatório completamente configurada. Para continuar, você deve configurar o banco de dados do servidor de relatório, ou usar o Microsoft Windows **painel de controle** para remover o recurso de servidor de relatório do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação. Depois de remover o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], é possível atualizar outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Ação corretiva  
 Caso não tenha configurado o banco de dados do servidor de relatório, o servidor de relatório não estará operacional e deverá ser removido antes da atualização.  
  
 Para obter mais informações sobre como desinstalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte [desinstalar o Reporting Services 2012](https://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\)). o tópico descreve como desinstalar uma versão específica e os procedimentos são semelhantes para versões anteriores.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
