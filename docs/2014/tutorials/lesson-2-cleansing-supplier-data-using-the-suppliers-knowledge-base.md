---
title: 'Lição 2: Limpeza de dados do fornecedor usando a Base de dados de Conhecimento fornecedores | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 215c14de-fc3f-46de-a022-bf69b9ea2a96
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b99676a9f51bf76dc9db294365a5a628dd25fa2e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488470"
---
# <a name="lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base"></a>Lição 2: Como limpar dados de fornecedor usando a base de dados de conhecimento Fornecedores
  Nesta lição, você deve limpar os dados do fornecedor em um arquivo do Excel usando o **fornecedores** base de dados de conhecimento que você criou na primeira lição. Limpeza de dados no DQS inclui um **processo auxiliado por computador** que analisa como dados está em conformidade com o conhecimento em uma base de dados de conhecimento e um **processo interativo** que permite que você examine e modifique resultados do processo auxiliado por computador. O recurso de limpeza de dados identifica dados incorretos na fonte de dados e corrige ou sugere correções para os dados incorretos. Também padroniza e enriquece dados de cliente usando valores de domínio, valores principais para sinônimos, regras de domínio, relações baseadas em termos e dados de referência. Você pode aprovar ou rejeitar interativamente as alterações propostas pelo processo auxiliado por computador. Ver [limpeza de dados](https://msdn.microsoft.com/library/gg524800.aspx) para obter mais detalhes.  
  
 O processo auxiliado por computador usa os valores de limite a seguir que você pode configurar usando a opção Configuração na página principal do Cliente DQS.  
  
-   **Pontuação mínima para sugestões:** A pontuação mínima ou o nível de confiança que é usado pelo DQS para sugerir a substituição de um valor.  
  
-   **Pontuação mínima para correções automáticas:** A pontuação mínima ou o nível de confiança que é usado pelo DQS para corrigir automaticamente um valor.  
  
 Ver [configurar valores de limite para limpeza e correspondência](https://msdn.microsoft.com/library/hh510415.aspx) para obter detalhes sobre como definir essas configurações.  
  
 Nesta lição, você executará as seguintes tarefas para limpar os dados de entrada usando a base de dados de conhecimento Fornecedores.  
  
1.  Crie um Projeto do Data Quality para Limpeza, selecione a base de dados de conhecimento Fornecedores como a base de dados de conhecimento a ser usada para analisar e limpar os dados de origem em um arquivo do Excel e selecione a atividade Limpeza.  
  
2.  Mapeie as colunas do Excel que você deseja limpar para os domínios do DQS/domínios compostos apropriados na base de dados de conhecimento.  
  
3.  Execute a atividade de limpeza auxiliada por computador. O processo auxiliado por computador exibe informações de qualidade de dados no Cliente do Data Quality que você pode usar para limpar os dados interativamente.  
  
4.  Exiba e gerencie os resultados da atividade de limpeza. Você pode examinar os valores que o processo auxiliado pelo computador considerar corretos, incorretos mas corrigidos, incorretos com uma alteração sugerida ou inválidos. Você pode aprovar ou rejeitar interativamente as alterações, corrigir ou substituir a sugestão do processo auxiliado pelo computador usando o campo Corrigir para.  
  
5.  Exporte os resultados do processo de limpeza para um arquivo do Excel.  
  
6.  Importe os valores do projeto de limpeza para domínios para aumentar o conhecimento na base de conhecimento com novas regras, valores, correções etc...  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 1: Criar um projeto de qualidade de dados](../../2014/tutorials/task-1-creating-a-data-quality-project.md)  
  
  
