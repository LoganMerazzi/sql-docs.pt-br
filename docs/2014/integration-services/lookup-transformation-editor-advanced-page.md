---
title: Editor de transformação de pesquisa (página Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: f3395c65-0320-47f9-8d83-daaa082d8713
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2ec8ac0bbb56282474bde4e399eaf1d32b0e1996
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767338"
---
# <a name="lookup-transformation-editor-advanced-page"></a>Editor da Transformação Pesquisa (página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor da Transformação Pesquisa** para configurar o cache parcial e para modificar a instrução SQL da transformação Pesquisa.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 **Tamanho de cache (32 bits)**  
 Ajuste o tamanho de cache (em megabytes) para computadores de 32 bits. O valor padrão é 5 megabytes.  
  
 **Tamanho de cache (64 bits)**  
 Ajuste o tamanho de cache (em megabytes) para computadores de 64 bits. O valor padrão é 5 megabytes.  
  
 **Ativar cache para linhas com entradas sem-correspondência**  
 Linhas de cache com entradas sem-correspondência no conjunto de dados de referência.  
  
 **Alocação de cache**  
 Especifique o percentual de cache a ser alocado para as linhas com entradas sem-correspondência no conjunto de dados de referência.  
  
 **Modificar instrução SQL**  
 Modifique a instrução SQL usada para gerar o conjunto de dados de referência.  
  
> [!NOTE]  
>  A instrução SQL opcional especificada nesta página substituirá o nome da tabela especificado na página **Conexão** do **Editor da Transformação Pesquisa**. Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;Página Conexão&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md).  
  
 **Definir Parâmetros**  
 Mapeie colunas de entrada para parâmetros usando a caixa de diálogo **Definir Parâmetros da Consulta** .  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [Lookup cache modes](https://go.microsoft.com/fwlink/?LinkId=219518) (em inglês) em blogs.msdn.com  
  
## <a name="see-also"></a>Consulte também  
 [Editor de Transformação Pesquisa &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de Transformação Pesquisa &#40;Página Conexão&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Editor de Transformação Pesquisa &#40;Guia Colunas&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Editor de Transformação Pesquisa &#40;Página Saída de Erro&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Transformação Pesquisa Difusa](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
