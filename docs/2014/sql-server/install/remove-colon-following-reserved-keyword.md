---
title: Palavra-chave reservada da seguir remove dois-pontos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- reserved keywords
ms.assetid: 4f23f7e4-7b4d-4e19-86c9-7527bb8b107d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6f68a641caf21e6cc1dfdefbcb31ff78a1fd8aa6
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583029"
---
# <a name="remove-colon-following-reserved-keyword"></a>Remover dois-pontos após palavra-chave reservada
  O Supervisor de Atualização detectou um script que contém dois-pontos (:) depois de uma palavra-chave reservada. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa sintaxe era ignorada e as instruções eram executadas corretamente. Agora, essa sintaxe faz com que a instrução falhe quando o modo de compatibilidade de banco de dados está definido como 100 ou posterior.  
  
 Os bancos de dados de usuário mantêm o modo de compatibilidade.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes de alterar o modo de compatibilidade do banco de dados para 100 ou posterior, modifique seus scripts removendo os dois-pontos depois das palavras-chave reservadas. Para obter mais informações, consulte ‘sp_dbcmptlevel’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
