---
title: Implantar projetos do Analysis Services (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- deploy [Analysis Services]
- projects [Analysis Services], deploying
- Business Intelligence Development Studio, deploying projects [Analysis Services]
ms.assetid: 29490a5b-1573-4a35-9277-10c6a6e4ef0e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5b6c79c2ea4355e9d889e235c8185a2460c0ed8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075385"
---
# <a name="deploy-analysis-services-projects-ssdt"></a>Implantar projetos do Analysis Services (SSDT)
  Durante o desenvolvimento de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você implanta com frequência o projeto em um servidor de desenvolvimento para criar o banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] definido pelo projeto. Isso é necessário para testar o projeto; por exemplo, procurar células no cubo, procurar membros da dimensão ou verificar as fórmulas dos KPIs (indicadores chave de desempenho).  
  
## <a name="deploying-a-project"></a>Implantando um projeto  
 É possível implantar um projeto independentemente ou todos os projetos da solução. Quando você implanta um projeto, ocorre uma sequência de fatos. Primeiro, o projeto é criado. Essa etapa cria os arquivos de saída que definem o banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e seus objetos constituintes. Em seguida, o servidor de destino é validado. Por fim, são criados o banco de dados de destino e seus objetos no servidor de destino. Durante a implantação, o mecanismo de implantação substitui completamente todos os bancos de dados preexistentes pelo conteúdo do projeto, exceto se esses objetos foram criados pelo projeto em uma implantação anterior.  
  
 Depois de uma implantação inicial, um arquivo Incrementalsnapshot XML é gerado no \<nome do projeto > pasta \obj. Ele é usado para determinar se o banco de dados e seus objetos no servidor de destino sofreram alterações fora do projeto. Em caso positivo, será solicitado que você substitua todos os objetos do banco de dados de destino. Se todas as alterações foram feitas dentro do projeto e ele estiver configurado para implantação incremental, somente as alterações serão implantadas no servidor de destino.  
  
 A configuração de projeto e suas configurações associadas determinam as propriedades de implantação que serão usadas para implantar o projeto. No caso de projeto compartilhado, cada desenvolvedor pode usar sua própria configuração com suas próprias opções de configuração de projeto. Por exemplo, cada desenvolvedor pode especificar um servidor de teste diferente para trabalhar isoladamente dos outros desenvolvedores.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um projeto do Analysis Services &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)  
  
  
