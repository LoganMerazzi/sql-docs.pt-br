---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 164d71a333c09b076a6e292aa8cd2aeeb3ff464d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62797882"
---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|8443|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SB_DIALOG_WO_CONV_GROUP|  
|Texto da mensagem|A conversa com a ID '%.*ls' e o iniciador %d referencia um grupo de conversa ausente '%.\*ls'. Execute DBCC CHECKDB para analisar e reparar o banco de dados.|  
  
## <a name="explanation"></a>Explicação  
A camada de metadados retornou NULL para o grupo de conversa. O banco de dados foi corrompido de algum modo. Uma possível origem da corrupção é um erro de disco.  
  
## <a name="user-action"></a>Ação do usuário  
Execute DBCC CHECKDB no modo de correção para deixar novamente o banco de dados em um estado consistente. É possível excluir mensagens, se necessário, para restaurar a consistência. Investigue os logs de erros do sistema para saber se o erro foi causado por outra falha no sistema.  
  
