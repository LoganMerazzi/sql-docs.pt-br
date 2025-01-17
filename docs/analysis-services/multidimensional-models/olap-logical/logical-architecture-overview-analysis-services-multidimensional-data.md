---
title: Visão geral da arquitetura lógica (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aca12552338eb05549199b22af3a63e9f4b4a101
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208664"
---
# <a name="logical-architecture-overview-analysis-services---multidimensional-data"></a>Visão geral da arquitetura lógica (Analysis Services – Dados Multidimensionais)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  O Analysis Services funciona em um modo de implantação de servidor que determina a arquitetura de memória e o ambiente de tempo de execução usados pelos diferentes tipos de modelos do Analysis Services. O modo de servidor é determinado durante a instalação. **Modo multidimensional e mineração de dados** dá suporte a OLAP tradicional e mineração de dados. **Modo de tabela** dá suporte a modelos de tabela. **Modo integrado do SharePoint** refere-se a uma instância do Analysis Services que foi instalado como [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint, usado para carregar e consultar o Excel ou [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modelos de dados dentro de uma pasta de trabalho.  
  
 Este tópico explica a arquitetura básica do Analysis Services no modo Multidimensional e de Mineração de Dados. Para obter mais informações sobre outros modos, consulte [modelagem Tabular](../../../analysis-services/tabular-models/tabular-models-ssas.md) e [comparando tabulares e multidimensionais soluções](../../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md).  
  
## <a name="basic-architecture"></a>Arquitetura básica  
 Uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pode conter vários bancos de dados, e um banco de dados pode ter objetos OLAP e objetos de mineração de dados simultaneamente. Os aplicativos se conectam a uma instância específica do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e a um banco de dados específico. Um computador servidor pode servir de host de várias instâncias do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Instâncias do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] são nomeadas como "\<ServerName >\\< nome_da_instância\>". A ilustração a seguir mostra todas as relações mencionadas entre [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos.  
  
 ![Relações de objetos de execução AMO](../../../analysis-services/multidimensional-models/olap-logical/media/amo-runningobjects.gif "relações de objetos de execução AMO")  
  
 As classes básicas são o conjunto mínimo de objetos exigidos para criar um cubo. Esse conjunto mínimo de objetos é uma dimensão, um grupo de medidas e uma partição. Uma agregação é opcional.  
  
 As dimensões são criadas a partir de atributos e hierarquias. As hierarquias são formadas por um conjunto ordenado de atributos, sendo que cada atributo do conjunto corresponde a um nível na hierarquia.  
  
 Os cubos são criados a partir de dimensões e grupos de medidas. As dimensões na coleta de dimensões de um cubo pertencem à coleta de dimensões do banco de dados. Os grupos de medidas são coletas de medidas que têm a mesma exibição de fonte de dados e têm o mesmo subconjunto de dimensões do cubo. Um grupo de medidas tem uma ou mais partições para gerenciar os dados físicos. Um grupo de medidas pode ter um projeto de agregação padrão. O projeto de agregação padrão pode ser usado por todas as partições no grupo de medidas, além disso, cada partição pode ser seu próprio projeto de agregação.  
  
 Objetos do servidor  
 Cada instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é vista como um objeto de servidor diferente no AMO; cada instância diferente está conectada a um objeto <xref:Microsoft.AnalysisServices.Server> por uma conexão diferente. Cada objeto de servidor contém uma ou mais fonte de dados, exibições de fonte de dados e objetos de banco de dados, bem como assemblies e funções de segurança.  
  
 Objetos de dimensão  
 Cada objeto de banco de dados contém vários objetos de dimensão. Cada objeto de dimensão contém um ou mais atributos que são organizados em hierarquias.  
  
 Objetos de Cubo  
 Cada objeto de banco de dados contém um ou mais objetos de cubo. Um cubo é definido por suas medidas e dimensões. As medidas e dimensões em um cubo são derivadas de tabelas e exibições na exibição de fonte de dados, na qual o cubo teve base ou para a qual foi gerado a partir das definições de medida e dimensão.  
  
## <a name="object-inheritance"></a>Herança de objetos  
 O modelo de objeto ASSL contém muitos grupos de elementos repetidos. Por exemplo, o grupo de elementos, "**dimensões** contêm **hierarquias**," define a hierarquia da dimensão de um elemento. Ambos **cubos** e **MeasureGroups** contêm o grupo de elementos, "**dimensões** contêm **hierarquias**."  
  
 A menos que explicitamente substituído, um elemento herda os detalhes desses grupos de elementos repetidos do nível mais alto. Por exemplo, o **traduções** para um **CubeDimension** são os mesmos que os **traduções** para seu elemento ancestral, **cubo**.  
  
 Para substituir explicitamente as propriedades herdadas de um objeto de nível mais alto, um objeto não precisa repetir toda a estrutura e propriedades do objeto de nível mais alto. As únicas propriedades que um objeto precisa declarar explicitamente são aquelas que ele deseja substituir. Por exemplo, uma **CubeDimension** pode listar apenas aquelas **hierarquias** que precisa ser desabilitado no **cubo**, ou para a qual a visibilidade precisa ser alterado, ou para a qual alguns **Nível** detalhes não foram fornecidos com o **dimensão** nível.  
  
 Algumas propriedades especificadas em um objeto fornecem valores padrão para a mesma propriedade em um objeto filho ou descendente. Por exemplo, **Cube.StorageMode** fornece o valor padrão de **Partition.StorageMode**. No caso dos valores padrão herdados, o ASSL aplica essas regras aos valores padrão herdados:  
  
-   Quando a propriedade do objeto filho for nula no XML, o valor da propriedade usará o valor herdado como padrão. No entanto, se você consultar o valor a partir do servidor, este retornará o valor nulo do elemento XML.  
  
-   Não é possível determinar programaticamente se a propriedade ou objeto filho foi definida corretamente no objeto filho ou herdado.  
  
## <a name="example"></a>Exemplo  
 O cubo Importações contém duas medidas, Pacotes e Último, e três dimensões relacionadas, Rota, Origem e Horário.  
  
 ![Exemplo 1 de cubo](../../../analysis-services/multidimensional-models/olap-logical/media/cubeintro1.gif "exemplo 1 de cubo")  
  
 Os valores alfanuméricos menores ao redor do cubo são os membros das dimensões. Exemplos de membros são: terra (membro da dimensão Rota), África (membro da dimensão Origem) e 1º trimestre (membro da dimensão Horário).  
  
### <a name="measures"></a>medidas  
 Os valores nas células do cubo representam as duas medidas, Pacotes e Último. A medida pacotes representa o número de pacotes importados e o **soma** função é usada para agregar os fatos. A medida último representa a data de recebimento e o **máx** função é usada para agregar os fatos.  
  
### <a name="dimensions"></a>Dimensões  
 A dimensão Rota representa os meios pelos quais as importações alcançam seu destino. Os membros dessa dimensão incluem terra, não-terra, aérea, marítima, rodoviária ou ferroviária. A dimensão Origem representa os locais onde as importações são produzidas, como África ou Ásia. A dimensão Horário representa os trimestres e semestres de um mesmo ano.  
  
### <a name="aggregates"></a>Agregações  
 Os usuários empresariais de um cubo podem determinar o valor de qualquer medida de cada membro de qualquer dimensão, independentemente do nível do membro na dimensão, pois o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] agrega valores em níveis superiores, conforme necessário. Por exemplo, os valores de medida na ilustração anterior podem ser agregados acordo com uma hierarquia de calendário padrão usando a hierarquia de tempo de calendário na dimensão de tempo, conforme ilustrado no diagrama a seguir.  
  
 ![Diagrama de medidas organizadas ao longo da dimensão de tempo](../../../analysis-services/multidimensional-models/olap-logical/media/cubeintro2.gif "diagrama de medidas organizadas ao longo da dimensão de tempo")  
  
 Além de agregar medidas usando uma única dimensão, você pode agregar medidas usando combinações de membros de diferentes dimensões. Isso permite que os usuários empresariais avaliem, simultaneamente, as medidas em várias dimensões. Por exemplo, se um usuário empresarial quiser analisar trimestralmente as importações que são recebidas por via aérea dos hemisférios ocidental e oriental, ele poderá emitir uma consulta ao cubo para recuperar o conjunto de dados a seguir.  
  
||||Packages|||Last|||  
|-|-|-|--------------|-|-|----------|-|-|  
||||Todas as origens|Hemisfério oriental|Hemisfério ocidental|Todas as origens|Hemisfério oriental|Hemisfério ocidental|  
|Todo o tempo|||25110|6547|18563|29-dez-99|22-dez-99|29-dez-99|  
||1º semestre||11173|2977|8196|28-jun-99|20-jun-99|28-jun-99|  
|||1º trimestre|5108|1452|3656|30-mar-99|19-mar-99|30-mar-99|  
|||2º trimestre|6065|1525|4540|28-jun-99|20-jun-99|28-jun-99|  
||2º semestre||13937|3570|10367|29-dez-99|22-dez-99|29-dez-99|  
|||3º trimestre|6119|1444|4675|30-set-99|18-set-99|30-set-99|  
|||4º trimestre|7818|2126|5692|29-dez-99|22-dez-99|29-dez-99|  
  
 Depois que um cubo for definido, você pode criar novas agregações ou alterar as agregações existentes para definir opções como, se as agregações serão pré-calculadas durante o processamento ou calculadas durante a consulta. **Tópico relacionado:** [agregações e Designs de agregação](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
### <a name="mapping-measures-attributes-and-hierarchies"></a>Mapeando medidas, atributos e hierarquias  
 As medidas, atributos e hierarquias no cubo de exemplo são derivados das seguintes colunas nas tabelas de fatos e dimensões do cubo.  
  
|Medida ou atributo (nível)|Members|Tabela de origem|Coluna de origem|Valor da coluna de exemplo|  
|------------------------------------|-------------|------------------|-------------------|-------------------------|  
|Medida de pacotes|Não aplicável|ImportsFactTable|Packages|12|  
|Última medida|Não aplicável|ImportsFactTable|Last|03-mai-99|  
|Nível Categoria da Rota na dimensão Rota|não-terra, terra|RouteDimensionTable|Route_Category|Não-terra|  
|Atributo Rota na dimensão Rota|aérea,marítima,rodoviária,ferroviária|RouteDimensionTable|Rota|Marítima|  
|Atributo Hemisfério na dimensão Origem|Hemisfério oriental,Hemisfério ocidental|SourceDimensionTable|Hemisphere|Hemisfério oriental|  
|Atributo Continente na dimensão Origem|África,Ásia,Austrália,Europa,América do Norte, América do Sul|SourceDimensionTable|Continente|Europe|  
|Atributo Semestre na dimensão Horário|1º semestre,2º semestre|TimeDimensionTable|Half|2º semestre|  
|Atributo Trimestre na dimensão Horário|1º trimestre,2º trimestre,3º trimestre,4º trimestre|TimeDimensionTable|Quarter|3º trimestre|  
  
 Dados em uma única célula de cubo são normalmente derivados de várias linhas de uma tabela de fatos. Por exemplo, a célula do cubo na interseção do membro ar, membro África e membro 1º trimestre contém um valor que é derivado por agregação das seguintes linhas na **ImportsFactTable** tabela de fatos.  
  
|||||||  
|-|-|-|-|-|-|  
|Import_ReceiptKey|RouteKey|SourceKey|TimeKey|Packages|Last|  
|3516987|1|6|1|15|10-jan-99|  
|3554790|1|6|1|40|19-jan-99|  
|3572673|1|6|1|34|27-jan-99|  
|3600974|1|6|1|45|02-fev-99|  
|3645541|1|6|1|20|09-fev-99|  
|3674906|1|6|1|36|17-fev-99|  
  
 Na tabela anterior, cada linha tem os mesmos valores para o **RouteKey**, **SourceKey**, e **TimeKey** colunas, indicando que essas linhas contribuem para a mesma célula do cubo.  
  
 O exemplo mostrado aqui representa um cubo muito simples, que tem um único grupo de medidas e no qual todas as tabelas de dimensões são unidas à tabela de fatos em um esquema em estrela. Outro esquema comum é um esquema floco de neve no qual uma ou mais tabelas de dimensão unem-se a outra tabela de dimensão, em vez de unirem-se diretamente à tabela de fatos. **Tópico relacionado:** [dimensões &#40;Analysis Services - dados multidimensionais&#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 O exemplo mostrado aqui contém uma única tabela de fatos. Quando um cubo tem várias tabelas de fatos, as medidas de cada tabela de fatos são organizadas em grupos de medidas e um grupo de medidas está relacionado à um conjunto específico de dimensões por relações de dimensões definidas. Essas relações são definidas pela especificação das tabelas participantes na exibição de fonte de dados e granularidade da relação. **Tópico relacionado:** [relações de dimensão](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
## <a name="see-also"></a>Consulte também  
 [Bancos de dados de modelo multidimensional](../../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
