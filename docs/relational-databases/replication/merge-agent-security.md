---
title: Segurança do Agente de Mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.MA.f1
helpviewer_keywords:
- Merge Agent Security dialog box
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 45cc5e8c2ca3e311704ffd4eb6577d2e934d484a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140718"
---
# <a name="merge-agent-security"></a>Segurança do Merge Agent
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A caixa de diálogo **Segurança do Merge Agent** permite especificar a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o Merge Agent é executado. O Merge Agent é executado no Distribuidor para assinaturas push e no Assinante para assinaturas pull. A conta do Windows é também referida como *conta do processo*, porque o processo do agente é executado nessa conta. Opções adicionais disponíveis na caixa de diálogo dependem de como você a acessa:  
  
-   Se a caixa de diálogo for acessada do Assistente para Nova Assinatura, também permitirá que você especifique o contexto no qual o Merge Agent fará conexões com o Assinante (para assinaturas push) ou com o Publicador e o Distribuidor (para assinaturas pull). A conexão pode ser feita usando a conta Windows ou no contexto de uma conta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada.  
  
-   Se a caixa de diálogo for acessada pela caixa de diálogo **Propriedades da Assinatura** , especifique o contexto no qual o Merge Agent fará conexões ao clicar no botão de propriedades ( **...** ) na linha **Conexão do Assinante** ou **Conexão do Publicador** daquela caixa de diálogo. Para obter mais informações sobre como acessar a caixa de diálogo **Propriedades da Assinatura**, confira [Exibir e modificar propriedades da assinatura push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e como [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Todas as contas devem ser válidas, com a senha correta especificada para cada conta. Contas e senhas não são validadas até que um agente seja executado.  
  
## <a name="options"></a>Opções  
 **Process Account**  
 Insira uma conta Windows na qual o Merge Agent é executado.  
  
-   Para assinaturas push, a conta deve:  
  
    -   Ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.  
  
    -   Ser um membro da PAL.  
  
    -   Ser um logon associado a um usuário no banco de dados de publicação.  
  
    -   Ter permissões de leitura no compartilhamento de instantâneo.  
  
-   Para assinaturas pull, a conta deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de assinatura.  
  
 Serão requeridas permissões adicionais se a conta do processo for representada quando as conexões forem feitas. Consulte as seções **Conectar ao Publicador e ao Distribuidor** e **Conectar ao Assinante** a seguir.  
  
 **Process Account** não pode ser especificada para assinaturas pull para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], porque o Merge Agent não é executado em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
 **Senha** e **Confirmar Senha**  
 Insira a senha para a conta do Windows.  
  
 **Conectar ao Publicador e ao Distribuidor**  
 Para assinaturas push, as conexões com o Publicador e o Distribuidor são sempre feitas representando a conta especificada na caixa de texto **Conta do processo** .  
  
 Para assinaturas pull, selecione se o Merge Agent deve fazer conexões com o Publicador e o Distribuidor representando a conta especificada na caixa de texto **Conta do processo** ou usando uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda a seleção para representar a conta do Windows em vez de usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para a conexão deve:  
  
-   Ser um membro da PAL.  
  
-   Ser um logon associado a um usuário no banco de dados de publicação.  
  
-   Ser um logon associado a um usuário no banco de dados de distribuição (o usuário pode ser o usuário Convidado).  
  
-   Ter permissões de leitura no compartilhamento de instantâneo.  
  
 **Conectar ao Assinante**  
 Para assinaturas pull, as conexões com o Assinante são sempre feitas representando a conta especificada na caixa de texto **Conta do processo** .  
  
 Para assinaturas push, selecione se o Merge Agent deve fazer conexões com o Publicador e o Distribuidor representando a conta especificada na caixa de texto **Conta do processo** ou usando uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você optar por usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , insira um logon e uma senha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  É recomendável a seleção para representar a conta do Windows em vez de usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A conta do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para conexão com o Assinante deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de assinatura.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar logons e senhas na replicação](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modelo de segurança do agente de replicação](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
