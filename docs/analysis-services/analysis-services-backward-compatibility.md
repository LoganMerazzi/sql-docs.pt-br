---
title: Compatibilidade com versões anteriores do SQL Server 2016 Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ab4f304d865992a3269b4ee83c9e25f61069e8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210269"
---
# <a name="analysis-services-backward-compatibility-sql-server-2016"></a>Compatibilidade com versões anteriores do Analysis Services (SQL Server 2016)
[!INCLUDE[ssas-appliesto-sql2016](../includes/ssas-appliesto-sql2016.md)]

Este artigo descreve as alterações na disponibilidade de recursos e o comportamento entre a versão atual e a versão anterior.

## <a name="deprecated-features"></a>Recursos preteridos
Um *recurso preterido* será descontinuado do produto em uma versão futura, mas é ainda tem suporte e incluído na versão atual para manter a compatibilidade com versões anteriores. Recomenda-se que você interromper o uso de recursos preteridos em projetos novos e existentes para manter a compatibilidade com versões futuras.
  
Os seguintes recursos foram preteridos nessa versão:
  
|||  
|-|-|  
|**Modo/categoria**|**Recurso**|  
|Multidimensional|Partições remotas|  
|Multidimensional|Grupos de medidas vinculados remotos|  
|Multidimensional|Write-back dimensional|  
|Multidimensional|Dimensões vinculadas|   
|Multidimensional|Notificações de tabela do SQL Server para o cache pró-ativo.  <br />A substituição é usar a sondagem para o cache pró-ativo. <br />Consulte [Cache pró-ativo &#40;Dimensões&#41;](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md) e [Cache pró-ativo e &#40;Partições&#41;](../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|Multidimensional|Cubos de sessão. Não há nenhuma substituição.|  
|Multidimensional|Cubos locais. Não há nenhuma substituição.|  
|Tabular|Os níveis de compatibilidade de modelo de tabela 1100 e 1103 não terão suporte em uma versão futura. A substituição é definir modelos de nível de compatibilidade 1200 ou superior, convertendo definições de modelo para metadados tabulares. Consulte [Nível de compatibilidade para modelos de tabela no Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
|Ferramentas|SQL Server Profiler para captura de rastreamento<br /><br /> A substituição é usar o Extended Events Profiler interno no SQL Server Management Studio.  <br /> Consulte [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Ferramentas|Server Profiler para reprodução de rastreamento <br />Substituição. Não há nenhuma substituição.|  
|APIs Trace Management Objects e Trace|Objetos Microsoft.AnalysisServices.Trace (contêm as APIs para os objetos Analysis Services Trace e Replay). A substituição é composta por várias partes:<br /><br /> -Configuração de rastreamento: Microsoft.SqlServer.Management.XEvent<br />-Leitura de rastreamento: Microsoft.SqlServer.XEvent.Linq<br />-Reprodução de rastreamento: Nenhum|  
  
> [!NOTE]  
>  Os anúncios anteriores de recursos preteridos do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] permanecem em vigor. Como o código de suporte a esses recursos ainda não foi retirado do produto, muitos desses recursos ainda estão presentes nesta versão. Enquanto os recursos anteriormente preteridos possam ser acessíveis, que eles ainda são considerados preteridos e podem ser fisicamente removidos do produto a qualquer momento.  

## <a name="discontinued-features"></a>Recursos descontinuados
Um *recurso Descontinuado* foi preterido em uma versão anterior. Ele pode continuar a ser incluído na versão atual, mas não é mais suportado. Recursos descontinuados podem ser removidos inteiramente em uma futura versão ou atualizar.

Os seguintes recursos foram preteridos em uma versão anterior e não têm mais suporte nesta versão.

|||  
|-|-|  
|**Recurso**|**Substituição ou solução alternativa**|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|nenhuma. Esse recurso foi preterido no SQL Server 2005.|  
|[CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)|nenhuma. Esse recurso foi preterido no SQL Server 2005.|  
|Dica do otimizador de consulta NON_EMPTY_BEHAVIOR|nenhuma. Esse recurso foi preterido no SQL Server 2008.|  
|Assemblies COM|nenhuma. Esse recurso foi preterido no SQL Server 2008.|  
|Propriedade de célula intrínseca CELL_EVALUATION_LIST|nenhuma. Esse recurso foi preterido no SQL Server 2005.|  
  
> [!NOTE]  
>  Os anúncios anteriores de recursos preteridos do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] permanecem em vigor. Como o código de suporte a esses recursos ainda não foi retirado do produto, muitos desses recursos ainda estão presentes nesta versão. Enquanto os recursos anteriormente preteridos possam ser acessíveis, que eles ainda são considerados preteridos e podem ser fisicamente removidos do produto a qualquer momento.  

## <a name="breaking-changes"></a>Alterações significativas
Um *alteração interruptiva* faz com que um modelo de dados, código do aplicativo ou script não funcionem depois de atualizar o modelo ou o servidor.
  
### <a name="net-40-version-upgrade"></a>Atualização de Versão do .NET 4.0  
 Bibliotecas de cliente de gerenciamento de objetos AMO (Analysis Services), o ADOMD.NET e o objeto de modelo de TOM (Tabular) agora voltados para o tempo de execução do .NET 4.0. Isso pode ser uma alteração interruptiva para aplicativos destinados ao .NET 3.5. Aplicativos que usam versões mais recentes desses assemblies agora devem ser voltados para o .NET 4.0 ou posterior.  
  
### <a name="amo-version-upgrade"></a>Atualização de Versão do AMO  
 Esta versão é uma atualização de versão para [objetos de gerenciamento do Analysis Services &#40;AMO&#41; ](https://msdn.microsoft.com/library/mt436122.aspx) e é uma alteração interruptiva em determinadas circunstâncias.  O código e os scripts existentes que chamam o AMO continuarão a ser executados como antes se você efetuar a atualização a partir de uma versão anterior. No entanto, se você precisar *recompilar* seu aplicativo e tiver como alvo uma instância do SQL Server 2016 Analysis Services, você deve adicionar o namespace a seguir para tornar seu código ou script operacional:  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 O namespace [Microsoft.AnalysisServices.Core](https://msdn.microsoft.com/library/microsoft.analysisservices.core.aspx) agora é necessário sempre que a referenciar o assembly Microsoft. AnalysisServices em seu código. Objetos que estiveram anteriormente apenas no namespace do **Microsoft.AnalysisServices** são movidos para o namespace principal nesta versão, se o objeto for usado em cenários de tabela e cenários multidimensionais da mesma maneira.  Por exemplo, as APIs de servidor são realocadas para o namespace principal.  
  
 Apesar de agora haver vários namespaces, eles existem no mesmo assembly (Microsoft.AnalysisServices.dll).  
  
### <a name="xevent-discover-changes"></a>Alterações de XEvent DISCOVER  
 Para oferecer melhor suporte a streaming no SSMS para SQL Server 2016 Analysis Services, de XEvent DISCOVER `DISCOVER_XEVENT_TRACE_DEFINITION` é substituído pelo seguintes rastreamentos XEvent:  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  

## <a name="behavior-changes"></a>Alterações de comportamento
Uma *alteração de comportamento* afeta a maneira como os recursos funcionam ou interagem na versão atual em comparação com as versões anteriores do SQL Server.
  
Revisões de valores padrão, a configuração manual necessária para concluir uma atualização ou restaurar a funcionalidade, ou então uma nova implementação de um recurso existente são exemplos de uma alteração de comportamento no produto.
  
Os comportamentos de recursos alterados nesta versão, mas que não interrompem um modelo ou código existente após a atualização, estão listados aqui.
  
### <a name="analysis-services-in-sharepoint-mode"></a>Analysis Services no modo do SharePoint
 Não é mais necessário executar o assistente de Configuração do Power Pivot como uma tarefa pós-instalação. Isso é verdadeiro para todas as versões com suporte do SharePoint que carregam modelos do SQL Server 2016 Analysis Services atual.
  
### <a name="directquery-mode-for-tabular-models"></a>Modo DirectQuery para modelos de tabela
 *DirectQuery* é um modo de acesso a dados para modelos de tabela, em que a execução da consulta é executada em um banco de dados relacional de back-end, recuperando um conjunto de resultados em tempo real. Ele geralmente é usado para grandes conjuntos de dados que não cabem na memória ou quando dados são voláteis e você deseja os dados mais recentes retornados em consultas a um modelo de tabela.
  
 O DirectQuery já existe como um modo de acesso a dados em várias versões mais recentes. No SQL Server 2016 Analysis Services, a implementação foi ligeiramente revisada, supondo que o modelo de tabela está no nível de compatibilidade 1200 ou superior. DirectQuery tem menos restrições do que antes. Ele também tem propriedades de banco de dados diferentes.
  
 Se você estiver usando DirectQuery em um modelo de tabela existente, você poderá manter o modelo em seu nível de compatibilidade atual, 1100 ou 1103, e continuar a usar o DirectQuery, já que ele está implementado para esses níveis. Como alternativa, você pode atualizar para 1200 ou superior para se beneficiar de aprimoramentos feitos ao DirectQuery.
  
 Não há nenhuma atualização in-loco de um modelo DirectQuery porque as configurações de níveis de compatibilidade mais antigos não têm contrapartes exatas nos níveis de compatibilidade 1200 e maior mais recentes. Se você tiver um modelo tabular existente que é executado no modo DirectQuery, você deve abrir o modelo no SQL Server Data Tools, desativar o DirectQuery, definir a **nível de compatibilidade** propriedade para 1200 ou superior e, em seguida, reconfigure o DirectQuery Propriedades. Ver [o modo DirectQuery](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md) para obter detalhes.


## <a name="see-also"></a>Confira também
[Compatibilidade com versões anteriores do Analysis Services (SQL Server 2017)](analysis-services-backward-compatibility-sql2017.md)
