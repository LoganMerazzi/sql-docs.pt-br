---
title: Propriedades personalizadas da tarefa Controle de CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2a073699-79a2-4ea1-a68e-fc17a80b74ba
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 52abc0392a20325288be4803f83b5350af63429e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947148"
---
# <a name="cdc-control-task-custom-properties"></a>Propriedades personalizadas da tarefa Controle de CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tabela a seguir descreve as propriedades personalizadas da tarefa Controle de CDC. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|Conexão|Conexão ADO.NET|Uma conexão ADO.NET com o banco de dados de CDC do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para acesso às tabelas de alterações e ao Estado de CDC se estiver armazenado no mesmo banco de dados.<br /><br /> A conexão deve ser a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está habilitado para CDC e onde a tabela de alteração selecionada está localizada.|  
|TaskOperation|Inteiro (enumeração)|A operação selecionada para a tarefa de controle de CDC. Os valores possíveis são: **Marcar Início da Carga Inicial**, **Marcar Fim da Carga Inicial**, **Marcar Início de CDC**, **Obter Intervalo de Processamento**, **Marcar Intervalo Processado**e **Redefinir Estado de CDC**.<br /><br /> Se você selecionar **MarkCdcStart**, **MarkInitialLoadStart**ou **MarkInitialLoadEnd** ao trabalhar na CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ou seja, não Oracle), o usuário especificado no gerenciador de conexão deverá ser  **db_owner** ou **sysadmin**.<br /><br /> Para obter mais informações sobre essas operações, consulte [Editor da Tarefa Controle de CDC](../../integration-services/control-flow/cdc-control-task-editor.md) e [Tarefa Controle de CDC](../../integration-services/control-flow/cdc-control-task.md).|  
|OperationParameter|Cadeia de caracteres|Atualmente usado com a operação **MarkCdcStart** . Esse parâmetro permite a entrada adicional necessária para a operação específica. Por exemplo, o número LSN necessário para a operação **MarkCdcStart**|  
|StateVariable|Cadeia de caracteres|Uma variável de pacote SSIS que armazena o estado CDC para o contexto CDC atual. A tarefa Controle de CDC lê e grava o estado em **StateVariable** e não o carrega, nem o armazena em um repositório persistente, a menos que **AutomaticStatePersistence** seja selecionado. Consulte [Definir uma variável de estado](../../integration-services/data-flow/define-a-state-variable.md).|  
|AutomaticStatePersistence|Booliano|A tarefa Controle CDC lê o Estado CDC da variável de pacote Estado CDC. Após uma operação, a tarefa Controle CDC atualiza o valor da variável de pacote Estado CDC. A propriedade **AutomaticStatePersistence** informa a tarefa Controle de CDC quem é responsável por manter o valor do Estado de CDC entre as execuções do pacote SSIS.<br /><br /> Quando essa propriedade for **true**, a tarefa Controle de CDC carregará automaticamente o valor da variável Estado de CDC de uma tabela de estados. Quando a tarefa Controle de CDC atualizar o valor da variável Estado de CDC, ela também atualizará seu valor no mesmo estado **table.stores**, o estado em uma tabela especial e atualizará a Variável de Estado. O desenvolvedor pode controlar qual banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém essa tabela de estado e seu nome. A estrutura dessa tabela de estado é predefinida.<br /><br /> Quando for **false**, a tarefa Controle de CDC não lidará com a persistência de seu valor. Quando true, a tarefa Controle de CDC armazena o estado em uma tabela especial e atualiza a variável StateVariable.<br /><br /> O valor padrão é **true**, indicando que essa persistência de estado é atualizada automaticamente.|  
|StateConnection|Conexão ADO.NET|Uma conexão ADO.NET com o banco de dados em que a tabela de estado reside ao usar **AutomaticStatePersistence**. O valor padrão é o mesmo de **Conexão**.|  
|StateName|Cadeia de caracteres|O nome associado ao estado persistente. A carga cheia e os pacotes CDC que funcionam com o mesmo contexto de CDC especificará um nome de contexto CDC comum. Esse nome é usado para verificar a linha de estado na tabela de estado.<br /><br /> Essa propriedade será aplicável somente quando **AutomaticStatePersistence** estiver definida como **true**.|  
|StateTable|Cadeia de caracteres|Especifica o nome da tabela onde o estado de contexto CDC é armazenado. Essa tabela deve ser acessível com o uso da conexão configurada para esse componente. Essa tabela deve incluir colunas de varchar chamadas **name** e **state**. (A coluna **state** deve ter, no mínimo, 256 caracteres).<br /><br /> Essa propriedade será aplicável somente quando **AutomaticStatePersistence** estiver definida como **true**.|  
|CommandTimeOut|inteiro|Esse valor indica o tempo limite (em segundos) a ser usado ao se comunicar com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esse valor é usado quando o tempo de resposta do banco de dados é muito lento e o valor padrão (30 segundos) não é o suficiente.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefa Controle de CDC](../../integration-services/control-flow/cdc-control-task.md)   
 [Editor da Tarefa Controle de CDC](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
  
