---
title: Configuração dinâmica usando o Windows PowerShell de energia | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e290e0e15797a8b84a6d52c945a5fd78458515fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208200"
---
# <a name="power-pivot-configuration-using-windows-powershell"></a>Configuração do Power Pivot usando o Windows PowerShell
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui cmdlets do Windows PowerShell que você pode usar para configurar uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. A configuração completa de uma instalação com o PowerShell requer o uso de cmdlets do SharePoint e do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para os cmdlets do SharePoint. A maior parte da configuração pode ser concluída usando uma das ferramentas do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obter mais informações sobre as ferramentas, consulte [Power Pivot Configuration Tools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
> [!IMPORTANT]  
>  Para um farm do SharePoint 2010, o SharePoint 2010 SP1 deve ser instalado antes da configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint ou de um farm do SharePoint que usa um servidor do banco de dados do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] . Se você ainda não instalou o service pack; instale-o antes de começar a configurar o servidor.  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-powershell"></a>Benefícios da Configuração do Power Pivot para SharePoint Usando o PowerShell  
 É possível criar arquivos de script do Windows PowerShell (.ps1) para automatizar tarefas de configuração. Essa abordagem será recomendada se você precisar de instalação e etapas de configuração controladas por script que possa ser executado em qualquer servidor. Você pode precisar desse script como parte de um plano de recuperação de desastre para reconstruir um servidor no caso de um problema de hardware.  
  
## <a name="view-a-list-of-the-power-pivot-cmdlets-on-a-server"></a>Exibir uma lista de Cmdlets do Power Pivot em um Servidor  
 Para ver o conteúdo e exemplos de cmdlets do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , consulte [Referência do PowerShell para PowerPivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md).  
  
 Para usar o PowerShell para exibir uma lista de cmdlets do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] :  
  
1.  Abra um Shell de Gerenciamento do SharePoint usando a opção **Executar como Administrador** .  
  
2.  Insira o seguinte comando:  
  
    ```  
    Get-help *powerpivot*  
    ```  
  
     Você deve ver uma lista de cmdlets que incluem o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no nome do cmdlet. Por exemplo, `Get-PowerPivotServiceApplication`. O número de cmdlets disponíveis depende da versão do Analysis Services que você está usando.  
  
    -   10 cmdlets com o servidor SQL Server 2012 SP1 Analysis Services configurados no modo do SharePoint e com o SharePoint 2013. A versão 2012 SP1 utiliza uma nova arquitetura que permite ao Analysis Server ser executado fora do farm do SharePoint e exige menos cmdlets do Windows PowerShell de gerenciamento.  
  
    -   17 cmdlets com o servidor SQL Server 2012 Analysis Services configurados no modo do SharePoint e com o SharePoint 2010.  
  
     Se nenhum comando é retornado na lista ou você verá uma mensagem de erro semelhante a "`get-help could not find *powerpivot* in a help file in this session.`", consulte a próxima seção neste tópico para obter instruções sobre como habilitar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cmdlets no servidor.  
  
     Todos os cmdlets têm ajuda online. O exemplo a seguir mostra como exibir a ajuda online para o cmdlet **New-PowerPivotServiceApplication** :  
  
    ```  
    Get-help new-powerpivotserviceapplication -full  
    ```  
  
     Como alternativa, para exibir apenas os exemplos, use a sintaxe a seguir:  
  
    ```  
    Get-help new-powerpivotserviceapplication -example  
    ```  
  
## <a name="enable-power-pivot-cmdlets-on-a-server"></a>Habilitar os Cmdlets do Power Pivot em um Servidor  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] estão disponíveis depois que você instala o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint e implanta a solução de farm. As soluções são implantadas quando você executa a ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Siga estas etapas para habilitar o uso de cmdlets:  
  
1.  Abra um Shell de Gerenciamento do SharePoint usando a opção **Executar como Administrador** .  
  
2.  Execute o primeiro cmdlet:  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     O cmdlet retorna o nome da solução, sua ID de solução e Deployed=False. Na próxima etapa, você implantará a solução.  
  
3.  Execute o segundo cmdlet para implantar a solução:  
  
    ```  
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
4.  Feche a janela. Abra-a novamente usando a opção **Executar como Administrador** .  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Administração e configuração de servidor do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Power Pivot Configuration Tools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
 [Referência do PowerShell para PowerPivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)  
  
  
