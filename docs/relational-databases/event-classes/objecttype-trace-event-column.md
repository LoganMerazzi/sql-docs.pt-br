---
title: Coluna de evento de rastreamento ObjectType | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Object Type column values
- events [SQL Server], Object Type column values
- event classes [SQL Server], Object Type column values
- Object Type column values [SQL Server]
ms.assetid: 42f85c50-34c9-49ca-955f-af9595e2707f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 76675cf49ba1ac19e18b3bb4b96980aa30c4f6c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115894"
---
# <a name="objecttype-trace-event-column"></a>Coluna de evento de rastreamento ObjectType
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A coluna Object Type é usada em diversos eventos de rastreamento. Este tópico descreve os possíveis valores dessa coluna e as definições a ela associadas.  
  
## <a name="object-type-column-values"></a>Valores da coluna Object Type  
  
|Valor|Definição|  
|-----------|----------------|  
|8259|Restrição CHECK|  
|8260|Padrão (restrição ou autônomo)|  
|8262|Restrição FOREIGN KEY|  
|8272|Procedimento armazenado|  
|8274|Regra|  
|8275|Tabela do sistema|  
|8276|Gatilho em servidor|  
|8277|Tabela (definida pelo usuário)|  
|8278|Exibição|  
|8280|Procedimento armazenado estendido|  
|16724|Gatilho CLR|  
|16964|banco de dados|  
|16975|Object|  
|17222|Catálogo de texto completo|  
|17232|Procedimento armazenado CLR|  
|17235|esquema|  
|17475|Credencial|  
|17491|Evento DDL|  
|17741|Evento de gerenciamento|  
|17747|Evento de segurança|  
|17749|Evento de usuário|  
|17985|Função de agregação CLR|  
|17993|Função SQL com valor de tabela embutida|  
|18000|Função de partição|  
|18002|Procedimento do filtro de replicação|  
|18004|Função SQL com valor de tabela|  
|18259|Função do servidor|  
|18263|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows|  
|19265|Chave assimétrica|  
|19277|Chave mestra|  
|19280|Chave Primária|  
|19283|ObfusKey|  
|19521|Logon de chave assimétrica|  
|19523|Logon de certificado|  
|19538|Role|  
|19539|Logon do SQL|  
|19543|Logon do Windows|  
|20034|Associação de serviço remoto|  
|20036|Notificação de eventos em banco de dados|  
|20037|Notificação de eventos|  
|20038|Função SQL escalar|  
|20047|Notificação de eventos em objeto|  
|20051|Sinônimo|  
|20307|Sequência|  
|20549|Ponto de extremidade|  
|20801|Consultas ad hoc que podem ser armazenadas em cache|  
|20816|Consultas preparadas que podem ser armazenadas em cache|  
|20819|Fila do serviço do Service Broker|  
|20821|Restrição UNIQUE|  
|21057|Função de aplicativo|  
|21059|Certificado|  
|21075|Servidor|  
|21076|Gatilho Transact-SQL|  
|21313|Assembly|  
|21318|Função CLR escalar|  
|21321|Função SQL escalar embutida|  
|21328|Esquema de partição|  
|21333|Usuário|  
|21571|Contrato do serviço do Service Broker|  
|21572|Gatilho em banco de dados|  
|21574|Função CLR com valor de tabela|  
|21577|Tabela interna (por exemplo, Tabela Nó XML, Tabela Fila.)|  
|21581|Tipo de mensagem do Service Broker|  
|21586|Rota do Service Broker|  
|21587|Estatísticas|  
|21825<br /><br /> 21827<br /><br /> 21831<br /><br /> 21843<br /><br /> 21847|Usuário|  
|22099|Serviço do Service Broker|  
|22601|Índice|  
|22604|Logon de certificado|  
|22611|Esquema XML|  
|22868|Tipo|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
