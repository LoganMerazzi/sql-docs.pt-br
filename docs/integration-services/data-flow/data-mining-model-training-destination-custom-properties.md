---
title: Propriedades personalizadas do destino do treinamento do modelo de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f0a70216-fdac-44ae-af29-35f65626217c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 028aceabe89183d4aec0c75606f6fe58c91192d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049463"
---
# <a name="data-mining-model-training-destination-custom-properties"></a>Propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O destino Treinamento do Modelo de Mineração de Dados tem propriedades personalizadas e as propriedades comum a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|ASConnectionId|Cadeia de caracteres|O identificador exclusivo do gerenciador de conexões.|  
|ASConnectionString|Cadeia de caracteres|A cadeia de caracteres de conexão com uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|ObjectRef|Cadeia de caracteres|Uma marca XML que identifica a estrutura de mineração de dados usada pela transformação.|  
  
 A entrada e as colunas de entrada do destino Treinamento do Modelo de Mineração de Dados não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de treinamento do modelo de Data Mining](../../integration-services/data-flow/data-mining-model-training-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
