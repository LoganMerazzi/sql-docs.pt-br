---
title: Referenciar outros assemblies em soluções de script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a6f942e1afe40467e331519f276b360f87f9a6da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62894730"
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Referenciando outros assemblies em soluções de script
  A biblioteca de classes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] oferece ao desenvolvedor de scripts um conjunto avançado de ferramentas para implementar uma funcionalidade personalizada em pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A tarefa Script e o componente Script também podem usar assemblies gerenciados personalizados.  
  
> [!NOTE]  
>  Para permitir que seus pacotes utilizem os objetos e métodos de um serviço Web, utilize o comando **Adicionar Referência Web** disponível em VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications). Em versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você teve que gerar uma classe proxy para usar um serviço Web.  
  
## <a name="using-a-managed-assembly"></a>Usando um assembly gerenciado  
 Para que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] localize um assembly gerenciado em tempo de design, você deve seguir as seguintes etapas:  
  
1.  Armazene o assembly gerenciado em qualquer pasta de seu computador.  
  
    > [!NOTE]  
    >  Em versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], só era possível adicionar uma referência a um assembly gerenciado que estivesse armazenado na pasta %windir%\Microsoft.NET\Framework\vx.x.xxxxx ou na pasta %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies.  
  
2.  Adicione uma referência ao assembly gerenciado.  
  
     Para adicionar a referência, no VSTA, na caixa de diálogo **Adicionar Referência**, na guia **Procurar**, localize e adicione o assembly gerenciado.  
  
 Para que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] encontre o assembly gerenciado em tempo de execução, você deve seguir as seguintes etapas:  
  
1.  Assine o assembly gerenciado com um nome forte.  
  
2.  Instale o assembly no cache de assembly global do computador no qual o pacote é executado.  
  
     Para obter mais informações, consulte [Compilar, implantar e depurar objetos personalizados](../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Usando a biblioteca de classes do Microsoft .NET Framework  
 A tarefa Script e o componente Script podem levar vantagem sobre todos os outros objetos e funcionalidades expostos pela biblioteca de classes [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Por exemplo, usando o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], você pode recuperar informações sobre seu ambiente e pode interagir com o computador que está executando o pacote.  
  
 Esta lista descreve várias das classes [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] usadas com mais frequência:  
  
-   `System.Data` Contém arquitetura ADO.NET.  
  
-   `System.IO` Fornece uma interface para o sistema de arquivos e fluxos.  
  
-   `System.Windows.Forms` Fornece a criação de formulários.  
  
-   `System.Text.RegularExpressions` Fornece classes para trabalhar com expressões regulares.  
  
-   `System.Environment` Retorna informações sobre o computador local, o usuário atual e as configurações de computador e usuário.  
  
-   `System.Net` Oferece comunicações de rede.  
  
-   `System.DirectoryServices` Expõe o Active Directory.  
  
-   `System.Drawing` Fornece bibliotecas de manipulação de imagens extensivos.  
  
-   `System.Threading` Habilita a programação multithreaded.  
  
 Para obter mais informações sobre o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consulte a Biblioteca MSDN.  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Estender pacotes com scripts](extending-packages-with-scripting.md)  
  
  
