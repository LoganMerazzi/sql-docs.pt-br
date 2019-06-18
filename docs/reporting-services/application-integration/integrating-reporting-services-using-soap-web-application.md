---
title: Usando a API SOAP em um aplicativo Web | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], Web applications
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- report servers [Reporting Services], SOAP
- Web applications [Reporting Services]
ms.assetid: e8ca4455-0dc3-4741-8872-3636114938ad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 53196d1336bb7be6093b749acb93f1ad95a99852
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62741942"
---
# <a name="integrating-reporting-services-using-soap---web-application"></a>Integrando o Reporting Services usando o SOAP – aplicativo Web
  Você pode acessar a funcionalidade completa do servidor de relatório por meio da API SOAP do Reporting Services. Por ser um serviço Web, a API SOAP pode ser acessada facilmente para fornecer os recursos de relatórios corporativos para seus aplicativos comerciais personalizados. Você acessa o serviço Web do servidor de relatório a partir de um aplicativo Web da mesma forma que acessa a API SOAP de um aplicativo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], você pode gerar uma classe proxy que expõe as propriedades e os métodos do serviço Web Servidor de Relatórios e que permite usar uma infraestrutura e ferramentas conhecidas para criar aplicativos de negócios na tecnologia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 A funcionalidade de gerenciamento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é acessada no aplicativo Web tão facilmente como em um aplicativo do Windows. Em um aplicativo Web, você pode adicionar e remover itens do banco de dados do servidor de relatório, definir segurança de item, modificar itens do banco de dados do servidor de relatório, gerenciar programação e entrega e muito mais.  
  
## <a name="enabling-impersonation"></a>Habilitando a representação  
 A primeira etapa na configuração do aplicativo Web é habilitar a representação no cliente de serviço Web. Com representação, os aplicativos do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] podem ser executados com a identidade do cliente em nome dos quais estão sendo operados. O [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] conta com os Serviços de Informações da Internet (IIS) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para autenticar o usuário e passar um token autenticado para o aplicativo do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] ou, se não for possível autenticar o usuário, passar um token não autenticado. Em qualquer um dos casos, o aplicativo [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] representa qualquer token recebido, se a representação estiver habilitada. Você pode habilitar a representação no cliente, modificando o arquivo Web.config do aplicativo cliente como a seguir:  
  
```  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  A representação é desabilitada por padrão.  
  
 Para obter mais informações sobre a representação do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)], consulte a documentação do SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="managing-the-report-server-using-soap-api"></a>Gerenciando do servidor de relatório por meio da API SOAP  
 Você também pode usar seu aplicativo Web para gerenciar um servidor de relatório e seu conteúdo. O Gerenciador de Relatórios, incluído com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], é um exemplo de aplicativo Web criado completamente por meio do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] e da API SOAP do Reporting Services. Você pode adicionar a funcionalidade de gerenciamento de relatório do Gerenciador de Relatórios para seus aplicativos Web personalizados. Por exemplo, é recomendável retornar uma lista de relatórios disponíveis no banco de dados do servidor de relatório e exibi-los em um controle **Listbox** do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] para os usuários poderem escolhê-los. O código a seguir conecta-se ao banco de dados do servidor de relatório e retorna uma lista de itens no banco de dados do servidor de relatório. Os relatórios disponíveis são, em seguida, adicionados a um controle Listbox que exibe o caminho de cada relatório.  
  
```vb  
Private Sub Page_Load(sender As Object, e As System.EventArgs)  
   ' Create a Web service proxy object and set credentials  
   Dim rs As New ReportingService2005()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return a list of catalog items in the report server database  
   Dim items As CatalogItem() = rs.ListChildren("/", True)  
  
   ' For each report, display the path of the report in a Listbox  
   Dim ci As CatalogItem  
   For Each ci In  items  
      If ci.Type = ItemTypeEnum.Report Then  
         catalogListBox.Items.Add(ci.Path)  
      End If  
   Next ci  
End Sub ' Page_Load   
```  
  
```csharp  
private void Page_Load(object sender, System.EventArgs e)  
{  
   // Create a Web service proxy object and set credentials  
   ReportingService2005 rs = new ReportingService2005();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return a list of catalog items in the report server database  
   CatalogItem[] items = rs.ListChildren("/", true);  
  
   // For each report, display the path of the report in a Listbox  
   foreach(CatalogItem ci in items)  
   {  
      if (ci.Type == ItemTypeEnum.Report)  
         catalogListBox.Items.Add(ci.Path);  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Integrando o Reporting Services em aplicativos](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Usando a API SOAP em um aplicativo do Windows](../../reporting-services/application-integration/integrating-reporting-services-using-soap-windows-application.md)  
  
  
