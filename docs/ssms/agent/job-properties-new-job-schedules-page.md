---
title: Propriedades do trabalho – Novo trabalho (página Agendas) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.schedules.f1
ms.assetid: 0b03585b-a510-484d-8a63-9b32459def9c
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8b7cb76d41c20f44c0e05980d435cd5a3d50ae05
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67686881"
---
# <a name="job-properties---new-job-schedules-page"></a>Propriedades do trabalho – Novo trabalho (página Agendas)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa página para exibir e organizar as agendas para um trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Lista de agendas**  
Lista as agendas para esse trabalho.  
  
**Nova**  
Crie uma agenda nova. Depois de criada, a agenda é adicionada ao trabalho.  
  
**Escolher**  
Selecione uma agenda dentre as agendas existentes. Como um trabalho e uma agenda precisam ter o mesmo proprietário, essa opção não lhe permitirá escolher dentre as agendas que você tem.  
  
**Editarar**  
Edite a agenda selecionada para alterar propriedades da agenda de trabalho.  
  
**Removerr**  
Remova a agenda selecionada do trabalho. Se nenhum outro trabalho usar a agenda, a agenda será excluída do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
  
