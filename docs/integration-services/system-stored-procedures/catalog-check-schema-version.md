---
title: catalog.check_schema_version | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 23746065ca7096b0405114344d4f6a752bfedda1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110463"
---
# <a name="catalogcheckschemaversion"></a>catalog.check_schema_version 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Determina se o esquema de catálogo SSISDB e os binários [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (ISServerExec e SQLCLR assembly) são compatíveis.  
  
 O ISServerExec.exc registra em log uma mensagem de erro quando o esquema e os binários são incompatíveis.  
  
 A versão do esquema de SSISDB é incrementada quando o esquema é alterado durante a aplicação de patches e durante atualizações. É recomendado que você execute este procedimento armazenado depois que um backup de SSISDB tiver sido restaurado para assegurar que o esquema e os binários sejam compatíveis.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.check_schema_version [@use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @use32bitruntime= ] *use32bitruntime*  
 Quando o parâmetro estiver definido como **1**, a versão de 32 bits de dtexec será chamada. O *use32bitruntime* é um **int**.  
  
## <a name="result-set"></a>Conjunto de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige a seguinte permissão:  
  
-   Associação à função de banco de dados **ssis_admin**.  
  
  
