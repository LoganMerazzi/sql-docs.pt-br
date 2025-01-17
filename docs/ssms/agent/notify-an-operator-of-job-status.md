---
title: Notificar um operador sobre o status do trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f93cd022a9c5f02091f4880ac53772d4e1532f9a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260613"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como definir opções de notificação no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], ou o SQL Server Management Objects, de forma que o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent possa enviar notificações a operadores sobre trabalhos.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para notificar um operador sobre o status do trabalho usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar um operador sobre o status do trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja editar e selecione **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , selecione a página **Notificações** .  
  
4.  Se desejar notificar um operador via email, marque **Email**, escolha um operador na lista e selecione uma destas opções:  
  
    -   **Quando o trabalho for bem-sucedido** , para notificar o operador quando o trabalho for concluído com êxito.  
  
    -   **Quando ocorrer falha no trabalho** para notificar o operador quando o trabalho não for concluído com êxito.  
  
    -   **Quando o trabalho for concluído** , para notificar o operador independentemente do status de conclusão.  
  
5.  Se desejar notificar um operador via pager, marque **Pager**, escolha um operador na lista e selecione uma destas opções:  
  
    -   **Quando o trabalho for bem-sucedido** , para notificar o operador quando o trabalho for concluído com êxito.  
  
    -   **Quando ocorrer falha no trabalho** para notificar o operador quando o trabalho não for concluído com êxito.  
  
    -   **Quando o trabalho for concluído** , para notificar o operador independentemente do status de conclusão.  
  
6.  Se desejar notificar um operador via net send, marque **Net send**, escolha um operador na lista e selecione uma destas opções:  
  
    -   **Quando o trabalho for bem-sucedido** , para notificar o operador quando o trabalho for concluído com êxito.  
  
    -   **Quando ocorrer falha no trabalho** para notificar o operador quando o trabalho não for concluído com êxito.  
  
    -   **Quando o trabalho for concluído** , para notificar o operador independentemente do status de conclusão.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar um operador sobre o status do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists
    --  and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'François Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para notificar um operador sobre o status do trabalho**  
  
Use a classe **Job** usando uma linguagem de programação que você possa escolher, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
