---
title: Remover o SSMA para componentes do MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ad23c4add9b6e7ea9999a434261a95282f129935
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63182070"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>Remover os componentes do SSMA para MySQL (MySQLToSql)
Quando você terminar de migrar bancos de dados do MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], talvez você queira desinstalar os componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, se você desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , em seguida, SSMA não oferecerá suporte a migração de dados do MySQL para o destino banco de dados (SQL Server/SQL Azure) usando o mecanismo de migração de dados do lado do servidor.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>Desinstalando o SSMA para cliente do MySQL  
Você pode desinstalar o SSMA usando **adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant for MySQL**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando o pacote de extensão  
Você pode remover o pacote de extensão usando **adicionar ou remover programas**.  
  
**Para desinstalar o pacote de extensão**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant para o pacote de extensão do MySQL**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o pacote de extensão, clique em **Sim**.  
  
4.  Nas instâncias com página de Scripts de banco de dados de utilitários, selecione uma instância e, em seguida, clique em **próxima**.  
  
5.  Na página de parâmetros de Conexão, selecione o método de autenticação e, em seguida, clique em **próxima**.  
  
    Autenticação do Windows usarão suas credenciais do Windows para tentar fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon e senha.  
  
6.  Na página de operação concluída, clique em **Okey**.  
  
7.  Na página concluir, clique em **Exit**.  
  
Depois que o processo de desinstalação for concluído, você pode confirmar que os objetos na **sysdb.ssma_MySQL** esquema e, possivelmente, todo **sysdb** banco de dados, foi removido usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No entanto, se você usar outros produtos do SSMA, eles também usam o **sysdb** banco de dados. Se o banco de dados existe e tem certeza de que nenhum outro banco de dados de referência para os objetos neste banco de dados, é possível desanexar o banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para cliente do MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Instalar os componentes do SSMA no SQL Server](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
