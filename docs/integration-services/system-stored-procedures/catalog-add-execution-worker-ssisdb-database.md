---
title: catalog.add_execution_worker (Banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
author: janinezhang
ms.author: janinez
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 5dc8e4283a8443c41be994745310114587712e3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110550"
---
# <a name="catalogaddexecutionworker-ssisdb-database"></a>catalog.add_execution_worker (Banco de dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Adiciona um Trabalho do Scale Out do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a uma instância de execução no Scale Out.

## <a name="syntax"></a>Sintaxe

```sql
catalog.add_execution_worker [@execution_id = ] execution_id, [@workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>Argumentos
[ @execution_id = ] *execution_id*  
 O identificador exclusivo da instância de execução. O *execution_id* é **bigint**.  
 
[@workeragent_id = ] *workeragent_id*  
A ID do agente de trabalho de um Trabalho do Scale Out. O *workeragent_id* é **uniqueIdentifier**.

## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  

## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e MODIFY na instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
 
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
 
- O usuário não tem as permissões apropriadas.

- O identificador da execução não é válido.

- A ID do agente de trabalho não é válida.

- A execução não está no Scale Out.

## <a name="see-also"></a>Consulte Também
[Execute pacotes no Scale Out](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md).

