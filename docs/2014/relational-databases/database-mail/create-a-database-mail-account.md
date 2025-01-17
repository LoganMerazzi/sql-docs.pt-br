---
title: Criar uma conta de email do Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], accounts
- accounts [Database Mail]
ms.assetid: c07abbc6-fc6a-470b-8fa3-532f2e06b16a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a286c7d4c0ff42389830713a6c42c89a7273f1d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917723"
---
# <a name="create-a-database-mail-account"></a>Criar uma conta do Database Mail
  Use o **Assistente para Configuração do Database Mail** ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar uma conta do Database Mail.  
  
-   **Antes de começar:**  [Pré-requisitos](#Prerequisites)  
  
-   **Para criar um conta do Database Mail usando:**  [Assistente de Configuração do Database Mail](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [Próximas etapas para configurar o Database Mail](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Determine o nome de servidor e o número de porta para o servidor de Protocolo SMTP que você usa para enviar e-mail. Se o servidor SMTP requer autenticação, determine o nome de usuário e a senha do servidor SMTP.  
  
-   Opcionalmente, você também pode especificar o tipo do servidor e o número da porta para o servidor. O tipo de servidor sempre é 'SMTP' em emails enviados. A maioria dos servidores SMTP usa a porta 25, a padrão.  
  
##  <a name="SSMSProcedure"></a> Usando o assistente para configuração do Database Mail  
 **Para criar uma conta do Database Mail usando um assistente**  
  
-   No Pesquisador de Objetos, conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usada para configurar o Database Mail e expanda a árvore de servidores.  
  
-   Expanda o nó **Gerenciamento** .  
  
-   Clique duas vezes em Database Mail para abrir o Assistente de Configuração do Database Mail.  
  
-   Na página **Selecionar Tarefa de Configuração** , selecione **Gerenciar contas e perfis do Database Mail**e clique em **Avançar**.  
  
-   Na página **Gerenciar Perfis e Contas** , selecione a opção **Criar uma nova conta** e clique em **Avançar**.  
  
-   Na página **Nova Conta** , especifique o nome de conta, descrição, informações de servidor de email e tipo de autenticação. Clique em **Avançar**.  
  
-   Na página **Concluir o Assistente** , examine as ações a serem executadas e clique em **Concluir** para concluir a criação da nova conta.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para criar uma conta do Database Mail usando Transact-SQL**  
  
 Execute o procedimento armazenado **msdb.dbo.sysmail_add_account_sp** para criar a conta e especifique as seguintes informações:  
  
-   O nome da conta a criar.  
  
-   Uma descrição opcional da conta.  
  
-   O endereço de email a ser exibido em mensagens de email enviadas.  
  
-   O nome para exibição a aparecer nas mensagens de email enviadas.  
  
-   O nome do servidor SMTP.  
  
-   O nome de usuário a usar para fazer logon no servidor SMTP, se o servidor SMTP exigir autenticação.  
  
-   A senha a usar para fazer logon no servidor SMTP, se o servidor SMTP exigir autenticação.  
  
 O exemplo a seguir cria uma nova conta do Database Mail.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
##  <a name="FollowUp"></a> Acompanhamento: Próximas etapas para configurar o Database Mail  
  
-   [Criar um perfil do Database Mail](create-a-database-mail-profile.md)  
  
  
