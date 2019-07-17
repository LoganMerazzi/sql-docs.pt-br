---
title: Partições em modelos de tabela do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d26b1b1558ca546fb47660488b15dc777c5ad87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162725"
---
# <a name="partitions"></a>Partições
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  As partições dividem uma tabela em partes lógicas. Cada partição pode ser processada (Atualizada) independentemente de outras partições. As partições criadas usando a caixa de diálogo partições no SSDT durante a criação do modelo se aplicam ao banco de dados de espaço de trabalho modelo. Quando o modelo é implantado, as partições definidas para o banco de dados de workspace modelo são duplicadas no banco de dados modelo implantado. Além disso, você pode criar e gerenciar partições para um banco de dados modelo implantado usando a caixa de diálogo partições no SSMS.  As informações fornecidas neste tópico descrevem partições criadas durante a criação de modelo usando a caixa de diálogo Gerenciador de partições no SSDT. Para obter informações sobre como criar e gerenciar partições para um modelo implantado, consulte [criar e gerenciar partições de modelos tabulares](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
##  <a name="bkmk_benefits"></a> Benefícios  
 Partições, em modelos tabulares, dividem uma tabela em objetos de partição lógicos. Cada partição pode ser processada independentemente de outras partições. Por exemplo, uma tabela pode incluir determinados conjuntos de linha que contêm dados que raramente são alterados, mas outros conjuntos de linha têm dados que são alterados frequentemente. Nestes casos, não há necessidade de processar todos os dados quando você realmente só deseja processar uma parte deles. As partições permitem que você divida porções de dados que você deseja processar com frequência dos dados que podem ser processados com menos frequência.  
  
 O design de modelo eficaz utiliza partições para eliminar processamento desnecessário e carga de processador subsequente em servidores do Analysis Services, enquanto, ao mesmo tempo, faz certos dados que são processados e atualizados com bastante frequência refletirem os dados mais recentes de fontes de dados. O modo como você implementa e utiliza partições durante a criação de modelo pode ser muito diferente de como partições são implementadas e utilizadas para modelos implantados. Mantenha em mente que, durante a fase de criação modelo, você pode estar trabalhando com somente um subconjunto dos dados que estarão, no final das contas, em seu modelo implantado.  
  
### <a name="processing-partitions"></a>Processando partições  
 Para modelos implantados, o processamento ocorre usando o SSMS ou executando um script que inclui o comando de processo e especifica as configurações e opções de processamento. Ao criar modelos usando o SSDT, você pode executar operações de processo usando um comando da barra de ferramentas ou menu modelo de processo. Uma operação de Processo pode ser especificada para uma partição, uma tabela ou tudo.  
  
 Quando uma operação de processo é executada, uma conexão para a fonte de dados é feita usando a conexão de dados. Novos dados são importados nas tabelas modelo, relações e hierarquias são recriadas para cada tabela, e cálculos em colunas calculadas e medidas são recalculados.  
  
 Ao dividir a tabela mais ainda em partições lógicas, você poderá determinar seletivamente o que, quando e como os dados em cada partição são processados. Quando você implanta um modelo, o processamento de partições pode ser concluído manualmente usando a caixa de diálogo partições no SSMS ou usando um script que executa um comando de processo.  
  
### <a name="partitions-in-the-model-workspace-database"></a>Partições no banco de dados de workspace modelo  
 Você pode criar novas partições, editar, mesclar ou excluir partições usando o Gerenciador de partições no SSDT. Dependendo do nível de compatibilidade do modelo que você está criando, o Gerenciador de partições fornece dois modos para selecionar tabelas, linhas e colunas para uma partição: Para modelos de tabela 1400, as partições são definidas por meio de uma consulta de M ou você pode usar o modo de Design para abrir o Editor de consultas. Para tabular 1100, 1103, 1200 modelos, use o modo de visualização de tabela e o modo de consulta SQL. 
  
### <a name="partitions-in-a-deployed-model-database"></a>As partições em um banco de dados modelo implantado  
 Quando você implanta um modelo, as partições para o banco de dados modelo implantado serão exibido como objetos de banco de dados no SSMS. Você pode criar, editar, mesclar e excluir partições para um modelo implantado usando a caixa de diálogo partições no SSMS. Gerenciar partições para um modelo implantado no SSMS está fora do escopo deste tópico. Para saber mais sobre como gerenciar partições no SSMS, consulte [criar e gerenciar partições de modelos tabulares](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Criar e gerenciar partições no banco de dados de workspace](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)|Descreve como criar e gerenciar partições no banco de dados de espaço de trabalho modelo usando o Gerenciador de partições no SSDT.|  
|[Processar partições no banco de dados de workspace](../../analysis-services/tabular-models/process-partitions-in-the-workspace-database-ssas-tabular.md)|Descreve como processar (atualizar) partições no banco de dados de workspace modelo.|  
  
## <a name="see-also"></a>Confira também  
 [Modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Processar dados](../../analysis-services/tabular-models/process-data-ssas-tabular.md)  
  
  
