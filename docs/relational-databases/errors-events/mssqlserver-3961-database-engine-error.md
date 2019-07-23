---
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9b89aab7a129aec5fcae840086b140f6975a8c99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043512"
---
# <a name="mssqlserver3961"></a>MSSQLSERVER_3961
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3961|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|XACT_METADATA_INVALID|  
|Texto da mensagem|Falha na transação de isolamento de instantâneo no banco de dados '%.*ls' porque o objeto acessado pela instrução foi modificado por uma instrução DDL em outra transação simultânea desde o início dessa transação.  Isso não é permitido porque os metadados não têm controle de versão. Uma atualização simultânea para metadados poderia gerar inconsistências se misturada com isolamento de instantâneo.|  
  
## <a name="explanation"></a>Explicação  
Esse erro pode ocorrer se você estiver consultando metadados sob isolamento do instantâneo e tiver uma instrução DDL simultânea que atualiza os metadados que estão sendo acessados sob isolamento do instantâneo. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem suporte para controle de versão de metadados. Por isso, há restrições nas operações DDL que podem ser executadas em uma transação explícita que está sendo executada sob isolamento do instantâneo. Uma transação implícita, por definição, é uma instrução única que torna possível impor semânticas de isolamento do instantâneo, até mesmo com instruções DDL. As instruções DDL a seguir não são permitidas sob o isolamento de instantâneo após uma instrução BEGIN TRANSACTION: ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME ou qualquer instrução DDL do CLR (common language runtime). Essas instruções são permitidas quando você está usando isolamento do instantâneo em transações implícitas. Uma transação implícita, por definição, é uma instrução única que torna possível impor semânticas de isolamento do instantâneo, até mesmo com instruções DDL.  
  
## <a name="user-action"></a>Ação do usuário  
Altere o nível de isolamento do instantâneo a um nível de isolamento de não instantâneo como leitura confirmada antes de consultar os metadados.  
  
