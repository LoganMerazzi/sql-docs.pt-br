---
title: Guia de início rápido para um Python básico de "Hello World" a execução no T-SQL – SQL Server Machine Learning do código
description: Guia de início rápido para o script Python no SQL Server. Conheça os fundamentos de chamar o script de Python usando o procedimento armazenado do sistema sp_execute_external_script em um exercício de Olá, mundo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/10/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6d8da3ce90e915344f2380d4cd5cc866db6715ef
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59476631"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>Início Rápido: Script de Python de "Hello world" no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste início rápido, você aprenderá conceitos-chave, executando um Python "Hello World" script inT-SQL, uma introdução para o **sp_execute_external_script** procedimento armazenado do sistema. 

## <a name="prerequisites"></a>Prerequisites

Um início rápido anterior, [Python Verifique se existe no SQL Server](quickstart-python-verify.md), fornece informações e links para configurar o ambiente do Python necessário para este início rápido.

## <a name="basic-python-interaction"></a>Interação de Python básica

Há duas maneiras de executar código Python no SQL Server:

+ Adicionar um script Python como um argumento de procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ De um [cliente de Python remoto](../python/setup-python-client-tools-sql.md), conecte-se ao SQL Server e executar o código usando o SQL Server como o contexto de computação. Isso exige [revoscalepy](../python/ref-py-revoscalepy.md).

O exercício a seguir destina-se no modelo de interação de primeira: como passar o código do Python para um procedimento armazenado.

1. Execute alguns códigos simples para ver como os dados são passados bidirecionalmente entre o SQL Server e o Python.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. Supondo que você tem tudo configurado corretamente, e o Python e o SQL Server estiverem falando uns aos outros, o resultado correto é calculado e o Python `print` função retorna o resultado para o **mensagens** windows.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Ao obter **stdout** mensagens é útil ao testar seu código, mais geralmente, você precisa retornar os resultados em formato tabular, para que você possa usá-lo em um aplicativo ou escrevê-lo a uma tabela.

Por enquanto, lembre-se estas regras:

+ Tudo dentro de `@script` argumento deve ser um código Python válido. 
+ O código deve seguir todas as regras de Python relativos a recuo, nomes de variáveis e assim por diante. Quando você receber um erro, verifique o espaço em branco e o uso de maiusculas.
+ Entre linguagens de programação Python é uma das mais flexível em relação a aspas simples e aspas duplas; eles são bastante intercambiáveis. No entanto, o T-SQL usa aspas simples para somente determinadas coisas e o `@script` argumento usa aspas simples para colocar o código do Python como uma cadeia de caracteres Unicode. Portanto, você precisará examinar o código do Python e alterar alguns aspas para aspas duplas.
+ Se você estiver usando todas as bibliotecas que não são carregadas por padrão, você deve usar uma instrução de importação no início do seu script para carregá-los. SQL Server adiciona várias bibliotecas de produto específico. Para obter mais informações, consulte [bibliotecas de Python](../python/python-libraries-and-data-types.md).
+ Se a biblioteca já não estiver instalada, pare e instalar o pacote do Python fora do SQL Server, conforme descrito aqui: [Instalar os novos pacotes Python no SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>Executar um script Hello World

O exercício a seguir executa outro scripts de Python simples.

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

Entradas para esse procedimento armazenado incluem:

+ *@language* parâmetro define a extensão da linguagem para chamar, nesse caso, Python.
+ *@script* o parâmetro define os comandos transmitidos para o tempo de execução do Python. O script de Python inteiro deve ser colocado entre este argumento, como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável.
+ *@input_data_1* dados são retornados pela consulta, passada para o tempo de execução do Python, que retorna os dados para o SQL Server como um quadro de dados.
+ COM conjuntos de resultados cláusula define o esquema da tabela de dados retornados para o SQL Server, adicionando "Hello World" como o nome da coluna **int** para o tipo de dados.

**Resultados**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Próximas etapas

Agora que executar alguns scripts de Python simples, dar uma olhada nas estruturação de entradas e saídas.

> [!div class="nextstepaction"]
> [Guia de início rápido: Lidar com entradas e saídas](quickstart-python-inputs-and-outputs.md)
