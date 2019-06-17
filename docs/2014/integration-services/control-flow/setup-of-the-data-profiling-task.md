---
title: Configuração da Tarefa Criação de Perfil de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], configuring
ms.assetid: fe050ca4-fe45-43d7-afa9-99478041f9a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1d2378426a3cd55b6df183cac7782d63578e2ed0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830188"
---
# <a name="setup-of-the-data-profiling-task"></a>Configuração da tarefa Criação de Perfil de Dados
  Antes de rever um perfil dos dados de origem, a primeira etapa é configurar e executar a tarefa Criação de Perfil de Dados. Você cria esta tarefa dentro de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para configurar a tarefa Criação de Perfil de Dados, use o Editor da Tarefa Criação de Perfil de Dados. Este editor permite selecionar onde produzir os perfis e quais perfis devem ser calculados. Depois de configurar a tarefa, você executa o pacote para calcular os perfis de dados.  
  
## <a name="requirements-and-limitations"></a>Requisitos e limitações  
 A tarefa Criação de Perfil de Dados funciona apenas com dados armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ela não funciona com fontes de dados de terceiros ou baseadas em arquivos.  
  
 Além disso, para executar um pacote que contém a tarefa Criação de Perfil de Dados, você deve usar uma conta que tem permissões de leitura/gravação, inclusive permissões CREATE TABLE, no banco de dados tempdb.  
  
## <a name="data-profiling-task-in-a-package"></a>Tarefa Criação de Perfil de Dados em um pacote  
 A tarefa Criação de Perfil de Dados apenas configura os perfis e cria o arquivo de saída que contém os perfis calculados. Para revisar esse arquivo de saída, você deve usar o Visualizador de Perfil de Dados, um programa de visualização autônomo. Como é necessário exibir a saída separadamente, você deve usar a tarefa Criação de Perfil de Dados em um pacote que não contém outras tarefas.  
  
 No entanto, você não tem de usar a tarefa Criação de Perfil de Dados como a única do pacote. Se você quiser criar perfis de dados no fluxo de trabalho ou no fluxo de dados de um pacote mais complexo, deverá usar as seguintes opções:  
  
-   Para implementar a lógica condicional baseada no arquivo de saída da tarefa, no fluxo de controle do pacote, coloque a tarefa Script após a tarefa Criação de Perfil de Dados. Dessa forma, você poderá usar essa tarefa Script para consultar o arquivo de saída.  
  
-   Para criar perfis de dados no fluxo de dados depois que os dados tiverem sido carregados e transformados, é necessário salvar os dados alterados em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] temporariamente. Em seguida, você poderá criar um perfil dos dados salvos.  
  
 Para obter informações, consulte [Incorporar uma tarefa Criação de Perfil de Dados no fluxo de trabalho do pacote](incorporate-a-data-profiling-task-in-package-workflow.md).  
  
## <a name="setup-of-the-task-output"></a>Configuração da saída da tarefa  
 Após a execução da tarefa Criação de Perfil de Dados em um pacote, você deve configurar a saída dos perfis que a tarefa computará. Para configurar a saída para os perfis, use a página **Geral** do Editor da Tarefa Criação de Perfil de Dados. Além de especificar o destino da saída, a página **Geral** também oferece a habilidade para executar um perfil rápido dos dados. Quando você seleciona **Perfil Rápido**, a tarefa Criação de Perfil de Dados cria o perfil de uma tabela ou exibição usando alguns ou todos os perfis padrão com suas configurações padrão.  
  
 Para obter mais informações, consulte [Editor da tarefa Criação de Perfil de Dados &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md) e [Formulário de Perfil Rápido de Tabela Única &#40;Tarefa Criação de Perfil de Dados&#41;](data-profiling-task.md).  
  
> [!IMPORTANT]  
>  O arquivo de saída pode conter dados confidenciais sobre seu banco de dados e os dados contidos no banco de dados. Para obter sugestões sobre como tornar esse arquivo mais seguro, consulte [Acesso aos arquivos usados por pacotes](../access-to-files-used-by-packages.md).  
  
## <a name="selection-and-configuration-of-the-profiles-to-be-computed"></a>Seleção e configuração dos perfis a serem calculados  
 Depois de configurar o arquivo de saída, você precisa selecionar os perfis de dados a serem calculados. A tarefa Criação de perfil de dados pode computar oito perfis de dados diferentes. Cinco desses perfis analisam colunas individuais e os três restantes analisam diversas colunas ou relações entre colunas e tabelas. Em uma tarefa Criação de Perfil de Dados simples, você pode calcular várias perfis para várias colunas ou combinações de colunas em várias tabelas ou exibições.  
  
 A tabela a seguir descreve os relatórios calculados por cada um desses perfis e os tipos de dados para os quais o perfil é válido.  
  
|Para calcular|Qual ajuda identificar|Use este perfil|  
|----------------|-------------------------|----------------------|  
|Todos os comprimentos de valores de cadeia de caracteres na coluna selecionada e a porcentagem de linhas na tabela que cada comprimento representa.|**Valores de cadeias de caracteres que não são válidos** – por exemplo, você cria o perfil de uma coluna que deve usar dois caracteres para códigos de estados nos Estados Unidos, mas descobre valores maiores que dois caracteres.|**Distribuição de comprimento de coluna -** válido para uma coluna com um desses tipos de dados:<br /><br /> Tipos de dados de caracteres: `char`, `nchar`, `varchar` e `nvarchar`|  
|Um conjunto de expressões regulares que cobrem a porcentagem especificada de valores em uma coluna de cadeia de caracteres.<br /><br /> Além disso para localizar expressões regulares que podem ser usadas no futuro para validar valores novos|**Valores de cadeias de caracteres que não são válidos ou não estão no formato correto** – por exemplo, um perfil padrão de uma coluna CEP/Código Postal pode produzir as expressões regulares: \d{5}-\d{4}, \d{5} e \d{9}. Se a saída contém outras expressões regulares, os dados conterão valores inválidos ou que estarão em um formato incorreto.|**Perfil de padrão de coluna -** válido para uma coluna com um desses tipos de dados:<br /><br /> Tipos de dados de caracteres: `char`, `nchar`, `varchar` e `nvarchar`|  
|A porcentagem de valores nulos na coluna selecionada.|**Razão alta de valores nulos inesperada em uma coluna** – por exemplo, você cria o perfil de uma coluna que deve conter CEPs dos Estados Unidos, mas descobre um alto percentual inesperada de CEPs ausentes.|**Coluna nula taxa -** válido para uma coluna com esses tipos de dados:<br /><br /> Qualquer tipo de dados. Isso inclui `image`, `text`, `xml`, tipos definidos pelo usuário e tipos de variável.|  
|Estatísticas como mínimo, máximo, média e desvio padrão para colunas numéricas, além de mínimo e máximo para colunas `datetime`.|**Valores numéricos e datas que não são válidos** – por exemplo, você cria o perfil de uma coluna de datas históricas e descobre uma data de máximo que está no futuro.|**Perfil de estatísticas de coluna -** válido para uma coluna com um desses tipos de dados:<br /><br /> Tipos de dados numéricos: tipos Integer (exceto `bit`), `money`, `smallmoney`, `decimal`, `float`, `real` e `numeric`<br /><br /> Tipos de dados de data e hora: `datetime`, `smalldatetime`, `timestamp`, `date`, `time`, `datetime2` e `datetimeoffset`<br />Observação: No caso de uma coluna que tem um tipo de dados de data e hora, o perfil calcula apenas mínimo e máximo.|  
|Todos os valores distintos na coluna selecionada e a porcentagem de linhas na tabela que cada valor representa. Ou, os valores que representam mais de uma porcentagem especificada na tabela.|**Um número incorreto de valores distintos em uma coluna** – por exemplo, você cria o perfil de uma coluna que contém estados dos Estados Unidos e descobre mais de 50 valores distintos.|**Distribuição de valor de coluna -** válido para uma coluna com um desses tipos de dados:<br /><br /> Tipos de dados numéricos: tipos Integer (exceto `bit`), `money`, `smallmoney`, `decimal`, `float`, `real` e `numeric`<br /><br /> Tipos de dados de caracteres: `char`, `nchar`, `varchar` e `nvarchar`<br /><br /> Tipos de dados de data e hora: `datetime`, `smalldatetime`, `timestamp`, `date`, `time`, `datetime2` e `datetimeoffset`|  
|Se uma coluna ou conjunto de colunas é uma chave, ou uma chave aproximada, para a tabela selecionada.|**Valores duplicados em uma possível coluna de chave** – por exemplo, você cria o perfil para as colunas Nome e Endereço em uma tabela Clientes e descobre valores duplicados em que as combinações de nome e endereço devem ser exclusivas.|**Chave Candidata** – um perfil de várias colunas que informa se uma coluna ou um conjunto de colunas é apropriado para servir como uma chave para a tabela selecionada. Válido para colunas com um destes tipos de dados:<br /><br /> Tipos de dados Integer: `bit`, `tinyint`, `smallint`, `int` e `bigint`<br /><br /> Tipos de dados de caracteres: `char`, `nchar`, `varchar` e `nvarchar`<br /><br /> Tipos de dados de data e hora: `datetime`, `smalldatetime`, `timestamp`, `date`, `time`, `datetime2` e `datetimeoffset`|  
|A extensão de valores em uma coluna (a coluna dependente) que dependem dos valores em uma outra coluna ou conjunto de colunas (a coluna determinante).|**Valores que não são válidos em colunas dependentes** – por exemplo, você cria o perfil da dependência entre uma coluna que contém CEPs dos Estados Unidos e uma coluna que contém estados dos Estados Unidos. O mesmo CEP deve ter sempre o mesmo estado. Porém, o perfil descobre violações da dependência.|**Dependência funcional -** válido para colunas com um desses tipos de dados:<br /><br /> Tipos de dados Integer: `bit`, `tinyint`, `smallint`, `int` e `bigint`<br /><br /> Tipos de dados de caracteres: `char`, `nchar`, `varchar` e `nvarchar`<br /><br /> Tipos de dados de data e hora: `datetime`, `smalldatetime`, `timestamp`, `date`, `time`, `datetime2` e `datetimeoffset`|  
|Se uma coluna ou um conjunto de colunas é apropriado para servir como uma chave estrangeira entre as tabelas selecionadas.<br /><br /> Isto é, este perfil informa a sobreposição nos valores entre duas colunas ou dois conjuntos de colunas.|**Valores que não são válidos** – por exemplo, você cria o perfil da coluna ProductID de uma tabela Vendas. O perfil descobre que a coluna contém valores que não são encontrados na coluna ProductID da tabela Produtos.|**Inclusão de Valor** – válido para colunas com um destes tipos de dados:<br /><br /> Tipos de dados Integer: `bit`, `tinyint`, `smallint`, `int` e `bigint`<br /><br /> Tipo de dados de caracteres: `char`, `nchar`, `varchar` e `nvarchar`<br /><br /> Tipos de dados de data e hora: `datetime`, `smalldatetime`, `timestamp`, `date`, `time`, `datetime2` e `datetimeoffset`|  
  
 Para selecionar quais perfis devem ser calculados, use a página **Solicitações de Perfil** do Editor da Tarefa Criação de Perfil de Dados. Para obter mais informações, consulte [Editor da Tarefa Criação de Perfil de Dados &#40;Profile Requests Page&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Na página **Solicitação de Perfil** , você especifica também a origem de dados e configura os perfis de dados. Ao configurar a tarefa, pense nas seguintes informações:  
  
-   Para simplificar a configuração e facilitar o descobrimento das características de dados pouco conhecidos, você pode usar o curinga, **(\*)** , no lugar do nome de uma coluna específica. Se você usar este curinga, a tarefa criará o perfil de todas as colunas que tiverem um tipo de dados apropriado, o que por sua vez poderá tornar o processamento mais lento.  
  
-   Quando a tabela ou exibição selecionada estiver vazia, a tarefa de Criação de perfis de dados não computará nenhum perfil.  
  
-   Quando todos os valores na coluna selecionada forem nulos, a tarefa Criação de Perfil de dados calculará somente o Perfil de Razão Nula da Coluna. Ela não calcula o Perfil de Distribuição de Comprimento de Coluna, o Perfil de Padrão de Coluna, o Perfil de Estatísticas de Coluna ou o Perfil de Distribuição de Valor de Coluna para a coluna vazia.  
  
 Cada um dos perfis de dados disponíveis tem as próprias opções de configuração. Para obter mais informações sobre essas opções, consulte os tópicos a seguir:  
  
-   [Opções da solicitação de perfil Chave de Candidato &#40;tarefa Criação de Perfil de Dados&#41;](candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação de perfil Distribuição de Tamanho de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Razão Nula de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Padrão de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Estatísticas de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [Opções de solicitação do perfil Distribuição de Valor de Coluna &#40;Tarefa Criação de Perfil de Dados&#41;](column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Dependência Funcional &#40;Tarefa Criação de Perfil de Dados&#41;](functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [Opções da solicitação do perfil Inclusão de Valor &#40;Tarefa Criação de Perfil de Dados&#41;](value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="execution-of-the-package-that-contains-the-data-profiling-task"></a>Execução do pacote que contém a tarefa Criação de Perfil de Dados  
 Depois de configurar a tarefa Criação de Perfil de Dados, você poderá executá-la. A tarefa, então, calculará os perfis de dados e produzirá essa informação em formato XML a um arquivo ou uma variável de pacote. A estrutura desse XML seguirá o esquema DataProfile.xsd. O esquema poderá ser aberto no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou em outro editor de esquemas, em um editor XML ou em um editor de texto, como o Bloco de Notas. Esse esquema de informações de qualidade de dados pode ser útil para as seguintes finalidades:  
  
-   Para trocar informações de qualidade de dados dentro e entre organizações.  
  
-   Para criar ferramentas personalizadas que trabalhem com informações de qualidade de dados.  
  
 O namespace de destino é identificado no esquema como [https://schemas.microsoft.com/sqlserver/2008/DataDebugger/](https://schemas.microsoft.com/sqlserver/2008/DataDebugger/).  
  
## <a name="next-step"></a>Próxima etapa  
 [Visualizador de Perfil de Dados](data-profile-viewer.md).  
  
  
