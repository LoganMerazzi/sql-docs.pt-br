---
title: "Procedimentos (catálogo do Integration Services) armazenados | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- stored procedures [Integration Services]
ms.assetid: a6ccd884-108f-4fb6-95ad-00b9cb65d5d6
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 21715bf65f3a85669dfe823511ddb9b6c2dd4d57
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="stored-procedures-integration-services-catalog"></a>Procedimentos armazenados (Catálogo do Integration Services)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta seção descreve os procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] disponíveis para administrar projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] implantados a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Chamar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] procedimentos armazenados para adicionar, remover, modificar ou executar objetos armazenados na **SSISDB** catálogo.  
  
 O nome padrão do catálogo é SSISDB. Os objetos armazenados no catálogo incluem projetos, pacotes, parâmetros, ambientes e histórico operacional.  
  
 Você também pode usar as exibições de banco de dados e chamar os procedimentos armazenados diretamente, ou escrever código personalizado que chame a API gerenciada. O [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e a API gerenciada consultam as exibições e chamam os procedimentos armazenados descritos nesta seção para executar muitas de suas tarefas.  
  
## <a name="in-this-section"></a>Nesta seção  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
 Adiciona um toque de dados à saída de um componente em um fluxo de dados de pacote.  
  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
 Adiciona um toque de dados a um caminho de fluxo de dados específico em um fluxo de dados de pacote.  
  
 [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)  
 Determina se o esquema de catálogo SSISDB e os binários [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (ISServerExec e SQLCLR assembly) são compatíveis.  
  
 [Catalog. clear_object_parameter_value &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)  
 Limpa o valor de um parâmetro para um projeto ou pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] existente armazenado no servidor.  
  
 [Catalog. configure_catalog &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)  
 Configura o catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] definindo uma propriedade de catálogo como um valor especificado.  
  
 [catalog.create_environment &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
 Cria um ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_environment_reference &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
 Cria uma referência de ambiente para um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_environment_variable &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
 Cria uma variável de ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. create_execution &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)  
 Cria uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
 Faz com que a execução de um pacote seja pausada e crie um arquivo de despejo.  
  
 [catalog.create_folder &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
 Cria uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_environment &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
 Exclui um ambiente de uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_environment_reference &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
 Exclui uma referência de ambiente de um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_environment_variable &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
 Exclui uma variável de um ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_folder &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
 Exclui uma pasta do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
 Exclui um projeto existente de uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. deny_permission &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)  
 Nega uma permissão em um objeto protegível no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.deploy_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
 Implanta um projeto a uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou atualiza um projeto existente que foi implantado anteriormente.  
  
 [Catalog. get_parameter_values &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)  
 Resolve e recupera os valores de parâmetro padrão de um projeto e os pacotes correspondentes no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.get_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
 Recupera as propriedades de um projeto existente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. grant_permission &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
 Concede uma permissão em um objeto protegível no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.move_environment &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
 Move um ambiente de uma pasta para outra no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.move_project &#40;&#40;Banco de dados SSISDB&#41;](../Topic/catalog.move_project%20\(\(SSISDB%20Database\).md)  
 Move um projeto de uma pasta para outra no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md)  
 Remove um toque de dados de uma saída de componente que está em uma execução.  
  
 [catalog.rename_environment &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
 Renomeia um ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.rename_folder &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
 Renomeia uma pasta no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.restore_project &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
 Restaura um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para uma versão anterior.  
  
 [Catalog. revoke_permission &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)  
 Revoga uma permissão em um objeto protegível no catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_property &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
 Define a propriedade de um ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_reference_type &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
 Define o tipo de referência e o nome de ambiente associados a uma referência de ambiente existente para um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_variable_property &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
 Define a propriedade de uma variável de ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. set_environment_variable_protection &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)  
 Define o bit de sensibilidade de uma variável de ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_variable_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
 Define o valor de uma variável de ambiente no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_execution_parameter_value &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Define o valor de um parâmetro para uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_execution_property_override_value](../../integration-services/system-stored-procedures/catalog-set-execution-property-override-value.md)  
 Define o valor de uma propriedade para uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_folder_description &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
 Define a descrição de uma pasta do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. set_object_parameter_value &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)  
 Define o valor de um parâmetro no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Associa o valor a uma variável de ambiente ou atribui um valor literal que será usado por padrão se nenhum outro valor for atribuído.  
  
 [Catalog. start_execution &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)  
 Inicia uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md)  
 Executa a manutenção do estado das operações para o catálogo SSISDB.  
  
 [Catalog. stop_operation &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)  
 Para uma validação ou instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. validate_package &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)  
 De forma assíncrona, valida um pacote no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. validate_project &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)  
 De forma assíncrona, valida um projeto no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
[Catalog.add_execution_worker &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)   
Adiciona um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala Out trabalho a uma instância de execução em expansão.

[Catalog.enable_worker_agent &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)   
Habilitar um trabalho de fora de escala para escala Out mestre funcionam com essa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catálogo.

[Catalog.disable_worker_agent &#40; Banco de dados SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)   
Desabilitar um trabalho de fora de escala para escala Out mestre funcionam com essa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catálogo.


