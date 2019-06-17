---
title: Gerenciamento de servidor do SQL Server Analysis Services | Microsoft Docs
ms.date: 11/15/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a93a7ddb0af87ae15f8d793f21a008d9a4bc25c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62659472"
---
# <a name="sql-server-analysis-services-server-management"></a>Gerenciamento de servidor do SQL Server Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Para o Azure Analysis Services, consulte [gerenciar o Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-manage).

## <a name="instances"></a>Instâncias

  Uma instância de servidor do Analysis Services é uma cópia do **msmdsrv.exe** executável que é executado como um serviço de sistema operacional. Cada instância é completamente independente de outras instâncias no mesmo servidor, tendo seus próprios parâmetros de configuração, permissões, portas, contas de inicialização, armazenamento de arquivo e propriedades de modo de servidor.  
  
 Cada instância é executada como serviço Windows, Msmdsrv.exe, no contexto de segurança de uma conta de logon definida.  
  
-   O nome do serviço da instância padrão é MSSQLServerOLAPService.  
  
-   O nome de cada instância nomeada do serviço é MSOLAP$ InstanceName.  
  
> [!NOTE]  
>  Se várias instâncias estiverem instaladas, o programa de instalação também instala um serviço de redirecionamento, que é integrado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço localizador. O serviço de redirecionamento é responsável por direcionar os clientes à instância nomeada adequada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O serviço do Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre é executado no contexto de segurança da conta de Serviço Local, uma conta de usuário limitada usada pelo Windows para serviços que não acessam recursos fora do computador local.  
  
 A expressão várias instâncias significa que você pode aumentar a escala instalando várias instâncias de servidor no mesmo hardware. Para o Analysis Services em particular, isso também significa que você pode dar suporte a diferentes modos de servidor tendo várias instâncias no mesmo servidor, cada uma configurada para ser executada em um modo específico.  

## <a name="server-mode"></a>Modo do Servidor
  
 Modo de servidor é uma propriedade de servidor que determina qual armazenamento e arquitetura de memória são usados para aquela instância. Um servidor que é executado em modo Multidimensional usa a camada de gerenciamento de recurso que foi criada para bancos de dados de cubo multidimensionais e modelos de mineração de dados. Em contraste, o modo de servidor de tabela usa o mecanismo de análise in-memory VertiPaq e a compactação de dados para agregar dados conforme eles forem solicitados.  
  
 As diferenças no armazenamento e na arquitetura de memória significam que uma única instância do Analysis Services será executada em bancos de dados tabulares ou bancos de dados multidimensionais, mas não ambos. A propriedade de modo de servidor determina qual o tipo de banco de dados executado na instância.  
  
 O modo de servidor é definido durante a instalação quando você especifica o tipo de banco de dados que será executado no servidor. Para dar suporte a todos os modos disponíveis, você pode instalar várias instâncias do Analysis Services, cada uma implantada em um modo de servidor que corresponde aos projetos que você está criando.  
  
 Como regra geral, a maioria das tarefas administrativas que você deve executar não variam por modo. Como administrador de sistema do Analysis Services, você pode usar os mesmos procedimentos e scripts para gerenciar qualquer instância do Analysis Services em sua rede independentemente de como tenha sido instalado.  
  
> [!NOTE]  
>  A exceção é o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. A administração de servidor de uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sempre está dentro do contexto de um farm do SharePoint. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] difere de outros modos de servidor porque sempre é de instância única e sempre gerenciado por meio da Administração Central do SharePoint ou da Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Embora seja possível se conectar ao [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no SQL Server Management Studio ou [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], isso não é desejável. Um farm do SharePoint inclui infraestrutura que sincroniza o estado de servidor e supervisiona a disponibilidade do servidor. Usar outras ferramentas pode interferir com estas operações. Para obter mais informações sobre [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] administração de servidor, consulte [Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md).  
  
  
  
## <a name="see-also"></a>Confira também  
 [Comparando soluções tabulares e multidimensionais](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
