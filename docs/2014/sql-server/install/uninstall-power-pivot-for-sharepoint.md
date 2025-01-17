---
title: Desinstalar o PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 3941a2f0-0d0c-4d1a-8618-7a6a7751beac
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9397dd268d767fd8c4bad9056455c21b9be65398
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62989864"
---
# <a name="uninstall-powerpivot-for-sharepoint"></a>Desinstalar o PowerPivot para SharePoint
  Desinstalar uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] é uma operação de várias etapas que inclui a preparação para desinstalação, a remoção de recursos e soluções do farm e a remoção de arquivos de programas e configurações de registro.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **Neste tópico:**  
  
-   [Pré-requisitos](#prereq)  
  
-   [Etapa 1: Verificação pré-desinstalação](#bkmk_before)  
  
-   [Etapa 2: Remover recursos e soluções do SharePoint](#bkmk_remove)  
  
-   [Etapa 3: Execute a instalação do SQL Server para remover programas do computador Local](#bkmk_uninstall)  
  
-   [Etapa 4: Desinstalar o PowerPivot para SharePoint em](#bkmk_addin)  
  
-   [Etapa 5: Verificar a desinstalação](#verify)  
  
-   [Etapa 6: Verificação pós-desinstalação](#bkmk_post)  
  
##  <a name="prereq"></a> Pré-requisitos  
  
-   Você deve ser administrador de farm do SharePoint ou administrador de aplicativo de serviço para desinstalar recursos e soluções no farm.  
  
-   Você deverá ser um Administrador do Sistema do SQL Server e membro do grupo de administradores local se também estiver desinstalando o Mecanismo de Banco de Dados.  
  
-   Você deve ser um Administrador do Sistema do Analysis Services e membro do grupo administradores local para desinstalar o Analysis Services e o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
##  <a name="bkmk_before"></a> Etapa 1: Verificação pré-desinstalação  
 O acesso aos dados PowerPivot será desabilitado quando o software que oferece suporte ao processamento de consulta e dados for removido do farm. A primeira etapa é excluir preventivamente arquivos e bibliotecas que não funcionarão mais. Isso permite que você solucione dúvidas ou preocupações sobre a 'falta de dados' antes de desinstalar o software.  
  
1.  Exclua todas as pastas de trabalho, documentos e bibliotecas PowerPivot com associação a uma instalação do PowerPivot para SharePoint. Nenhuma das bibliotecas nem os documentos funcionarão depois que o software for desinstalado.  
  
    -   [Excluir uma galeria do PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Excluir uma biblioteca de feeds de dados PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
2.  Exclua pastas de trabalho do Excel ou relatórios do Reporting Services de outras bibliotecas que contenham ou façam referência a dados PowerPivot.  
  
3.  Remova qualquer web part de um painel PerformancePoint que faça referência a dados PowerPivot.  
  
4.  Revise as permissões do SharePoint nos sites e bibliotecas existentes para determinar se é necessário alterá-las. Alguns cenários de acesso a dados PowerPivot, particularmente o acesso a dados secundários por meio de uma cadeia de conexão de URL a dados PowerPivot em outra pasta de trabalho, exigem permissões de leitura, que é superior às permissões de exibição normalmente atribuídas aos usuários do SharePoint que apenas visitam um site. Se você não precisar mais de permissões de leitura, poderá reduzir as permissões de acordo.  
  
5.  Opcionalmente, interrompa os serviços e aguarde alguns dias antes de desinstalar o software. Essa etapa não é necessária na desinstalação, mas ela oferece a opção de retomar temporariamente o serviço, enquanto você tenta resolver problemas de migração de dados ou substituição de tecnologia que possam ter passado despercebidos.  
  
##  <a name="bkmk_remove"></a> Etapa 2: Remover recursos e soluções do SharePoint  
 Use a Ferramenta de Configuração do PowerPivot para remover os serviços e aplicativos PowerPivot do SharePoint.  
  
-   Você deve ser um administrador de farm, um administrador do servidor na instância do Analysis Services e um **db_owner** no banco de dados de configuração do farm.  
  
-   Use a versão apropriada da ferramenta de configuração para a versão do SharePoint. Não use a ferramenta com instalações do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
-   Verifique se o serviço Administração do SharePoint está em execução.  
  
1.  **Execute a ferramenta de configuração:** Observe que as ferramentas de configuração são listadas somente quando [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] está instalado no servidor local. Sobre o **iniciar** , aponte para **todos os programas**, clique em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], clique em **ferramentas de configuração**e, em seguida, clique em um dos seguintes:  
  
    -   **PowerPivot para SharePoint 2013**  
  
    -   **Ferramenta de configuração do PowerPivot**  
  
2.  Selecione **Remover Recursos, Serviços, Aplicativos e Soluções** e clique em **OK**.  
  
3.  Opcionalmente, expanda a janela para o tamanho total. Você verá uma barra de botões na parte inferior da janela que inclui os comandos **Validar**, **Executar**e **Sair** .  
  
4.  Revise cada ação da lista de tarefas para entender o que faz cada uma delas.  
  
     Em **Remover Aplicativos de Serviço PowerPivot**, você tem a opção de excluir dados associados ao aplicativo de serviço. Os dados do aplicativo são um banco de dados do SQL Server que foi criado com o aplicativo de serviço com a finalidade de armazenar agendas de atualização de dados, informações de instância de banco de dados, dados de uso e outros dados usados pelo PowerPivot para SharePoint. Ele não armazena arquivos de usuário, como pastas de trabalho PowerPivot. A menos que você tenha uma razão específica para manter os dados do aplicativo (por exemplo, se você tiver políticas de retenção de dados relacionadas à atualização de dados ou ao acesso aos dados), você poderá excluir o banco de dados do aplicativo sem remover nenhum arquivo criado ou salvo por usuários do SharePoint.  
  
     Para excluir o banco de dados, selecione **Remover Aplicativos de Serviço PowerPivot** e selecione **Exclua dados de aplicativo associados a este aplicativo de serviço**.  
  
5.  Opcionalmente, revise as informações detalhadas na guia **Saída** ou na guia **Script** .  
  
     A guia Saída é um resumo das ações que serão executadas pela ferramenta. Essas informações são salvas em arquivos de log em:  
  
     `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`  
  
     A guia Script mostra os cmdlets PowerShell ou referencia os arquivos de script PowerShell que serão executados pela ferramenta.  
  
6.  Clique em **Validar** para verificar se cada ação é válida. Se **Validar** não estiver disponível, isso indicará que todas as ações são válidas para o sistema.  
  
7.  Clique em **Executar** para executar todas as ações válidas para esta tarefa. **Executar** estará disponível apenas depois que a verificação da validação tiver sido aprovada. Quando você clica em **Executar**, o seguinte aviso é exibido, lembrando a você que as ações são processadas em modo de lote: "Todas as definições de configuração sinalizadas como válidas na ferramenta serão aplicadas ao farm do SharePoint. Deseja continuar?"  
  
8.  Clique em **Sim** para continuar.  
  
 **Solucionando erros:**  
  
 Na ferramenta de configuração, você pode exibir informações de erro no painel Parâmetros de cada ação. Para problemas relacionados à implantação ou retração da solução, verifique se o serviço Administração do SharePoint foi iniciado. Esse serviço executa os trabalhos de timer que disparam alterações na configuração em um farm. Se o serviço não estiver em execução, a implantação ou a retração da solução apresentará falha. Erros persistentes indicam que um trabalho de implantação ou retração existente já está na fila e bloqueando ação adicional da ferramenta de configuração. Você pode usar o seguinte comando do PowerShell para verificar se o serviço está sendo executado.  
  
```  
Get-Service | where {$_.displayname -like "*sharepoint* administration*"}  
```  
  
 Para localizar e remover um trabalho de implantação ou retração que já esteja na fila, proceda da seguinte maneira:  
  
1.  Para todos os outros erros, verifique os logs ULS. Para obter mais informações, consulte [configurar e exibir arquivos de Log do SharePoint e log de diagnóstico &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
2.  Inicie o Shell de Gerenciamento do SharePoint como administrador e execute o comando a seguir para exibir os trabalhos na fila:  
  
    ```  
    Stsadm -o enumdeployments  
    ```  
  
3.  Examine as implantações existentes para as seguintes informações: **Tipo** é Retração ou Implantação; **Arquivo** é powerpivotwebapp.wsp ou powerpivotfarm.wsp.  
  
4.  Para implantações ou retrações relacionadas a soluções PowerPivot, copie o valor GUID **JobId** e, em seguida, cole o seguinte comando (use os comandos marcar, copiar e colar no menu Editar do Shell para copiar o GUID):  
  
    ```  
    Stsadm -o canceldeployment -id "<GUID>"  
    ```  
  
5.  Tente a tarefa novamente na ferramenta de configuração clicando em **Validar** e, em seguida, em **Executar**.  
  
 Opcionalmente, você pode usar o PowerShell para remover recursos e soluções do farm. Para obter mais informações, consulte [referência do PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).  
  
##  <a name="bkmk_uninstall"></a> Etapa 3: Execute a instalação do SQL Server para remover programas do computador Local  
 A exclusão de arquivos de programa requer que você execute a Instalação do SQL Server para desinstalar o software. A desinstalação remove os arquivos e as entradas de registro criadas pela Instalação. Você pode usar a página Programas e Recursos para desinstalar o software. Uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] faz parte de uma instalação do SQL Server.  
  
 Você pode desinstalar parte de uma instalação sem afetar outras instâncias do SQL Server (ou recursos na mesma instância) que já estejam instaladas. Por exemplo, você pode desinstalar o PowerPivot para SharePoint e manter outros componentes, como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou Mecanismo de Banco de Dados, instalados.  
  
1.  Selecione **Microsoft SQL Server 2014 (64 bits)** na lista de programas.  
  
2.  Clique em **Desinstalar/Alterar**.  
  
3.  Clique em **Remover**. Isso inicia a Instalação do SQL Server.  
  
     Na Instalação, você pode selecionar a instância do **PowerPivot** e as opções **Analysis Services** e **Integração com o SharePoint do Analysis Services** para remover apenas esse recurso, deixando os demais itens inalterados.  
  
##  <a name="bkmk_addin"></a> Etapa 4: Desinstalar o PowerPivot para SharePoint em  
 Se sua implantação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] tem dois ou mais servidores e você instalou o Suplemento do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , desinstale o suplemento do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] de cada servidor em que ele foi instalado para desinstalar completamente todos os arquivos do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Para obter mais informações, consulte [instalar ou desinstalar o PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
##  <a name="verify"></a> Etapa 5: Verificar a desinstalação  
  
1.  Na Administração Central, em **Gerenciar serviços no servidor**, conecte-se ao servidor do qual você desinstalou o PowerPivot para SharePoint.  
  
2.  -   Se você desinstalou o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013, verifique se o **Serviço de Sistema PowerPivot do SQL Server** não aparece mais na lista.  
  
    -   Se você desinstalou o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010, verifique se o **SQL Server Analysis Services** e o **Serviço de Sistema PowerPivot do SQL Server** não aparecem mais na lista.  
  
3.  Depois de desinstalar o último servidor PowerPivot para SharePoint no farm, faça o seguinte:  
  
    1.  Em Gerenciamento de Aplicativos, em **Gerenciar aplicativos de serviço**, verifique se o aplicativo de serviço PowerPivot padrão não aparece mais na lista.  
  
    2.  Em Configurações do Sistema, em **Gerenciar recursos do farm**, verifique se o Recurso de Integração do PowerPivot não está mais na página. Em **Gerenciar soluções do farm**, verifique se as soluções do PowerPivot não aparecem mais na página.  
  
    3.  Em Monitoração, em **Configurar log de diagnóstico** e em **Configurar uso e coleta de dados de integridade**, verifique se os eventos e as categorias de evento do PowerPivot não aparecem mais.  
  
    4.  Em Configurações Gerais do Aplicativo, verifique se o **Painel de Gerenciamento PowerPivot** não está mais na página.  
  
##  <a name="bkmk_post"></a> Etapa 6: Verificação pós-desinstalação  
 Use a lista a seguir para remover o software e os arquivos que não foram excluídos durante a desinstalação.  
  
1.  Exclua todos os arquivos de dados e as subpastas de `C:\Program Files\Microsoft SQL Server\MSAS12.PowerPivot`e depois exclua a pasta. Essa etapa também exclui arquivos armazenados em cache anteriormente no diretório DATA.  
  
2.  Exclua todas as pastas de trabalho, documentos e bibliotecas PowerPivot caso ainda não o tenha feito.  
  
    -   [Excluir uma galeria do PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Excluir uma biblioteca de feeds de dados PowerPivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
3.  No Serviço de Repositório Seguro, exclua os aplicativos de destino que contêm credenciais armazenadas usadas pelo PowerPivot para SharePoint. Algumas entradas, mas não todas, no Serviço de Repositório Seguro são excluídas quando você desinstala o PowerPivot para SharePoint. Os aplicativos de destino criados para a conta de atualização de dados autônoma do PowerPivot, além dos aplicativos de destino criados para atualização de dados, ainda existem e devem ser excluídos manualmente.  
  
     Por outro lado, os aplicativos de destino individuais que foram gerados automaticamente pelo Serviço de Sistema PowerPivot serão excluídos automaticamente quando o PowerPivot for desinstalado.  
  
4.  No Painel de Controle, clique em **Programas**e em **Desinstalar um programa** . Desinstale qualquer biblioteca cliente do Analysis Services que não estiver mais sendo usada. O Analysis Services ADOMD.NET e os Objetos de Gerenciamento de Análise do Microsoft SQL Server não são removidos quando você desinstala o PowerPivot para SharePoint. Como as bibliotecas podem ser usadas por outro programa que utiliza dados do Analysis Services, a Instalação do SQL Server não as desinstala automaticamente. Você deverá desinstalar essas bibliotecas de cliente individualmente se não precisar mais delas.  
  
     Não desinstale o Suplemento do SQL Server Reporting Services SharePoint 2010 a menos que esteja seguindo instruções de solução de problemas ou de instalação que o instruem especificamente a desinstalá-lo. O Suplemento Reporting Services é usado pelo Access Services. É instalado pela ferramenta Preparação de Produtos do SharePoint 2010 e deve permanecer no sistema para oferecer suporte à funcionalidade exigida pelo SharePoint.  
  
     Não instale o provedor OLE DB do Analysis Services. O SharePoint instala o provedor OLE DB como pré-requisito para as pastas de trabalho do Excel que se conectam a bancos de dados do Analysis Services. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] instala uma versão mais recente, mas essa versão é compatível com versões anteriores para você deixar o sistema encarregado de evitar problemas com conexão de dados mais tarde.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar ou desinstalar o PowerPivot para SharePoint Add-in &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Ferramentas de Configuração do PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
  
