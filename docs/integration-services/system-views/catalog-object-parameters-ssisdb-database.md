---
title: catalog.object_parameters (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 20253a1bb82bba8b11b24eafbc1c26010abdeb27
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65714680"
---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe os parâmetros para todos os pacotes e projetos no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|O ID (identificador exclusivo) do parâmetro.|  
|project_id|**bigint**|O ID exclusivo do projeto.|  
|object_type|**smallint**|O tipo do parâmetro. O valor é `20` para um parâmetro de projeto e o valor é `30` para um parâmetro de pacote.|  
|object_name|**sysname**|O nome do projeto ou pacote correspondente.|  
|parameter_name|**sysname(nvarchar(128))**|O nome do parâmetro.|  
|data_type|**nvarchar(128)**|O tipo de dados do parâmetro.|  
|required|**bit**|Quando o valor é `1`, o valor do parâmetro é necessário para iniciar a execução. Quando o valor é `0`, o valor de parâmetro não é necessário para iniciar a execução.|  
|sensitive|**bit**|Quando o valor é `1`, o valor do parâmetro é confidencial. Quando o valor é `0`, o valor do parâmetro não é confidencial.|  
|descrição|**nvarchar(1024)**|Uma descrição opcional do pacote.|  
|design_default_value|**sql_variant**|O valor padrão para o parâmetro que foi atribuído durante o design do projeto ou pacote.|  
|default_value|**sql_variant**|O valor padrão que é usado atualmente no servidor.|  
|value_type|**char(1)**|Indica o tipo de valor do parâmetro. Este campo exibe `V` quando parameter_value é um valor literal e `R` quando o valor é atribuído referenciando uma variável de ambiente.|  
|value_set|**bit**|Quando o valor é `1`, o valor do parâmetro foi atribuído. Quando o valor é `0`, o valor do parâmetro não foi atribuído.|  
|referenced_variable_name|**nvarchar(128)**|O nome da variável de ambiente que é atribuída ao valor do parâmetro. O valor padrão é **NULL**.|  
|validation_status|**char(1)**|Identificado apenas para fins informativos. Não é usado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|last_validation_time|**datetimeoffset(7)**|Identificado apenas para fins informativos. Não é usado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="permissions"></a>Permissões  
 Para consultar linhas nesta exibição, você deve ter uma das permissões a seguir:  
  
-   Permissão READ no projeto  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação na função de servidor **sysadmin**.  
  
 A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
