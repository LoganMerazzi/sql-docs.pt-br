---
title: Segurança do DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 921927f5-1b1e-452a-a79e-c691829fd826
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ae5ff9bf9fe78ca7230865c6f3df5f2b1333f005
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480853"
---
# <a name="dqs-security"></a>Segurança do DQS
  A infraestrutura de segurança [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) se baseia na infraestrutura de segurança do SQL Server. Um administrador de banco de dados concede a um usuário um conjunto de permissões, associando o usuário a uma função DQS. Isso determina os recursos DQS aos quais o usuário tem acesso e as atividades funcionais que o usuário tem permissão para executar.  
  
## <a name="dqs-roles"></a>Funções DQS  
 Há quatro funções DQS. Uma delas é o administrador de banco de dados (DBA) que lida principalmente com instalação de produto, manutenção de banco de dados e gerenciamento de usuário. Esta função usa basicamente o SQL Server Management Studio, e não o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Sua função de servidor é sysadmin.  
  
 As três outras funções são operadores de informações, administradores de dados que usam o produto diretamente, trabalhando no aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Essas funções incluem o seguinte:  
  
-   O **Administrador do DQS** (dqs_administrator role) pode fazer tudo no escopo do produto. O administrador pode editar e executar um projeto, criar e editar uma base de dados de conhecimento, finalizar uma atividade, parar um processo em uma atividade e alterar a configuração e as definições dos Serviços de Dados de Referência. Entretanto, o Administrador do DQS não pode instalar o servidor ou adicionar novos usuários. O administrador de banco de dados deve fazer isso.  
  
-   O **Editor de KB do DQS** (função dqs_kb_editor) pode executar todas as atividades do DQS, exceto a administração. O Editor de KB pode editar e executar um projeto, além de criar e editar uma base de dados de conhecimento. Eles podem consultar os dados de monitoramento de atividades, mas não podem finalizar ou parar uma atividade ou executar tarefas administrativas.  
  
-   O **DQS KB Operador** (função dqs_kb_operator) pode editar e executar um projeto. Eles não podem executar qualquer tipo de gerenciamento de conhecimento; eles não podem criar ou alterar uma base de dados de conhecimento. Eles podem consultar os dados de monitoramento de atividades, mas não podem finalizar uma atividade ou executar tarefas administrativas.  
  
## <a name="user-management"></a>Gerenciamento de usuário  
 O DBA (administrador de banco de dados) cria os usuários DQS e associa-os a funções DQS no SQL Server Management Studio. O DBA gerencia suas permissões, adicionando Logons do SQL como usuários do banco de dados DQS_MAIN e associando cada usuário a uma das funções do DQS. Cada função recebe permissões a um conjunto de procedimentos armazenados no banco de dados DQS_MAIN. As três funções DQS não estão disponíveis para os bancos de dados DQS_PROJECTS e DQS_STAGING_DATA.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como criar um usuário e conceder funções DQS usando o SQL Server Management Studio.|[Gerenciar usuários do DQS no SSMS](../../2014/data-quality-services/manage-dqs-users-in-ssms.md)|  
  
  
