---
title: Sincronizar relógios dos servidores de destino (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 74939b313abc695012813f361189ac38a68eafe7
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263426"
---
# <a name="synchronize-target-server-clocks-sql-server-management-studio"></a>Synchronize Target Server Clocks (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como sincronizar os relógios dos servidores de destino no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] com o relógio do servidor mestre usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. Sincronizar esses relógios do sistema dá suporte às agendas de trabalho.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para sincronizar os relógios dos servidores de destino usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-synchronize-target-server-clocks"></a>Para sincronizar os relógios dos servidores de destino  
  
1.  No **Pesquisador de Objetos,** clique no sinal de adição para expandir o servidor onde você deseja sincronizar os relógios dos servidores de destino com o relógio do servidor mestre.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e selecione **Gerenciar Servidores de Destino**.  
  
3.  Na caixa de diálogo **Gerenciar Servidores de Destino** , clique em **Postar Instruções**.  
  
4.  Na lista **Tipo de instrução** , selecione **Sincronizar relógios**.  
  
5.  Em **Destinatários**, siga um destes procedimentos:  
  
    -   Clique em **Todos os servidores de destino** para sincronizar os relógios de todos os servidores de destino com o relógio do servidor mestre.  
  
    -   Clique em **Estes servidores de destino** para sincronizar os relógios de apenas alguns servidores de destino com o relógio do servidor mestre, selecionando cada um deles.  
  
6.  Quando terminar, clique em **OK**.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-synchronize-target-server-clocks"></a>Para sincronizar os relógios dos servidores de destino  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_resync_targetserver (Transact-SQL)](https://msdn.microsoft.com/40e44df7-d3e3-44ee-b149-08aba629a21f).  
  
