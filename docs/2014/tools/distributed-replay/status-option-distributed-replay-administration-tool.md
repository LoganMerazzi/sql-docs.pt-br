---
title: Opção de status (ferramenta de administração do Distributed Replay) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42e06144f35ab2db8f124dddff74fb836b6d9c4c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150361"
---
# <a name="status-option-distributed-replay-administration-tool"></a>Opção de status (ferramenta de administração do Distributed Replay)
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ferramenta de administração do Distributed Replay, `DReplay.exe`, é uma ferramenta de linha de comando que você pode usar para se comunicar com o distributed replay controller. Este tópico descreve a opção de linha de comando **status** e a sintaxe correspondente.  
  
 A opção **status** consulta o controlador e exibe o status atual.  
  
 ![Ícone de link do tópico](../../database-engine/media/topic-link.gif "Ícone de link do tópico") Para obter mais informações sobre as convenções de sintaxe usadas com a sintaxe da ferramenta de administração, confira [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dreplay status [-mcontroller] [-fstatus_interval]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 **-m** *controller*  
 Especifica o nome do computador do controlador. Você pode usar "`localhost`" ou "`.`" para fazer referência ao computador local.  
  
 Se o parâmetro **-m** não for especificado, será usado o computador local.  
  
 **-f** *status_interval*  
 Especifica a frequência (em segundos) na qual exibir o status.  
  
 Se o parâmetro **-f** não for especificado, o intervalo padrão será de 30 segundos.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o status atual é exibido a cada 60 segundos. O valor `localhost` indica que o serviço do controlador está em execução no mesmo computador que a ferramenta de administração.  
  
```  
dreplay status -m localhost -f 60  
```  
  
## <a name="permissions"></a>Permissões  
 Você deve executar a ferramenta de administração como um usuário interativo, um usuário local ou uma conta de usuário de domínio. Para usar uma conta de usuário local, a ferramenta de administração e o controlador devem estar em execução no mesmo computador.  
  
 Para saber mais, confira [Distributed Replay Security](distributed-replay-security.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
