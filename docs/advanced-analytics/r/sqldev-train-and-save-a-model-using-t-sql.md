---
title: "Lição 5: Treinar e salvar um modelo usando o T-SQL | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: 10
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 785e4dc3db234447c806ddc349682d08a8447923
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-5-train-and-save-a-model-using-t-sql"></a>Lição 5: Treinar e salvar um modelo usando o T-SQL

Este artigo faz parte de um tutorial para desenvolvedores em SQL sobre como usar o R no SQL Server.

Nesta lição, você aprenderá a treinar um modelo de aprendizado de máquina usando o R. Você treinar o modelo usando os recursos de dados que você acabou de criar e, em seguida, salve o modelo treinado em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. Nesse caso, os pacotes R já estão instalados com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], portanto, tudo o que pode ser feito no SQL.

## <a name="create-the-stored-procedure"></a>Criar o procedimento armazenado

Ao chamar o R do T-SQL, você use o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). No entanto, para os processos que você repetir com frequência, como o treinamento de um modelo, é mais fácil encapsular a chamada para `sp_execute_exernal_script` em outro procedimento armazenado.

1.  Primeiro, crie um procedimento armazenado que contém o código de R para criar o modelo de previsão de dica. Em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma nova **consulta** janela e execute a seguinte instrução para criar o procedimento armazenado _TrainTipPredictionModel_. Esse procedimento armazenado define os dados de entrada e usa um pacote do R para criar um modelo de regressão logística.

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTipPredictionModel]
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
      -- Insert the trained model into a database table
      INSERT INTO nyc_taxi_models
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model and put it in data frame
    trained_model <- data.frame(model=as.raw(serialize(logitObj, NULL)));
    ',
      @input_data_1 = @inquery,
      @output_data_1_name = N'trained_model'
      ;
    
    END
    GO
    ```

    - No entanto, para garantir que alguns dados restante para testar o modelo, 70% dos dados são selecionados aleatoriamente da tabela de dados táxi.
    
    - A consulta SELECT usa a função escalar personalizada _fnCalculateDistance_ para calcular a distância direta entre os locais de embarque e desembarque de passageiros.  os resultados da consulta são armazenados na variável de entrada padrão do R, `InputDataset`.
  
    - As chamadas de script R a `rxLogit` função, que é uma das funções de R aprimoradas incluídos com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para criar o modelo de regressão logística.
  
        A variável binária _tipped_ é usada como a coluna *label* ou de resultado, e o modelo é ajustado com o uso destas colunas de recursos:  _passenger_count_, _trip_distance_, _trip_time_in_secs_e _direct_distance_.
  
    -   O modelo treinado, salvo na variável do R `logitObj`, é serializado e colocado em um quadro de dados para a saída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa saída é inserida na tabela de banco de dados _nyc_taxi_models_, de modo que você possa usá-la para previsões futuras.
  
2.  Execute a instrução para criar o procedimento armazenado, se ainda não existir.

## <a name="generate-the-r-model-using-the-stored-procedure"></a>Gerar o modelo de R usando o procedimento armazenado

Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

1. Para gerar o modelo de R, chame o procedimento armazenado sem outros parâmetros:

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. Assista a **mensagens** janela de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para mensagens que poderiam ser canalizadas do R **stdout** fluxo, como essa geração: 

    "Mensagem (NS) STDOUT do script externo: linhas lidas: 1193025, linhas de Total processadas: 1193025, tempo Total de bloco: 0.093 segundos"

    Você também poderá ver mensagens específicas de função individual, `rxLogit`, exibir as variáveis e métricas geradas como parte da criação do modelo de teste.

3.  Quando a instrução for concluída, abra a tabela *nyc_taxi_models*. Processamento de dados e ajustar o modelo podem demorar um pouco.

    Você pode ver que uma nova linha foi adicionada, que contém o modelo serializado na coluna _modelo_.

    ```
    model
    ------
    0x580A00000002000302020....
    ```

Na próxima etapa, você usará o modelo treinado para criar previsões.

## <a name="next-lesson"></a>Próxima lição

[Lição 6: Colocar o modelo](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 4: Criar recursos de dados usando o T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

