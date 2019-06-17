---
title: Instalar o Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0904dc53e17ed140310df38d1f63dc9fe3fc45cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63054281"
---
# <a name="install-sql-server-analysis-services"></a>Instalar o SQL Server Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  SQL Server Analysis Services é um servidor de banco de dados analítico que hospeda modelos de tabela, cubos multidimensionais e modelos de mineração de dados que você pode acessar de relatórios, planilhas e painéis.  
  
 Analysis Services tem várias instâncias, o que significa que você pode instalar mais de uma cópia em um único computador ou executar versões novas e antigas lado a lado. Qualquer instância de que instalação é executada em um dos três modos, conforme determinado durante a instalação: Multidimensional e mineração, tabela de dados, ou o SharePoint. Se você quiser usar vários modos, você precisará de uma instância separada para cada um.  
  
 Depois de instalar o servidor em um modo específico, você poderá usá-lo para hospedar soluções que estejam em conformidade com esse modo. Por exemplo, um servidor de modo de tabela será exigido se você desejar acesso a dados de modelo de tabela pela rede.  
  
## <a name="get-tools-and-designers"></a>Obter ferramentas e designers  
 A Instalação do SQL Server não instala mais as ferramentas de gerenciamento ou designers de modelo usados para design de soluções ou administração de servidor. Nesta versão, as ferramentas têm uma instalação separada, que você pode obter por meio dos links a seguir:  
  
-   [Baixar o SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md)  
  
-   [Baixar o SQL Server Data Tools (SSDT)](../../../ssdt/download-sql-server-data-tools-ssdt.md)  
  
 Você precisará SSMS e SSDT para trabalhar com dados e instâncias do Analysis Services. As ferramentas podem ser instaladas em qualquer lugar, mas não se esqueça de configurar portas no servidor antes de tentar uma conexão. Veja [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) para obter detalhes.  
  
## <a name="install-using-a-wizard"></a>Instalar usando um assistente  
 A lista a seguir mostra a você quais páginas no assistente de Instalação do SQL Server são usadas para instalar o Analysis Services.  
  
1.  Selecione o **Analysis Services** na Árvore de Recursos na Instalação.  
  
     ![Árvore de recursos de instalação mostrando o Analysis Services](../../../analysis-services/instances/install-windows/media/ssas-setupas.gif "árvore de recursos de instalação mostrando o Analysis Services")  
  
2.  Na página de configuração do Analysis Services, selecione um modo. Modo de tabela é o padrão...  
  
     ![Página de configuração com as opções de configuração do Analysis Services](../../../analysis-services/instances/install-windows/media/ssas-setupasconfig.png "página de configuração com as opções de configuração do Analysis Services")  
  
  O modo tabular usa o mecanismo de análise na memória xVelocity (VertiPaq), que é o armazenamento padrão para modelos de tabela. Depois de implantar modelos de tabela para o servidor, você pode configurar seletivamente soluções tabulares para usar o armazenamento em disco DirectQuery como uma alternativa ao armazenamento associado à memória.  
 
 Multidimensional e mineração de dados de modo use MOLAP como o armazenamento padrão para modelos implantados no Analysis Services. Depois de implantar para o servidor, você pode configurar uma solução para usar o ROLAP para executar consultas diretamente no banco de dados relacional, em vez de armazenar dados de consulta em um banco de dados multidimensional do Analysis Services.  
  

  
 O gerenciamento de memória e as configurações de E/S podem ser ajustados para obter um melhor desempenho ao usar modos de armazenamento não padrão. Veja [Propriedades do servidor do Analysis Services](../../../analysis-services/server-properties/server-properties-in-analysis-services.md) para obter mais informações.  
  
## <a name="command-line-setup"></a>Instalação de Linha de Comando  
 A Instalação do SQL Server inclui um parâmetro (**ASSERVERMODE**) que especifica o modo do servidor. O exemplo a seguir ilustra a instalação de linha de comando que instala o Analysis Services no modo de servidor Tabular.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS /ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 **INSTANCENAME** deve ter menos de 17 caracteres.  
  
 Todos os valores de conta de espaço reservado devem ser substituídos por contas e senhas válidas.  
  
 **ASSERVERMODE** diferencia maiúsculas de minúsculas.  Todos os valores devem ser expressos em maiúsculas. A tabela a seguir descreve os valores válidos para **ASSERVERMODE**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|TABULAR|Este é o valor padrão. Se você não definir **ASSERVERMODE**, o servidor está instalado no modo de tabela.|
|MULTIDIMENSIONAL|Esse valor é opcional.|  
|POWERPIVOT|Esse valor é opcional. Na prática, se você configura o parâmetro **ROLE** , o modo de servidor é automaticamente definido como 1, tornando **ASSERVERMODE** opcional para um [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para uma instalação do SharePoint. Para obter mais informações, veja [Instalar Power Pivot por meio do Prompt de Comando](http://msdn.microsoft.com/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328).|  
  
  
## <a name="see-also"></a>Consulte também  
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Modelagem de tabela](https://msdn.microsoft.com/library/hh212945(v=sql.110).aspx)  
  
  
