---
title: Estender pacotes com scripts | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SQL Server Integration Services, scripting
- SSIS, scripting
- scripts [Integration Services], about scripting
ms.assetid: 67fe18ef-f3aa-41d4-9b9d-5defd4618c4b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 08953ebc12d19ab7a91cc187b579b9313a385f3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62894750"
---
# <a name="extending-packages-with-scripting"></a>Estendendo pacotes com scripts
  Se você considerar que os componentes internos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não atendem às suas necessidades, poderá ampliar a capacidade do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] codificando suas próprias extensões. Há duas opções distintas para estender seus pacotes: você pode escrever código dentro dos wrappers avançados fornecidos pela tarefa e o componente Script, ou pode criar extensões personalizadas do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a partir do zero com a derivação das classes base fornecidas pelo modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Essa seção explora a opção mais simples das duas – a extensão de pacotes com scripts.  
  
 A tarefa e o componente Script permitem estender os fluxos de controle e de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com pouquíssima codificação. Os dois objetos usam o ambiente de desenvolvimento VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications) e a linguagem de programação [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e se beneficiam de toda a funcionalidade oferecida pela biblioteca de classes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], bem como assemblies personalizados. A tarefa Script e o componente Script permitem ao desenvolvedor criar a funcionalidade personalizada sem precisar escrever todo o código de infraestrutura que costuma ser requerido no desenvolvimento de uma tarefa personalizada ou componente de fluxo de dados personalizado.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Comparar a tarefa Script e o componente de Script](../extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
 Discute as semelhanças e diferenças entre a tarefa Script e o componente Script.  
  
 [Comparar soluções de script e objetos personalizados](comparing-scripting-solutions-and-custom-objects.md)  
 Discute os critérios a serem usados na escolha entre uma solução de script e o desenvolvimento de um objeto personalizado.  
  
 [Referenciar outros assemblies em soluções de script](referencing-other-assemblies-in-scripting-solutions.md)  
 Discute as etapas requeridas para referenciar e usar assemblies e namespaces externos em um projeto de script.  
  
 [Estender o pacote com a tarefa Script](../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)  
 Discute como criar tarefas personalizadas usando a tarefa Script. Uma tarefa costuma ser chamada uma vez para cada execução de pacote ou uma vez para cada fonte de dados aberta por um pacote.  
  
 [Estender o fluxo de dados com o componente de Script](data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
 Discute como criar origens, transformações e destinos dos fluxos de dados personalizados através do componente Script. Em geral, um componente de fluxo de dados é chamado uma vez para cada linha de dados processada.  
  
## <a name="reference"></a>Referência  
 [Referência de mensagens e erros do Integration Services](../integration-services-error-and-message-reference.md)  
 Lista os códigos de erro predefinidos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com seus nomes simbólicos e descrições.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Estendendo pacotes com objetos personalizados](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Discute como criar tarefas personalizadas de programa, componentes de fluxo de dados e outros objetos de pacote para uso em vários pacotes.  
  
 [Compilar Pacotes Programaticamente](../building-packages-programmatically/building-packages-programmatically.md)  
 Descreve como criar, configurar, executar, carregar, salvar e gerenciar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] programaticamente.  
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da [!INCLUDE[msCoName](../../includes/msconame-md.md)], bem como as soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
