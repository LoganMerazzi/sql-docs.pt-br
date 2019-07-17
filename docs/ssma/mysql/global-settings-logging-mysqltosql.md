---
title: Configurações globais (registro em log) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0d033492-5ec3-473a-8de1-821894ec9518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3d5188d701cd7930ff93c37aab74e11bba949d9b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896388"
---
# <a name="global-settings-logging--mysqltosql"></a>Configurações globais (registro em log) (MySQLToSQL)
Use o **configurações globais** caixa de diálogo para especificar as configurações de registro em log para o SSMA. Normalmente, você alteraria essas configurações somente ao trabalhar com o suporte ao produto.  
  
Para acessar essa caixa de diálogo, nos **ferramentas** menu, selecione **configurações globais** e, em seguida, clique no **log** botão na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Nível de mensagens**  
As seguintes opções estão disponíveis sob **nível de mensagens**:  
  
|Opção|Descrição|  
|----------|---------------|  
|**[todas as categorias]**|Usado para definir o nível de log para todas as opções a seguir.|  
|**Coletor**|Coleta metadados sobre o esquema de origem e salva-o ao projeto.|  
|**Conversor**|Converte a estruturas de objetos de banco de dados de origem, como tabelas e procedimentos armazenados, em correspondente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estruturas.|  
|**Migrator de dados**|Migra dados do banco de dados de origem em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Formatador**|Subcomponente do conversor que gera scripts para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema.|  
|**Interface gráfica do usuário**|Mensagens que aparecem quando você usa a ferramenta SSMA.|  
|**Vinculador**|Resolve identificadores SQL e fornece informações para outros componentes.|  
|**Outros**|Todas as mensagens que não estão em nenhuma outra categoria.|  
|**Analisador**|Analisa o esquema de origem.|  
|**Sincronizador**|Objetos de banco de dados da fonte de cargas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**TreeConverter**|Converte objetos nos metadados do código-fonte em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados.|  
  
Para cada opção sob **nível de mensagens**, configure um dos seguintes níveis de log para o SSMA:  
  
|||  
|-|-|  
|**Erro fatal**|Grave apenas as mensagens de erro fatal no log.|  
|**Erro**|Grave no log de erro e mensagens de erro fatal.|  
|**Aviso**|Gravar mensagens de erro fatal, erro e aviso no log.|  
|**Info**|Gravar no log informativo, aviso ou erro e mensagens de erro fatal.|  
|**Depurador**|Gravar todas as mensagens, incluindo mensagens no log de depuração.|  
  
**Caminho do arquivo de log**  
O caminho do arquivo e o nome dos arquivos de log SSMA. Para especificar um nome diferente, clique no caminho atual e, em seguida, clique no botão Procurar ( **...** ) botão.  
  
**Tamanho do arquivo de log**  
O tamanho máximo do arquivo de log em KB. O tamanho mínimo é de 10 KB. O tamanho padrão é 10240 KB.  
  
**Número total de arquivos de log**  
Quando um log ficar cheio, o SSMA renomear o arquivo de log e iniciar um novo. Ao usar essa configuração, especifique o número máximo de arquivos de log para manter. O mínimo é 2.  
  
