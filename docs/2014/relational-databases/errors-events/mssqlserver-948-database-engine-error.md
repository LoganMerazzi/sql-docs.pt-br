---
title: MSSQLSERVER_948 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "948"
helpviewer_keywords:
- 948 (Database Engine error)
ms.assetid: 95c4ad45-a518-4165-a5c4-6e6b932b0570
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b3d55dca978b4383a1a28b0103750b42a294095f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62912561"
---
# <a name="mssqlserver948"></a>MSSQLSERVER_948
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|948|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NA|  
|Texto da mensagem|O banco de dados '%.*ls' não pode ser aberto porque sua versão é a %d. Esse servidor oferece suporte à versão %d e anteriores. Não há suporte para um caminho de downgrade.|  
  
## <a name="explanation"></a>Explicação  
 Determinados recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] afetam a estrutura dos arquivos de banco de dados. Quando você anexa um banco de dados a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível que o formato de arquivo não seja compatível com uma versão diferente do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Por exemplo, esse erro pode ser causado pelo uso de um formato de armazenamento vardecimal em uma versão posterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, depois, pela tentativa de anexar os arquivos de banco de dados a uma versão anterior a do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2.  
  
## <a name="user-action"></a>Ação do usuário  
 Determine a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo executada no servidor de origem. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ou o servidor com o botão direito e, em seguida, clique em **Properties** ou tipo `SELECT @@VERSION` em uma janela de consulta. Abra o banco de dados usando a versão original do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Investigue os recursos habilitados no banco de dados original na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Modifique essas configurações para trabalhar com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual será anexado o banco de dados.  
  
  
