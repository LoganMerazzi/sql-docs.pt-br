---
title: Programação de mineração de dados do Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1b4068d012b64cb4fc5352ed11c8576a38d6d6c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65450115"
---
# <a name="data-mining-programming"></a>Programação de mineração de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

  Se você considerar que ferramentas e visualizadores internos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não atendem às suas necessidades, poderá ampliar a capacidade do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] codificando suas próprias extensões. Nessa abordagem, você tem duas opções:  
  
-   **XMLA**  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte a XML for Analysis (XMLA) como protocolo para comunicação com aplicativos cliente. Comandos adicionais têm suporte do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que estende a especificação do XML for Analysis.  
  
     Como o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa XMLA para definição de dados, manipulação de dados e suporte a controle de dados, você pode criar estruturas de mineração e modelos de mineração usando as ferramentas visuais fornecidas pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e, em seguida, estender os objetos de data mining criados usando os scripts de extensão DMX e de linguagem ASSL.  
  
     Você pode criar e pode modificar objetos de data mining completamente em scripts de XMLA e executar consultas de previsão em modelos programaticamente de seus próprios aplicativos.  
  
-   **Analysis Management Objects (AMO)**  
  
     O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também fornece uma estrutura completa que permite aos provedores de mineração de dados de terceiros integrar os seguintes objetos de mineração de dados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Você pode criar estruturas de mineração e modelos de mineração usando AMO. Consulte os seguintes exemplos em CodePlex:  
  
    -   Navegador AMO  
  
         Conecta-se à instância do SSAS especificada e lista todos os objetos de servidor e suas propriedades, incluindo estrutura de mineração e modelos de mineração.  
  
    -   Exemplo Simples de AMO  
  
         O Exemplo Simples do AS aborda o acesso programático à maioria dos objetos principais, e demonstra a navegação de metadados e o acesso aos valores em objetos.  
  
         O exemplo também demonstra como criar e processar uma estrutura e um modelo de mineração de dados, bem como navegar em um modelo de mineração de dados existente.  
  
-   **DMX**  
  
     Você pode usar DMX para encapsular instruções de comando, consultas de previsão e resultados da consulta e metadados de retorno em um formato de tabela, supondo que você tenha criado uma conexão com um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [OLE DB para mineração de dados](data-mining-programming-ole-db.md)  
 Descreve adições à especificação para dar suporte à mineração de dados e a dados multidimensionais: novos conjuntos de linhas e colunas de esquemas, linguagem DMX para criação e gerenciamento de estruturas de mineração.  
  
## <a name="related-reference"></a>Referência relacionada  
 [Desenvolvendo com ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net)  
 Apresenta objetos de programação do servidor e do cliente ADOMD.NET.  
  
 [Desenvolvendo com AMO &#40;Objetos de Gerenciamento de Análise&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)  
 Apresenta a biblioteca de programação AMO.  
  
 [Desenvolvendo com ASSL &#40;linguagem de script do Analysis Services&#41;](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)  
 Apresenta o XML for Analysis (XMLA) e suas extensões.  
  
## <a name="see-also"></a>Consulte também  
 [Documentação do desenvolvedor do Analysis Services](../analysis-services-developer-documentation.md)   
 [Referência de DMX &#40;extensões DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md)  
  
  
