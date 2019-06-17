---
title: Consultar os parâmetros usados para criar um modelo de mineração | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df2eb8317f90a96b35fc886e2158000e0f57d09d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62469475"
---
# <a name="query-the-parameters-used-to-create-a-mining-model"></a>Consultar os parâmetros usados para criar um modelo de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A composição de um modelo de mineração é afetada não apenas pelos casos de treinamento, mas também pelos parâmetros que foram definidos quando o modelo foi criado. Portanto, talvez seja útil recuperar as configurações de parâmetro de um modelo existente para compreender melhor o comportamento do modelo. A recuperação de parâmetros também é útil na documentação de uma versão específica desse modelo.  
  
 Para localizar parâmetros que foram usados quando o modelo foi criado, você cria uma consulta em um dos conjuntos de linhas do esquema do modelo de mineração. Esses conjuntos de linhas de esquema são expostos como um conjunto de exibições do sistema que pode ser consultado usando a sintaxe do Transact-SQL. Este procedimento descreve como criar uma consulta que retorna os parâmetros usados para criar o modelo de mineração especificado.  
  
### <a name="to-open-a-query-window-for-a-schema-rowset-query"></a>Para abrir uma janela Consulta para uma consulta de conjunto de linhas de esquema  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém o modelo que deseja consultar.  
  
2.  Clique com o botão direito do mouse no nome da instância, selecione **Nova Consulta**e selecione **DMX**.  
  
    > [!NOTE]  
    >  Você também pode criar uma consulta para um modelo de mineração de dados usando o modelo **MDX** .  
  
3.  Se a instância tiver vários bancos de dados, selecione o banco de dados que contém o modelo que deseja consultar na lista **Banco de Dados Disponíveis** da barra de ferramentas.  
  
### <a name="to-return-model-parameters-for-an-existing-mining-model"></a>Para retornar parâmetros de modelo para um modelo de mineração existente  
  
1.  No painel de consulta DMX, digite ou cole o seguinte texto:  
  
    ```  
    SELECT MINING_PARAMETERS  
    FROM $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = ''  
    ```  
  
2.  No Pesquisador de Objetos, selecione o modelo de mineração desejado e arraste-o no painel de consulta DMX, entre as aspas simples.  
  
3.  Pressione F5 ou clique em **Executar**.  
  
## <a name="example"></a>Exemplo  
 O código a seguir retorna uma lista dos parâmetros usados para criar o modelo de mineração que você criou no [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Esses parâmetros incluem os valores explícitos de todos os padrões usados pelos serviços de mineração disponíveis dos provedores no servidor.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
 O exemplo de código retorna os seguintes parâmetros para o modelo de clustering:  
  
 Resultados de eExample:  
  
 MINING_PARAMETERS  
  
 CLUSTER_COUNT=10,CLUSTER_SEED=0,CLUSTERING_METHOD=1,MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_STATES=100,MINIMUM_SUPPORT=1,MODELLING_CARDINALITY=10,SAMPLE_SIZE=50000,STOPPING_TOLERANCE=10  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções de consulta de Data Mining](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
