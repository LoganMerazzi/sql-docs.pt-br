---
title: Executar o Console do SSMA (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle SSMA Console
- Script File Commands, Script Generation Commands,Manageability Commands
- Script File Commands,Project Commands
ms.assetid: 7228ccba-c69f-4b4c-8664-01a2750183c5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 210f25b55c2cc2536d4c6f00f215b27eac5f7be0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287224"
---
# <a name="executing-the-ssma-console-oracletosql"></a>Executar o console do SSMA (OracleToSQL)
Microsoft fornece um conjunto robusto de script de comandos de arquivo para executar e controlar atividades do SSMA. O aplicativo de console usa determinados comandos do arquivo de script padrão como enumerado nesta seção.  
  
## <a name="project-script-file-commands"></a>Comandos de arquivo de Script do projeto  
Os comandos de projeto lidar com a criação de projetos, abrir, salvar e sair de projetos.  
  
**Comando**  
  
create-new-project  
                  : Cria um novo projeto SSMA.  
  
**Script**  
  
-   `project-folder` indica a pasta do projeto sendo criado.  
  
-   `project-name` indica o nome do projeto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. {booliano}  
  
-   `project-type:`Atributo opcional. Indica o tipo de projeto ou seja, "sql-server 2005" projeto ou projeto "sql-server-2008" ou "sql-server-2012" projeto ou projeto "sql-server-2014" ou "sql azure". O padrão é "sql-server-2014".  
  
**Exemplo:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
Atributo 'Substituir-if-exists' está **falsos** por padrão.  
  
É o atributo 'tipo de projeto' **sql-server-2008** por padrão.  
  
**Comando**  
  
Abrir projeto: Abre um projeto existente.  
  
**Script**  
  
-   `project-folder` indica a pasta do projeto sendo criado. O comando falhará se a pasta especificada não existe.  {string}  
  
-   `project-name` indica o nome do projeto. O comando falhará se o projeto especificado não existe.  {string}  
  
**Exemplo de sintaxe:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
O SSMA para o aplicativo de Console do Oracle dá suporte à compatibilidade com versões anteriores. Você poderá abrir projetos criados por uma versão anterior do SSMA.  
  
**Comando**  
  
Salvar projeto  
  
Salva o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
close-project  
  
Fecha o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
  
## <a name="database-connection-script-file-commands"></a>Comandos de arquivo de Script de Conexão de banco de dados  
Os comandos de Conexão de banco de dados ajudam a conectar-se ao banco de dados.  
  
-   O **procurar** não há suporte para o recurso da interface do usuário no console.  
  
-   Para obter mais informações sobre 'Criando arquivos de Script', consulte [criando arquivos de Script &#40;OracleToSQL&#41;](../../ssma/oracle/creating-script-files-oracletosql.md).  
  
**Comando**  
  
conectar-se-origem-banco de dados  
  
-   Executa a conexão à fonte de dados e carrega os metadados de nível alto do banco de dados de origem, mas não todos os metadados.  
  
-   Se a conexão à fonte não pode ser estabelecida, um erro será gerado e o aplicativo de console para ainda mais a execução  
  
**Script**  
  
Definição de servidor é recuperada do atributo nome definido para cada conexão na seção servidor de arquivo de conexão do servidor ou o arquivo de script.  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
Force-carga-origem/destino-banco de dados  
  
-   Carrega os metadados da fonte.  
  
-   É útil para trabalhar no projeto de migração off-line.  
  
-   Se a conexão para o origem/destino não puder ser estabelecida, um erro será gerado e o aplicativo de console para ainda mais a execução  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```xml  
<force-load object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
ou em  
  
```xml  
<force-load>  
  
   <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Comando**  
  
reconnect-source-database  
  
-   Reconecta-se à fonte de dados, mas não carrega todos os metadados ao contrário do comando connect-origem-banco de dados.  
  
-   Se não é possível estabelecer (conexão com a fonte de re), um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
connect-target-database  
  
-   Conecta-se para o banco de dados do SQL Server de destino e carrega os metadados de nível alto do banco de dados de destino, mas não os metadados inteiramente.  
  
-   Se a conexão para o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Script**  
  
Definição de servidor é recuperada do atributo nome definido para cada conexão na seção servidor de arquivo de conexão do servidor ou o arquivo de script  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
reconnect-target-database  
  
-   Reconecta-se ao banco de dados de destino, mas não carrega todos os metadados, ao contrário do comando de destino-connect-database.  
  
-   Se a (re) conexão para o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file--commands"></a>Comandos de arquivo de Script de relatório  
Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do Console do SSMA.  
  
**Comando**  
  
generate-assessment-report  
  
-   Gera relatórios de avaliação no banco de dados de origem.  
  
-   Se a conexão de banco de dados de origem não é executada antes de executar esse comando, será gerado um erro e sai do aplicativo de console.  
  
-   Falha ao se conectar ao servidor de banco de dados de origem durante a execução do comando, também resulta em encerrar o aplicativo de console.  
  
**Script**  
  
-   `conversion-report-folder:` Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:` Especifica os objetos considerados para a geração de relatório de avaliação (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **AssessmentReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   assessment-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
ou em  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Comandos de arquivo de Script de migração  
Os comandos de migração converter o esquema de banco de dados de destino para o esquema de origem e migra dados para o servidor de destino.  
  
A saída do console padrão definindo para os comandos de migração é o relatório de saída 'Full' com nenhum relatório de erro detalhada: Resumo somente no nó de raiz da árvore de objeto de origem.  
  
**Comando**  
  
convert-schema  
  
-   Executa a conversão de esquema de origem ao esquema de destino.  
  
-   Se a conexão de banco de dados de origem ou de destino não é executada antes de executar esse comando ou a conexão para o servidor de banco de dados de origem ou destino falha durante a execução do comando, será gerado um erro e sai do aplicativo de console.  
  
**Script**  
  
-   `conversion-report-folder:` Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:` Especifica os objetos de origem considerados para a conversão de esquema (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **SchemaConversionReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<convert-schema  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
ou em  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Comando**  
  
migrate-data  
  
Migra os dados de origem para o destino.  
  
**Script**  
  
-   `conversion-report-folder:` Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:` Especifica os objetos de origem considerados para a migração de dados (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **DataMigrationReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>">  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <data-migration-connection  
  
         source-use-last-used="true"/source-server="<server-unique-name>"  
  
         target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
ou em  
  
```xml  
<migrate-data  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandos de arquivo de Script de preparação de migração  
O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e destino.  
  
**Comando**  
  
map-schema  
  
Mapeamento de esquema de banco de dados de origem ao esquema de destino.  
  
Migra os dados de origem para o destino.  
  
**Script**  
  
-   `source-schema` Especifica o esquema de origem que nossa intenção é migrar.  
  
-   `sql-server-schema` Especifica o esquema de destino onde desejamos a serem migrados.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Comandos de arquivo de Script de capacidade de gerenciamento  
Os comandos de capacidade de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem. A saída do console padrão definindo para os comandos de migração é o relatório de saída 'Full' com nenhum relatório de erro detalhada: Resumo somente no nó de raiz da árvore de objeto de origem.  
  
**Comando**  
  
synchronize-target  
  
-   Sincroniza os objetos de destino com o banco de dados de destino.  
  
-   Se esse comando for executado no banco de dados de origem, um erro for encontrado.  
  
-   Se a conexão de banco de dados de destino não é executada antes de executar esse comando ou a conexão ao servidor de banco de dados de destino falha durante a execução do comando, será gerado um erro e o aplicativo de console é encerrado.  
  
**Script**  
  
-   `object-name:` Especifica os objetos de destino considerados para sincronizar com o banco de dados de destino (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `on-error:` Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Falha-script  
  
-   `report-errors-to:` Especifica o local do relatório de erros para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for dado, em seguida, de arquivos por nome **TargetSynchronizationReport.XML** é criado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
ou em  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
ou em  
  
```xml  
<synchronize-target>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
**Comando**  
  
refresh-from-database  
  
-   Atualiza os objetos de origem do banco de dados.  
  
-   Se esse comando é executado no banco de dados de destino, um erro será gerado.  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
-   `object-name:` Especifica os objetos de origem considerados para a atualização do banco de dados de origem (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `on-error:` Especifica se deve especificar os erros de atualização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Falha-script  
  
-   `report-errors-to:` Especifica o local do relatório de erros para a operação de atualização (atributo opcional) se apenas o caminho da pasta for dado, em seguida, de arquivos por nome **SourceDBRefreshReport.XML** é criado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
ou em  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
ou em  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandos de arquivo de Script de geração de script  
Os comandos de geração de Script executam tarefas duplas: Eles ajudam a salvar o console de saída em um arquivo de script; e registrar a saída do T-SQL para o console ou um arquivo de acordo com o parâmetro que você especificar.  
  
**Comando**  
  
Salvar como script  
  
Usado para salvar os scripts dos objetos em um arquivo mencionado quando metabase Target, essa é uma alternativa ao comando de sincronização, onde podemos obter os scripts e execute o mesmo banco de dados de destino.  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
-   `object-name:` Especifica os objetos cujos scripts serão salvos. (Ele pode ter nomes de objetos individuais ou um nome de objeto de grupo)  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `metabase:` Especifica se ele IO de origem ou destino da metabase.  
  
-   `destination:` Especifica o caminho ou a pasta em que o script foi salvo, se o nome do arquivo não for fornecido, em seguida, um nome de arquivo na. out formato (valor do atributo object_name)  
  
-   `overwrite:` Se for true, em seguida, ele substitui se o mesmo nome de arquivo existe. Ele pode ter os valores (true/false).  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file/folder>"  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
ou em  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file/folder>"  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Comando**  
  
convert-sql-statement  
  
-   `context` Especifica o nome do esquema.  
  
-   `destination` Especifica se a saída deve ser armazenada em um arquivo.  
  
    Se esse atributo não for especificado, a instrução T-SQL convertida é exibida no console. (atributo opcional)  
  
-   `conversion-report-folder` Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `conversion-report-overwrite` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-converted-sql-to` Especifica o caminho da pasta onde o T-SQL convertido deve ser armazenado arquivo (ou). Quando um caminho de pasta é especificado junto com o `sql-files` atributo, cada arquivo de origem terão um criado sob a pasta especificada do arquivo de T-SQL de destino correspondente. Quando um caminho de pasta é especificado junto com o `sql` atributo, o T-SQL convertido é gravado em um arquivo chamado **Result.out** sob a pasta especificada.  
  
-   `sql` Especifica as instruções sql de Oracle a ser convertido, uma ou mais instruções podem ser separados usando um ";"  
  
-   `sql-files` Especifica o caminho dos arquivos de sql que tem a ser convertido em código T-SQL.  
  
-   `write-summary-report-to` Especifica o caminho onde o relatório será gerado. Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **ConvertSQLReport.XML** é criado. (atributo opcional)  
  
    Criação tem 2 mais subcategorias, sobre visualização de relatório.:  
  
    -   erros de relatório (= "true/false", com padrão como "false" (atributos opcionais)).  
  
    -   detalhado (= "true/false", com padrão como "false" (atributos opcionais)).  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   file-name="<file-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
   <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
ou em  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>" (optional)  
  
   verbose="<true/false>" (optional)  
  
   report-errors="<true/false>"  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
ou em  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
  
## <a name="next-step"></a>Próxima etapa  
Para obter informações sobre as opções de linha de comando, consulte [opções de linha de comando no Console do SSMA &#40;OracleToSQL&#41; ](../../ssma/oracle/command-line-options-in-ssma-console-oracletosql.md) .  
  
Para obter informações sobre arquivos de script de console de exemplo, consulte [trabalhando com os arquivos de Script de Console de exemplo &#40;OracleToSQL&#41;](../../ssma/oracle/working-with-the-sample-console-script-files-oracletosql.md)  
  
A próxima etapa depende de seus requisitos de projeto:  
  
-   Para especificar uma senha ou a exportação / importação de senhas, consulte [gerenciamento de senhas &#40;OracleToSQL&#41;](../../ssma/oracle/managing-passwords-oracletosql.md).  
  
-   Para gerar relatórios, consulte [geração de relatórios &#40;OracleToSQL&#41;](../../ssma/oracle/generating-reports-oracletosql.md).  
  
-   Para solucionar problemas no console, consulte [solução de problemas &#40;OracleToSQL&#41;](../../ssma/oracle/troubleshooting-oracletosql.md).  
  
