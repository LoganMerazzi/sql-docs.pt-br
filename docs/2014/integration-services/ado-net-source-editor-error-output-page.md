---
title: Editor de origem do ADO NET (página saída de erro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.erroroutput.f1
ms.assetid: 4dd9d129-a95c-4d3a-bbbf-e84a39089950
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8543f1a7bd14db09873aaefb58b74efae0f3cf34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061643"
---
# <a name="ado-net-source-editor-error-output-page"></a>Editor de Origem ADO NET (Página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem ADO NET** para selecionar as opções de manipulação de erros e definir as propriedades nas colunas de saída de erros.  
  
 Para obter mais informações sobre a origem ADO NET, consulte [ADO NET Source](data-flow/ado-net-source.md).  
  
 **Para abrir a página Saída de Erro**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que tenha a origem ADO NET.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem ADO NET.  
  
3.  No **Editor de Origem ADO NET**, clique em **Saída de Erro**.  
  
## <a name="options"></a>Opções  
 **Entrada/Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exiba as colunas externas (origem) que você selecionou na página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ADO NET** .  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos relacionados:** [Tratamento de erro em dados](data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de Origem ADO NET &#40;página Gerenciador de Conexões&#41;](../../2014/integration-services/ado-net-source-editor-connection-manager-page.md)   
 [Editor de Origem ADO NET &#40;Página Colunas&#41;](../../2014/integration-services/ado-net-source-editor-columns-page.md)   
 [Gerenciador de conexões ADO.NET](connection-manager/ado-net-connection-manager.md)  
  
  
