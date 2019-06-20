---
title: Instalar ou desinstalar o Power Pivot para o suplemento SharePoint (SharePoint 2016) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4a3fba818dbedfe7d21f3b3a9527ed3b83f085ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63055110"
---
# <a name="install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016"></a>Instalar ou desinstalar o suplemento do Power Pivot para SharePoint (SharePoint 2016)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] é uma coleção de componentes de servidor de aplicativos e serviços back-end que fornece acesso a dados do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do [!INCLUDE[SPS2016](../../../includes/sps2016-md.md)] . O suplemento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint (**spPowerpivot16.msi**) é um pacote de instalação usado para instalar os componentes do servidor de aplicativos.  
  
 **Observação:** Este tópico descreve a instalação do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] arquivos de solução e [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para a ferramenta de configuração do SharePoint 2016. Após a instalação, confira o tópico [Configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md) para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
 Para obter informações sobre como baixar o **spPowerPivot16.msi**, consulte o [Microsoft® SQL Server® 2016 Power Pivot® para Microsoft SharePoint®](https://www.microsoft.com/download/details.aspx?id=52675).  
  
##  <a name="bkmk_background"></a> Plano de fundo  
  
-   **Servidor de aplicativos:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] a funcionalidade no SharePoint 2016 inclui uso de pastas de trabalho como uma fonte de dados, atualização de dados agendada, e o Painel de gerenciamento do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] é um pacote do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Installer (**spPowerpivot16.msi**) que implanta bibliotecas de cliente do Analysis Services e copia os arquivos de instalação do [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] no computador. O instalador não implanta nem configura recursos do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no SharePoint. Os seguintes componentes são instalados por padrão:  
  
    -   [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]para obter informações sobre a ferramenta de configuração e recursos adicionais. Esse componente inclui scripts do PowerShell (arquivos .ps1), pacotes da solução SharePoint (.wsp), e a ferramenta de configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] para implantar o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] em um farm do SharePoint 2016.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Provedor OLE DB para Analysis Services (MSOLAP).  
  
    -   Provedor de dados ADOMD.NET.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Serviços de back-end:** Se você usar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel para criar pastas de trabalho que contêm dados analíticos, você deve ter o Office Online Server configurada com um servidor BI que executa [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modo para acessar esses dados em um ambiente de servidor. Você pode executar a Instalação do SQL Server em um computador que tenha o SharePoint Server 2016 instalado, ou em um computador diferente que não tenha software SharePoint. O Analysis Services não tem nenhuma dependência no SharePoint.  
  
     Para obter mais informações sobre como instalar, desinstalar e configurar serviços de back-end, consulte o seguinte:  
  
    -   [Instale o Analysis Services no modo do Power Pivot.](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [Desinstalar o Power Pivot para SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> Onde instalar o spPowerPivot16.msi?  
 Uma prática recomendada é instalar o **spPowerPivot16.msi** em todos os servidores de farm do SharePoint para verificar a consistência da configuração, inclusive servidores de aplicativo e servidores front-end da Web. O pacote de instalador inclui os provedores de dados do Analysis Services, bem como a ferramenta configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] . Ao instalar o **spPowerPivot16.msi** , você pode personalizar a instalação excluindo componentes individuais.  
  
 **Provedores de dados:** Tecnologias de vários SharePoint e SQL Server usam os provedores de dados do Analysis Services incluem Serviços PerformancePoint e Power View. A instalação do **spPowerPivot16.ms** em todos os servidores do SharePoint assegura que o conjunto completo de provedores de dados do Analysis Services e a conectividade do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] estejam consistentemente disponíveis no farm.  
  
> [!NOTE]  
>  Você deve instalar os provedores de dados do Analysis Services em um servidor do SharePoint 2016 que esteja usando o **spPowerPivot16.msi**. Outros pacotes de instalação disponíveis no Feature Pack do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] não têm suporte porque esses pacotes não incluem o arquivos de suporte do SharePoint 2016 exigidos pelos provedores de dados nesse ambiente.  
  
 **Ferramenta de configuração:** O [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] ferramenta de configuração é necessária somente em um dos servidores do SharePoint. No entanto, uma prática recomendada em farms de vários servidores é instalar a ferramenta de configuração em pelo menos dois servidores, para que você tem acesso à ferramenta de configuração caso um dos dois servidores esteja offline.  
  
##  <a name="bkmk_prereq"></a> Requisitos e pré-requisitos  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2016.  
  
-   O**spPowerPivot16.msi** é de 64 bits somente, de acordo com os requisitos de produtos e tecnologias do SharePoint.  
  
-   Um servidor no [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modo. O Servidor do Office Online usará a instância do SQL Server Analysis Services como um servidor do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . O Analysis Services pode ser executado no servidor SharePoint local ou em um computador remoto. Ele não pode ser instalado no Servidor do Office Online.  
  
-   **Permissões:** Para instalar o [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)], o usuário atual deve ser um administrador no computador e no grupo de administradores de Farm do SharePoint.  
  
-   Para obter mais informações sobre os requisitos e pré-requisitos do [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] , vá para [Requisitos de hardware e software para o servidor do Analysis Services no Modo do SharePoint](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f).  
  
##  <a name="bkmk_install"></a> Para instalar o Power Pivot para SharePoint  
 O pacote de instalação do **spPowerpivot16.msi** dá suporte a uma interface gráfica do usuário e a um modo de linha de comando. Ambos os métodos de instalação requerem a execução do .msi com privilégios de administrador. Após a instalação, confira o tópico [Configurar o PowerPivot e implantar soluções &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md) para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
### <a name="user-interface-installation"></a>Instalação da interface do usuário  
 Para instalar o [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] com a interface gráfica do usuário, conclua as seguintes etapas:  
  
1.  Execute o **spPowerPivot16.msi**.  
  
2.  Selecione **Avançar** na página de boas-vindas.  
  
3.  Revise e aceite o contrato de licença, e selecione **Avançar**.  
  
4.  Na página **Seleção de Recursos** , todos os recursos são selecionados por padrão.  
  
5.  Selecione **Avançar**.  
  
6.  Selecione **Instalar** para concluir a instalação.  
  
### <a name="command-line-installation"></a>Instalação na linha de comando  
 Para uma instalação em linha de comando, abra um prompt de comando com permissões administrativas e execute o **spPowerPivot16.msi**. Por exemplo:  
  
 `Msiexec.exe /i spPowerPivot16.msi`para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
 Para criar um log de instalação, use as opções de log MsiExec padrão. O exemplo a seguir cria o arquivo de log "Install_log" usando a opção de registro em log detalhado "v".  
  
```  
Msiexec.exe /i spPowerPivot16.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>Instalação silenciosa na linha de comando para scripts  
 Você pode usar a opção **/q** ou **/quiet** para uma instalação "silenciosa" que não exibirá caixas de diálogo nem avisos. A instalação silenciosa é útil quando você deseja gerar scripts da instalação do suplemento.  
  
> [!IMPORTANT]  
>  Se você usar a opção **/q** para uma instalação de linha de comando silenciosa, o contrato de licença de usuário final não será exibido. Independentemente do método de instalação, o uso deste software é controlado por um contrato de licença e você é responsável por respeitar o contrato de licença.  
  
 **Para executar uma instalação silenciosa:**  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    Msiexec.exe /i spPowerPivot16.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>Instalação na linha de comando para incluir componentes específicos  
 A ferramenta de configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] não é necessária em todos os servidores do SharePoint. No entanto, é recomendável instalá-la pelo menos em dois servidores para que a ferramenta de configuração esteja disponível quando você precisar.  
  
 Quando você instala o spPowerPivot16.msi, pode usar as opções de linha de comando para instalar itens específicos, como os provedores de dados, e não a ferramenta de configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] . A linha de comando a seguir é um exemplo de como instalar todos os componentes exceto a ferramenta de configuração:  
  
```  
Msiexec /i spPowerPivot16.msi AGREETOLICENSE="yes" ADDLOCAL=" SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common"  
```  
  
|Opção|Descrição|  
|------------|-----------------|  
|Analysis_Server_SP_addin16|[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Configuração|  
|SQL_OLAPDM|Provedor OLE DB do Analysis Services para SQL Server 2016|  
|SQL_ADOMD|Provedor ADOMD.NET|  
|SQL_AMO|Provedor de AMO (Objetos de Gerenciamento de Análise) do SQL Server 2016.|  
|SQLAS_SP16_Common|Componentes comuns do Analysis Services para SharePoint 2016|  
  
##  <a name="bkmk_deploy_solution"></a> Implantar os arquivos de solução do SharePoint com a ferramenta de configuração do Power Pivot para SharePoint 2016  
 Três dos arquivos copiados no disco rígido pelo spPowerPivot16.msi são arquivos da solução SharePoint. O escopo de um arquivo de solução é o nível do aplicativo Web, enquanto o escopo do outros arquivos é o nível do farm. Os arquivos são os seguintes:  
  
-   `PowerPivot16FarmSolution.wsp`  

-   `PowerPivot16WebApplicationSolution.wsp`  
  
 Os arquivos de solução do são copiados para a seguinte pasta:  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Após a instalação do .msi, execute a Ferramenta de Configuração do [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] para configurar e implantar as soluções no farm do SharePoint.  
  
 **Para iniciar a ferramenta de configuração:**  
  
 No menu Iniciar do Windows do tela, digite "power" e nos resultados da pesquisa de aplicativos, selecione  **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] configuração**. Observe que os resultados da pesquisa podem incluir dois links pois a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala ferramentas de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] separadas para o SharePoint 2013 e o SharePoint 2016. Certifique-se de iniciar a ferramenta de configuração [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] .  
  
 ![PowerPivot para SharePoint 2016](../../../analysis-services/instances/install-windows/media/powerpivot-for-sharepoint-2016-configuration.png "configuração PowerPivot para SharePoint 2016")  
  
 **Or**  
  
1.  Vá para **Iniciar**, **Todos os Programas**.  
  
2.  Selecione [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)].  
  
3.  Selecione **Ferramentas de Configuração**.  
  
4.  Selecione **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Configuração**.  
  
 Para obter mais informações sobre a ferramenta de configuração, consulte [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a> Desinstalar ou reparar o suplemento  
  
> [!CAUTION]  
>  Se você desinstalar o **spPowerPivot16.msi** , os provedores de dados e a ferramenta de configuração serão desinstalados. A desinstalação dos provedores de dados fará com que o servidor não consiga se conectar ao [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)].  
  
 Você pode desinstalar ou reparar o [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] usando um dos seguintes métodos:  
  
1.  **Painel de controle do Windows:** Selecione [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]** . Selecione **Desinstalar** ou **Reparar**.  
  
2.  Execute o spPowerPivot16.msi e selecione a opção **Remover** ou **Reparar** .  
  
 **Linha de comando:** Para reparar ou desinstalar [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] usando a linha de comando, abra um prompt de comando **com permissões de administrador** e execute um dos seguintes comandos:  
  
-   Para reparar, execute o seguinte comando:  
  
    ```  
    msiexec.exe /f spPowerPivot16.msi  
    ```  
  
 OU  
  
-   Para desinstalar, execute o seguinte comando:  
  
    ```  
    msiexec.exe /uninstall spPowerPivot16.msi  
    ```  
  
  
