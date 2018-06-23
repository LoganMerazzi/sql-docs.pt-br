---
title: Carregamento de arquivo e salve as colunas de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0101e809-d6ea-4d0c-95ec-65dd77acf665
caps.latest.revision: 4
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f3e5ddbc14ab934dfdd0c1a16c2ec7f711f67a57
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010543"
---
# <a name="file-load-and-save-data-columns"></a>Colunas de dados File Load and Save
  A categoria de evento File Load and Save tem a seguinte classe de evento:  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|90|File Load Begin|Início do carregamento do arquivo.|  
|91|File Load End|Término do carregamento do arquivo.|  
|92|File Save Begin|Início do salvamento do arquivo.|  
|93|File Save End|File Save End|  
|94|PageOut Begin|Início de PageOut.|  
|95|PageOut End|PageOut End|  
|96|PageIn Begin|Início de PageIn.|  
|97|PageIn End|PageIn End|  
  
 A tabela a seguir lista as colunas de dados dessa classe de evento.  
  
## <a name="file-load-begin"></a>File Load Begin  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="file-load-end"></a>File Load End  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|IntegerData|10|1|Dados Integer.|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Êxito|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="file-save-begin"></a>File Save Begin  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento|  
  
## <a name="file-save-end"></a>File Save End  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|IntegerData|10|1|Dados Integer.|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Êxito|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="pageout-begin"></a>PageOut Begin  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="pageout-end"></a>PageOut End  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|IntegerData|10|1|Dados Integer.|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Êxito|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="pagein-begin"></a>PageIn Begin  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="pagein-end"></a>PageIn End  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|IntegerData|10|1|Dados Integer.|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Êxito|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de evento Carregar e salvar arquivo](file-load-and-save-event-category.md)  
  
  