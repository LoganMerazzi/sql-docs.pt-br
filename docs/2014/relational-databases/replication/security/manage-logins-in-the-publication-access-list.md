---
title: Gerenciar logons na Lista de Acesso à Publicação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server replication], publication access list
- publications [SQL Server replication], publication access lists
- publication access list (PAL)
- PAL (publication access list)
- logins [SQL Server replication], managing
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 966b8a03d10bb8e87950e19e3e099954e8aaad8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62960929"
---
# <a name="manage-logins-in-the-publication-access-list"></a>Gerenciar logons na lista de acesso à publicação
  Este tópico descreve como gerenciar logons na Lista de Acesso à Publicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O acesso a uma publicação é controlado pela PAL (lista de acesso à publicação). É possível adicionar e remover logons e grupos do PAL.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
-   **Para gerenciar logons na Lista de Acesso à Publicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve associar o logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com um usuário de banco de dados no banco de dados de publicação antes de adicionar o logon à PAL.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Use a PAL (lista de acesso à publicação) na página **Lista de Acesso à Publicação** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** para gerenciar logons. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar as propriedades da publicação](../publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-manage-logins-in-the-pal"></a>Para gerenciar logons na PAL  
  
1.  Na página **Lista de Acesso à Publicação** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, use os botões **Adicionar**, **Remover** e **Remover Tudo** para adicionar e remover logons e grupos da PAL. Não remova o **distributor_admin** da PAL. Essa conta é usada para replicação.  
  
    > [!NOTE]  
    >  Se for usado um Distribuidor remoto, as contas da PAL precisarão estar disponíveis tanto no Publicador quanto no Distribuidor. A conta ou deve ser uma conta de domínio ou uma conta local que é definida em ambos os servidores. As senhas associadas a ambos os logons devem ser as mesmas.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-groups-and-logins-that-belong-to-the-pal"></a>Para exibir grupos e logons que pertencem à PAL  
  
1.  No Publicador do banco de dados da publicação, execute [sp_help_publication_access](/sql/relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql). Para **@publication**, especifique o nome da publicação. Isso exibe informações sobre os grupos e logons na PAL.  
  
#### <a name="to-add-groups-and-logins-to-the-pal"></a>Para adicionar grupos e logons à PAL  
  
1.  No Publicador do banco de dados da publicação, execute [sp_grant_publication_access](/sql/relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql). Para **@publication**especifique o nome da publicação e para **@login**especifique o nome do logon ou grupo que está sendo adicionado.  
  
#### <a name="to-remove-groups-and-logins-from-the-pal"></a>Para remover grupos e logons da PAL  
  
1.  No Publicador do banco de dados da publicação, execute [sp_revoke_publication_access](/sql/relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql). Para **@publication**especifique o nome da publicação e para **@login**especifique o nome do logon ou grupo que está sendo removido.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de segurança do agente de replicação](replication-agent-security-model.md)   
 [Proteger uma topologia de replicação](view-and-modify-replication-security-settings.md)   
 [Proteger o Publicador](secure-the-publisher.md)  
  
  
