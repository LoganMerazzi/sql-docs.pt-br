---
title: Trabalhando com os arquivos de Script de Console de exemplo (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sample console script files
ms.assetid: 7e6aaa8a-5f5c-414d-9fb8-21e56b9ffaef
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7d00385c7346d7602719326dbe700f7cd44c63fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288567"
---
# <a name="working-with-the-sample-console-script-files-mysqltosql"></a>Trabalhando com os arquivos de Script de Console de exemplo (MySQLToSQL)
Alguns arquivos de exemplo foram fornecidos juntamente com o produto para a referência de usuário e o uso. Esta seção descreve a maneira de personalizar facilmente esses scripts para as necessidades do usuário final.  
  
## <a name="sample-console-script-files"></a>Arquivos de Script de Console de exemplo  
Os seguintes arquivos de script de console de exemplo que abrangem cenários diferentes foram fornecidos para referência de usuário:  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   Este exemplo fornece os diferentes modos de conexão disponível para o banco de dados de origem e de destino e o usuário pode selecionar qualquer modo, de acordo com o requisito. Este exemplo contém as definições de servidor.  
  
    -   O usuário pode se conectar ao banco de dados necessário, simplesmente alterando os valores para a origem necessários e definições de servidor de destino. No exemplo fornecido todos os valores foram fornecidos valores como variáveis que estão disponíveis na **VariableValueFileSample.xml**.  Todos os outros parâmetros de conexão podem ser removidos do arquivo de conexão de servidor de trabalho do usuário.  
  
    -   Para obter mais informações sobre como se conectar ao servidor de origem e destino, consulte [criar os arquivos de Conexão de servidor &#40;MySQLToSQL&#41; ](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md) .  
  
-   **VariableValueFileSample.xml:** Arquivos de script de todas as variáveis que foram usadas no console do exemplo e `ServersConnectionFileSample.xml` foram agrupadas nesse arquivo. Para executar os scripts de console de exemplo que o usuário tem que simplesmente substituir a variável de exemplo valores com o usuário definido aqueles e passam esse arquivo como um argumento de linha de comando adicionais, juntamente com o arquivo de script.  
  
    Para obter mais informações sobre o arquivo de valor de variável, consulte [criando arquivos de valor de variável &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md).  
  
-   **AssessmentReportGenerationSample.xml:** Este exemplo permite ao usuário gerar um relatório de avaliação de xml que pode ser usado pelo usuário para análise antes que ele comece a converter e migrar os dados.  
  
    No `generate-assessment-report` o usuário deve alterar mandatorily o valor da variável de comando (consulte **VariableValueFileSample.xml**) na `object-name` do atributo a ser o nome de banco de dados em uso pelo usuário. Dependendo do tipo de objeto especificado, o `object-type` valor também terá que ser alterado.  
  
    Se o usuário tem que avaliar vários objetos / bancos de dados ele pode especificar vários `metabase-object` nós conforme ilustrado no `generate-assessment-report` 4 de exemplo do comando do exemplo de arquivo de script de console.  
  
    Para obter mais informações sobre como gerar relatórios, consulte [geração de relatórios &#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md).  
  
    **Observações:**  
  
    -   Certifique-se de que o argumento de linha de comando do arquivo de valor da variável é passado para o aplicativo de console e VariableValueFileSample.xml é atualizado com o usuário especificado valores.  
  
    -   Certifique-se de que o argumento de linha de comando de arquivo de conexão de servidor é passado para o aplicativo de console e o ServersConnectionFileSample.xml é atualizado com os valores de parâmetro de servidor correto.  
  
-   **SqlStatementConversionSample.xml:**  
    Este exemplo permite que o usuário gere correspondente `t-sql` script para o banco de dados de origem `sql` comando fornecido como entrada.  
  
    No `convert-sql-statement` o usuário deve alterar mandatorily o valor da variável de comando (consulte **VariableValueFileSample.xml**) na `context` do atributo como o nome do banco de dados que está sendo utilizado pelo usuário. O usuário também precisará alterar o `sql` valor de atributo para o banco de dados de origem `sql` comando que ele exija a ser convertido.  
  
    O usuário também pode fornecer arquivos sql a ser convertido. Isso tem sido ilustrado no `convert-sql-statement` 4 de exemplo do comando do exemplo de arquivo de script de console.  
  
    > [!NOTE]  
    > Certifique-se de que o argumento de linha de comando do arquivo de valor da variável é passado para o aplicativo de console e VariableValueFileSample.xml é atualizado com o usuário especificado valores.  
  
-   **ConversionAndDataMigrationSample.xml:**  
     Este exemplo permite que o usuário executar uma migração de ponta a ponta da conversão para a migração de dados. A lista de valores de atributo obrigatório que eles terão de alterar é listada abaixo:  
  
    **Nome do comando**  
  
    `map-schema`  
  
    Mapeamento de esquema de banco de dados de origem ao esquema de destino.  
  
    **Atributo**  
  
    -   `source-schema:` Especifica o banco de dados de origem que requer a ser convertido.  
  
    -   `sql-server-schema`: Especifica o banco de dados de destino que deve ser migrados para o  
  
    **Nome do comando**  
  
    `convert-schema`  
  
    1.  Executa a conversão de esquema de origem ao esquema de destino.  
  
    2.  Se o usuário tem que avaliar vários objetos / bancos de dados ele pode especificar vários `metabase-object` nós conforme ilustrado no `convert-schema` 4 de exemplo do comando do exemplo de arquivo de script de console.  
  
    **Atributo**  
  
    `object-name`: Especifique o banco de dados de origem / nome que exige a ser convertido do objeto. Certifique-se de que o correspondente `object-type` é alterada com base no tipo de objeto que é especificado no `object-name`  
  
    **Nome do comando**  
  
    `synchronize-target`  
  
    1.  Sincroniza os objetos de destino com o banco de dados de destino.  
  
    2.  Se o usuário tem que avaliar vários objetos / bancos de dados ele pode especificar vários `metabase-object` nós conforme ilustrado no `synchronize-target` 3 de exemplo do comando do exemplo de arquivo de script de console.  
  
    **Atributo**  
  
    `object-name:` Especifique o banco de dados do sql server / nome que exige a criação do objeto. Certifique-se de que o correspondente `object-type` é alterada com base no tipo de objeto que é especificado no `object-name`  
  
    **Nome do comando**  
  
    `migrate-data`  
  
    1.  Migra os dados de origem para o destino.  
  
    2.  Se o usuário tem que avaliar vários objetos / bancos de dados ele pode especificar vários `metabase-object` nós conforme ilustrado no `migrate-data` 2 do exemplo do comando do exemplo de arquivo de script de console.  
  
    **Atributo**  
  
    `object-name:` Especifica o banco de dados de origem / tabelas nome que exige a serem migrados. Certifique-se de que o correspondente `object-type` é alterada com base no tipo de objeto que é especificado no `object-name`  
  
## <a name="see-also"></a>Consulte também  
[Criando arquivos de valor da variável &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
[Criar os arquivos de Conexão de servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
[Geração de relatórios &#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md)  
  
