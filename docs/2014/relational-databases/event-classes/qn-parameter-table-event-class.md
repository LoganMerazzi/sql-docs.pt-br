---
title: Classe de evento QN:Parameter Table | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], QN:Parameter Table
ms.assetid: 292da1ed-4c7e-4bd2-9b84-b9ee09917724
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 395df605926f0ff4ddc30970cdcebce0f1d0c8fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63044441"
---
# <a name="qnparameter-table-event-class"></a>Classe de evento QN:Parameter Table
  O evento QN:Parameter table fornece informações sobre as operações necessárias para criar, manter contagens de referência e descartar as tabelas internas que armazenam informações sobre parâmetros. Esse evento também informa a atividade interna para reajustar a contagem de uso para uma tabela de parâmetros.  
  
## <a name="qnparameter-table-event-class-data-columns"></a>Colunas de dados da classe de evento QN:Parameter Table  
  
|Coluna de dados|Tipo|Descrição|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|`int`|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|DatabaseID|`int`|A ID do banco de dados especificada pela instrução de *banco de dados* USE ou a ID do banco de dados padrão se nenhuma instrução de *banco de dados*USE tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados Server Name for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|O nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|EventClass|`Int`|Tipo de evento = 200.|27|Não|  
|EventSequence|`int`|Número de sequência para esse evento.|51|Não|  
|EventSubClass|`nvarchar`|O tipo de subclasse de evento, fornecendo mais informações sobre cada classe de evento. Essa coluna pode conter os seguintes valores:<br /><br /> Tabela criada: Indica que uma tabela de parâmetros foi criada no banco de dados.<br /><br /> Tentativa de descarte de tabela: Indica que o banco de dados tentou descartar automaticamente uma tabela de parâmetros não usada para liberar recursos.<br /><br /> Falha na tentativa de descarte de tabela: Indica que o banco de dados tentou descartar uma tabela de parâmetros não usada e falhou. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] irá reagendar automaticamente a exclusão da tabela de parâmetros para liberar recursos.<br /><br /> Tabela descartada: Indica que o banco de dados descartou com sucesso uma tabela de parâmetros.<br /><br /> Tabela fixada: Indica que a tabela de parâmetros está marcada para uso atual pelo processamento interno.<br /><br /> Tabela desafixada: Indica que a tabela de parâmetros foi desafixada. Processamento interno terminou de usar a tabela.<br /><br /> Número de usuários aumentado: Indica que o número de assinaturas de notificação de consulta que fazem referência a uma tabela de parâmetros aumentou.<br /><br /> Número de usuários diminuiu: Indica que o número de assinaturas de notificação de consulta que fazem referência a uma tabela de parâmetros diminuiu.<br /><br /> Contador LRU: Indica que a contagem de uso para a tabela de parâmetros foi reinicializada.<br /><br /> Tarefa de limpeza iniciada: Indica quando a limpeza para todas as assinaturas nesta tabela de parâmetros foi iniciada. Isto ocorre quando o banco de dados é iniciado ou quando uma tabela subjacente às assinaturas desta tabela de parâmetros é descartada.<br /><br /> Tarefa de limpeza concluída: Indica quando a limpeza para todas as assinaturas nesta tabela de parâmetros foi concluída.|21|Sim|  
|GroupID|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|`nvarchar`|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário.<br /><br /> 0 = usuário<br /><br /> 1 = sistema|60|Não|  
|LoginName|`nvarchar`|O nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do Windows no formato *DOMAIN*\\*Username*).|11|Não|  
|LoginSID|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|RequestID|`int`|Identificador da solicitação que contém a instrução.|49|Sim|  
|ServerName|`nvarchar`|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, se um aplicativo se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando Logon1 e executar uma instrução como Logon2, o SessionLoginName mostrará "Logon1" e LoginName mostrará "Logon2". Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TextData|`ntext`|Retorna um documento XML que contém informações específicas para esse evento. Esse documento está de acordo com o esquema XML disponível na página [SQL Server Query Notification Profiler Event Schema](https://go.microsoft.com/fwlink/?LinkId=63331) .|1|Sim|  
  
  
