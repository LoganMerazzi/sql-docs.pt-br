---
title: Converter a caixa de diálogo do modelo de implantação de pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.bids.converttolegacydeployment.f1
ms.assetid: 9e60a34a-10f7-48d1-966f-b3ff236ab4b7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 88a8d26716ed0945488fdd24ce1e19d3877e049f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829326"
---
# <a name="convert-to-package-deployment-model-dialog-box"></a>Caixa de diálogo Converter em Modelo de Implantação de Pacote
  A caixa de diálogo **Converter em Modelo de Implantação de Pacote** permite converter um pacote para o modelo de implantação de pacote depois de verificar se o projeto e cada pacote do projeto são compatíveis com esse modelo. Se um pacote usar recursos exclusivos para o modelo de implantação de projeto, como parâmetros, o pacote não poderá ser convertido.  
  
## <a name="task-list"></a>Lista de Tarefas  
 Converter um pacote para o modelo de implantação de pacote exige duas etapas.  
  
1.  Quando você seleciona o comando **Converter em Modelo de Implantação de Pacote** no menu **Project** , o projeto e cada pacote do projeto terão a compatibilidade verificada com esse modelo. Os resultados são exibidos na tabela **Resultados** .  
  
     Se o projeto ou pacote falhar no teste de compatibilidade, clique em **Falha** na coluna **Resultado** para obter mais informações. Clique em **Salvar Relatório** para salvar uma cópia destas informações em um arquivo de texto.  
  
2.  Se o projeto e todos os pacotes passarem no teste de compatibilidade, clique em **OK** para converter o pacote.  
  
> [!NOTE]  
>  Para converter um projeto no modelo de implantação de projeto, use o **Assistente de Conversão de Projeto do Integration Services**. Para obter mais informações, consulte [Integration Services Project Conversion Wizard](../../2014/integration-services/integration-services-project-conversion-wizard.md).  
  
## <a name="see-also"></a>Consulte também  
 [Implantação de projetos e pacotes](packages/deploy-integration-services-ssis-projects-and-packages.md)   
 [Implantação de pacote &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [Assistente de Conversão de Projeto do Integration Services](../../2014/integration-services/integration-services-project-conversion-wizard.md)  
  
  
