---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e44899e6b586610dc9b18e3ab2e4ec31d4451c1e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048345"
---
# <a name="mssqlserver10539"></a>MSSQLSERVER_10539
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10539|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NO_PLAN_FOR_STMT|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' a partir do cache porque um plano de consulta não está disponível para a instrução com deslocamento inicial %d. Esse problema poderá ocorrer se a instrução depender de objetos do banco de dados que ainda não foram criados. Verifique se todos os objetos de banco de dados necessários existem e execute a instrução antes de criar o guia de plano.|  
  
## <a name="explanation"></a>Explicação  
Não há um plano de consulta disponível no cache de planos para a instrução com o deslocamento inicial especificado.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se todos os objetos de banco de dados necessários existem e execute a instrução antes de criar o guia de plano.  
  
## <a name="see-also"></a>Consulte Também  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
