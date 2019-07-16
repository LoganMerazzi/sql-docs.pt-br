---
title: Adicionar uma tabela com um modelo de tabela do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 224df75c15acf560c7eadc70fe91fbbc2b0396d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207869"
---
# <a name="add-a-table"></a>Adicionar uma tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve como adicionar uma tabela de uma fonte de dados do qual você tiver importado anteriormente dados em seu modelo. Para adicionar uma tabela da mesma fonte de dados, você pode usar a conexão de fonte de dados existente. É recomendado sempre usar uma única conexão ao importar qualquer número de tabelas de uma única fonte de dados.  
  
### <a name="to-add-a-table-from-an-existing-data-source"></a>Para adicionar uma tabela de uma fonte de dados existente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Conexões Existentes**.  
  
2.  Na página **Conexões existentes** , selecione a conexão para a fonte de dados que tem a tabela que você deseja adicionar e clique em **Abrir**.  
  
3.  Na página **Selecionar Tabelas e Exibições** , selecione a tabela da fonte de dados que você deseja adicionar a seu modelo.  
  
    > [!NOTE]  
    >  A página **Selecionar Tabelas e Exibições** não mostrará tabelas que foram importadas previamente como marcadas.  Se você selecionar uma tabela que foi importada previamente usando esta conexão, e você não deu à tabela um nome amigável diferente, um 1 será acrescentado ao nome amigável. Você não precisa selecionar novamente nenhuma tabela que foi previamente importada usando esta conexão.  
  
4.  Se necessário, use **Visualizar e Filtrar** para selecionar somente certas colunas ou aplicar filtros aos dados a serem importados.  
  
5.  Clique em **Concluir** para importar a nova tabela.  
  
> [!NOTE]  
>  Ao importar várias tabelas ao mesmo tempo de uma única fonte de dados, as relações entre essas tabelas na origem serão automaticamente criadas no modelo. Ao adicionar uma tabela posteriormente, porém, você pode precisar criar relações manualmente no modelo entre tabelas recém-adicionadas e as tabelas que foram previamente importadas.  
  
## <a name="see-also"></a>Confira também  
 [Importar dados](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [Excluir uma tabela](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)  
  
  
