---
title: Quais são as novidades do SQL Server 2017 no Linux | Microsoft Docs
description: Este artigo destaca o que há de novo para o SQL Server 2017 no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.openlocfilehash: 6ec87bdb2a1ca458893b65bc47e18a8f4664acb1
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63456726"
---
# <a name="whats-new-for-sql-server-on-linux"></a>O que há de novo para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve os principais recursos e serviços disponíveis para o SQL Server 2017 em execução no Linux.

Visualização de 2019 do SQL Server foi lançada. Este artigo não cobre versões de visualização do SQL Server de 2019. Para saber mais sobre visualização de 2019 do SQL Server, consulte [quais são as novidades na visualização de 2019 do SQL Server para Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).

> [!NOTE]
> Além desses recursos neste artigo, as atualizações cumulativas são liberadas em intervalos regulares após a versão GA. Essas atualizações cumulativas fornecem várias melhorias e correções. Para obter informações sobre a versão CU mais recente, consulte [ https://aka.ms/sql2017cu ](https://aka.ms/sql2017cu). Para baixar os pacotes e problemas conhecidos, consulte o [notas de versão](sql-server-linux-release-notes.md).

## <a name="sql-server-database-engine"></a>Mecanismo de Banco de Dados do SQL Server

- Habilitados os principais recursos do mecanismo de banco de dados do SQL Server.
- Suporte para caminhos de Linux nativo.
- Suporte a IPv6.
- Suporte para arquivos de banco de dados em NFS.
- Habilitada [Transport Layer Security](sql-server-linux-encrypted-connections.md) criptografia (TLS).
- Habilitada [autenticação do Active Directory](sql-server-linux-active-directory-authentication.md).
- [Funcionalidade de grupos de disponibilidade](sql-server-linux-availability-group-overview.md) para alta disponibilidade.
- [Pesquisa de texto completo](sql-server-linux-setup-full-text-search.md) dão suporte.

## <a name="sql-server-agent"></a>SQL Server Agent

- Habilitada [SQL Server Agent](sql-server-linux-setup-sql-agent.md) dão suporte para as seguintes tarefas:
  - [Trabalhos de Transact-SQL](sql-server-linux-run-sql-server-agent-job.md)
  - [Email de banco de dados](sql-server-linux-db-mail-sql-agent.md)
  - [Envio de logs](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Capacidade de executar pacotes SSIS no Linux. Para obter mais informações, consulte [configurar o SQL Server Integration Services no Linux com o ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="other-improvements"></a>Outras melhorias

- Ferramenta de configuração de linha de comando [mssql-conf](sql-server-linux-configure-mssql-conf.md).
- Suporte de instalação autônoma com [variáveis de ambiente](sql-server-linux-configure-environment-variables.md).
- Plataforma cruzada [extensão do Visual Studio Code mssql-server](sql-server-linux-develop-use-vscode.md).
- Gerador de script de plataforma cruzada [mssql scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md).
- Monitor de modo de exibição de gerenciamento dinâmico (DMV) de plataforma cruzada, [ferramenta DBFS](https://github.com/Microsoft/dbfs).

## <a name="next-steps"></a>Próximas etapas

Para instalar o SQL Server no Linux, use um dos seguintes tutoriais:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

Para ver outros aprimoramentos introduzidos no SQL Server 2017, consulte [o que há de novo no SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

> [!TIP]
> Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
