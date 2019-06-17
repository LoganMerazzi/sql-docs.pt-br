---
title: Diretórios virtuais são especificados (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 7d32b560-49d6-4558-b5d6-9127067f82d6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f5e0643fad0a9e554c3c89f1d1c546a7ab69534d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091073"
---
# <a name="virtual-directories-are-unspecified-upgrade-advisor"></a>Diretórios virtuais não especificados (Supervisor de Atualização)
  O Supervisor de Atualização não detectou configurações de diretório virtual para o serviço Web Servidor de Relatórios ou para o Gerenciador de Relatórios. Concluída a atualização, configure as reservas de URL do servidor de relatório usando o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 A atualização de uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui a reserva de novas URLs para o serviço Web Servidor de Relatórios e para o Gerenciador de Relatórios. O Supervisor de Atualização não detectou diretórios virtuais para o servidor de relatório ou para o Gerenciador de Relatórios da instância que será atualizada, sendo assim, o processo de atualização possui informações insuficientes para a criação de reservas de URL para o servidor de relatório atualizado. A atualização pode prosseguir, mas o servidor de relatório ou o diretório virtual do Gerenciador de Relatórios ficará indefinido após a atualização da instalação.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Concluída a atualização, use o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para definir as URLs do servidor de relatório e do Gerenciador de Relatórios. Use o Gerenciador do IIS para remover todos os diretórios virtuais que não serão mais necessários.  
  
 Para obter mais informações, consulte [configurar uma URL &#40;Configuration Manager do SSRS&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
