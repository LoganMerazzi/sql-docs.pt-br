---
title: Adicionar colunas a uma tabela de modelo tabular do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a726f7dd8ef72ad30bd055d2f76cc58c7db6183d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163113"
---
# <a name="add-columns-to-a-table"></a>Adicionar colunas a uma tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve como adicionar colunas a uma tabela existente.  
  
## <a name="add-columns-from-the-datasource"></a>Adicionar colunas da fonte de dados  
 Ao usar o Assistente de Importação de Tabela para importar dados de uma tabela de fonte de dados, uma nova tabela é criada no modelo que inclui todas as colunas na tabela de origem. Ou, se você escolher filtrar determinadas colunas usando o recurso Visualizar e Filtrar, somente essas colunas e os dados filtrados que você selecionar. Você também pode escrever uma Consulta SQL que especifica somente algumas colunas para importar. Você pode, no entanto, determinar posteriormente uma tabela de origem tem colunas adicionais que você deseja adicionar à tabela modelo ou precisa adicionar uma coluna calculada com valores derivados de uma fórmula DAX.  
  
 Por exemplo, se quando você inicialmente importou de uma fonte de dados, usou o recurso Visualizar e Filtrar no Assistente de Importação de Tabela para selecionar um número limitado de colunas da tabela de origem, você determina posteriormente que precisa adicionar outra coluna que existe na tabela de origem, mas ainda não existe na tabela modelo. Por exemplo, ou uma nova coluna AdjustedProfit foi acrescentada à tabela FactSales na fonte de dados e agora você deseja adicionar a mesma coluna AdjustedProfit e dados à tabela de Vendas no modelo.  
  
 Nestes casos, você pode usar a caixa de diálogo Editar Propriedades da Tabela para selecionar colunas da tabela de origem e adicioná-las à tabela modelo. A caixa de diálogo Editar Propriedades da Tabela inclui a janela de visualização da tabela. A janela de visualização da tabela exibe a tabela na origem. As colunas que já estão incluídas na definição de tabela modelo já estão marcadas. Essas colunas que ainda não estão incluídas na definição de tabela modelo não estão marcadas. Você pode adicionar colunas da origem para a definição de tabela modelo selecionando a coluna e clicando em OK. A janela de visualização de tabela na caixa de diálogo Editar Propriedades da Tabela fornece a mesma exibição e os recursos que a janela de visualização de tabela na página Visualizar e Filtrar do Assistente de Importação de Tabela.  
  
> [!IMPORTANT]  
>  Ao adicionar uma coluna a uma tabela que contém duas ou mais partições, antes de adicionar a coluna à definição de tabela usando a caixa de diálogo Editar Propriedades da Tabela, você deve usar o Gerenciador de Partições primeiro para adicionar a coluna a todas as partições definidas. Depois de adicionar a coluna às partições definidas, você pode adicionar a mesma coluna à definição de tabela usando a caixa de diálogo Editar Propriedades da Tabela.  
  
> [!NOTE]  
>  Se você usou uma Consulta SQL para selecionar tabelas e colunas quando inicialmente usou o Assistente de Importação de Tabela para importar dados, deve usar uma Consulta SQL novamente na caixa de diálogo Editar Propriedades da Tabela para adicionar colunas à tabela modelo.  
  
#### <a name="to-add-a-column-from-the-data-source-by-using-the-edit-table-properties-dialog-box"></a>Para adicionar uma coluna da fonte de dados usando a caixa de diálogo Editar Propriedades da Tabela  
  
1.  No designer de modelo, clique na tabela à qual você quer adicionar uma coluna, clique no menu **Tabela** e clique em  **Propriedades da Tabela**.  
  
2.  Na caixa de diálogo **Editar Propriedades da Tabela** , na janela de visualização de tabela, selecione a coluna de origem que você quer adicionar e clique em OK. As colunas já incluídas na definição de tabela já estarão marcadas.  
  
## <a name="add-a-calculated-column"></a>Adicionar uma coluna calculada  
 Em uma coluna calculada, uma fórmula DAX é usada para definir um valor para cada linha. Por exemplo, você pode criar uma coluna calculada com uma fórmula simples (=1) que acrescenta um valor de 1 a cada linha. Colunas calculadas também podem ter mais fórmulas complexas que calculam valores com base em outros dados no modelo. As colunas calculadas são abordadas em mais detalhes em outros tópicos. Para obter mais informações, consulte [Colunas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md).  
  
#### <a name="to-create-a-calculated-column"></a>Para criar uma coluna calculada  
  
1.  No designer de modelo, na Exibição de Dados, selecione a tabela à qual você quer adicionar uma coluna calculada em branco, role até a coluna mais à direita, ou clique no menu **Coluna** e clique em **Adicionar Coluna**.  
  
     Para criar uma nova coluna entre duas colunas existentes, clique com o botão direito do mouse em uma coluna existente e clique em **Inserir Coluna**.  
  
2.  Na barra de fórmulas, digite uma fórmula DAX para adicionar atributos para cada linha.  
  
## <a name="add-a-blank-column"></a>Adicionar uma coluna em branco  
 Você pode criar uma coluna nomeada e em branco em uma tabela modelo. Colunas em branco poderão ser úteis se você desejar colar dados de outra origem. Lembre-se de que dados colados são armazenados de maneira diferente de dados importados. Para obter mais informações, consulte [copiar e colar dados](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md).  
  
#### <a name="to-create-a-named-blank-column"></a>Para criar uma coluna nomeada e em branco  
  
1.  No designer de modelo, na Exibição de Dados, selecione a tabela à qual você quer adicionar uma coluna em branco, role até a coluna mais à direita, ou clique no menu **Coluna** e clique em **Adicionar Coluna**.  
  
     Para criar uma nova coluna entre duas colunas existentes, clique com o botão direito do mouse em uma coluna existente e clique em **Inserir Coluna**.  
  
2.  Clique na célula superior, digite um nome e, em seguida, pressione ENTER.  
  
## <a name="see-also"></a>Confira também  
 [Editar caixa de diálogo de propriedades de tabela](http://msdn.microsoft.com/library/8d913e83-7246-44cc-8fc7-31729023c0d8)   
 [Alterar os mapeamentos de tabela, de coluna ou de filtro de linha](../../analysis-services/tabular-models/change-table-column-or-row-filter-mappings-ssas-tabular.md)  
  
  
