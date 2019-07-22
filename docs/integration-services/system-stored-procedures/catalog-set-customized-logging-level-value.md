---
title: catalog.set_customized_logging_level_value | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: d83fb763-c7c6-4e20-bd10-0f995598b198
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0146d58a1495ad5c17625edbb9b9c6f2d295cfb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985307"
---
# <a name="catalogsetcustomizedlogginglevelvalue"></a>catalog.set_customized_logging_level_value 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Altera as estatísticas ou os eventos registrados em log por um nível de log personalizado existente. Para obter mais informações sobre níveis de registro em log personalizados, consulte [Registro em Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.set_customized_logging_level_value [ @level_name = ] level_name  
    , [ @property_name = ] property_name  
    , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @level_name = ] *level_name*  
 O nome de um nível de log personalizado existente.  
  
 O *level_name* é **nvarchar(128)** .  
  
 [ @property_name = ] *property_name*  
 O nome da propriedade a ser alterada. Os valores válidos são **PROFILE** e **EVENTS**.  
  
 O *property_name* é **nvarchar(128)** .  
  
 [ @property_value = ] *property_value*  
 O novo valor para a propriedade especificada do nível de log personalizado especificado.  
  
 Para obter uma lista de valores válidos para perfil e eventos, consulte [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md).  
  
 O *property_value* é um **bigint**.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (êxito)  
  
 Quando há falha no procedimento armazenado, ele gera um erro.  
  
## <a name="result-set"></a>Conjunto de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Associação na função de banco de dados **ssis_admin**  
  
-   Associação na função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve as condições que podem provocar falha no procedimento armazenado.  
  
-   O usuário não tem as permissões necessárias.  
  
  
