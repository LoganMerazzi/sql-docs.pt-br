---
title: Esta pasta de trabalho contém uma ou mais consultas que atualizam dados externos | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61056ecc8b49e7d21cd15702116da511a517ef31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208001"
---
# <a name="this-workbook-contains-one-or-more-queries-that-refresh-external-data"></a>Esta pasta de trabalho contém uma ou mais consultas que atualizam dados externos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Para pastas de trabalho do Excel que contêm dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , os Serviços do Excel mostram este aviso quando detectam informações de conexão e solicitam que você habilite ou desabilite consultas para essa pasta de trabalho.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11_md](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)]|  
|Causa|Os Serviços do Excel são configurados para avisar na atualização de dados.|  
|Texto da mensagem|Esta pasta de trabalho contém uma ou mais consultas que atualizam dados externos. Um usuário mal-intencionado pode criar uma consulta para acessar informações confidenciais e distribuí-las a outros usuários ou pode executar outras ações prejudiciais.<br /><br /> Se você confiar na origem dessa pasta de trabalho, clique em Sim para habilitar consultas a dados externos nessa pasta de trabalho. Se você não tiver certeza, clique em Não para que as alterações não sejam aplicados em sua pasta de trabalho.<br /><br /> Você deseja habilitar consultas a dados externos nesta pasta de trabalho?|  
  
## <a name="explanation"></a>Explicação  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] As pastas de trabalho contêm cadeias de conexão de dados incorporadas usadas pelo Excel para se comunicar com um servidor externo [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que carrega e calcula os dados. Quando o aviso na atualização de dados estiver habilitado, o Serviços do Excel detectará essa cadeia de conexão e avisará o usuário.  
  
 Para filtrar e dividir dados [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] na pasta de trabalho, as consultas devem ser habilitadas. Certifique-se de habilitar consultas apenas para as pastas de trabalho [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] nas quais você confia.  
  
## <a name="user-action"></a>Ação do usuário  
 Clique em **Sim** para habilitar consultas.  
  
 Você também pode alterar os parâmetros de configuração para que o aviso na atualização não ocorra mais:  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Clique em **Aplicativo dos Serviços do Excel**.  
  
3.  Clique em **Local de Arquivo Confiável**.  
  
4.  Clique em **http://** ou no local que você deseja configurar.  
  
5.  Em Dados Externos, desmarque a caixa de seleção para **Avisar na atualização de dados**.  
  
6.  Clique em **OK**.  
  
 Como alternativa, você pode criar um novo local confiável para sites que contenham pastas de trabalho do [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] e, em seguida, modificar as definições de configuração apenas para esse site. Para obter mais informações, consulte [Criar um local confiável para sites do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  
