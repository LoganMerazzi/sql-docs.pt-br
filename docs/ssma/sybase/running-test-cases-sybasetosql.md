---
title: Executar casos de teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 73047e0741d4dee12ecec3e83df308e3f7abd343
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021024"
---
# <a name="running-test-cases-sybasetosql"></a>Executar casos de teste (SybaseToSQL)
Quando o SSMA testador executa um caso de teste, ele executa os objetos selecionados para teste e cria um relatório sobre os resultados da verificação. Se os resultados são idênticos em ambas as plataformas, o teste foi bem-sucedido. A correspondência de objetos entre Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é determinado de acordo com as configurações de mapeamento de esquema para o projeto atual do SSMA.  
  
Um requisito necessário para um teste bem-sucedido é que todos os objetos do Sybase são convertidos e carregados no banco de dados de destino. Além disso, os dados da tabela devem ser migrados para que o conteúdo das tabelas nas duas plataformas sejam sincronizado.  
  
## <a name="run-test-case"></a>Executar casos de teste  
Para executar o caso de teste preparado:  
  
1.  Clique o **executar** botão.  
  
2.  No **conectar-se ao Sybase** caixa de diálogo, insira as informações de conexão e, em seguida, clique em **Connect**.  
  
Quando o teste for concluído, o relatório de caso de teste é criado. Clique o **relatório** botão para exibir o [exibindo relatórios de caso de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md). O resultado do teste (relatório de casos de teste) é armazenado automaticamente na [repositórios de teste usando o &#40;SybaseToSQL&#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md) para uso posterior.  
  
## <a name="test-case-execution-steps"></a>Etapas de execução do caso de teste  
  
### <a name="prerequisites"></a>Pré-requisitos  
O SSMA testador verifica se todos os pré-requisitos foram atendidos para a execução de teste antes do início do teste. Se algumas condições não forem atendidas, uma mensagem de erro é exibida.  
  
### <a name="initialization"></a>Inicialização  
Nesta etapa, o Testador de SSMA cria auxiliares objetos (tabelas, gatilhos e exibições) no Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles permitem que o controle de alterações feitas nas tabelas afetadas escolhidas para a verificação se o modo de comparações de tabela for **altera somente**.  
  
Suponha que a tabela verificada é denominada USER_TABLE. Para essa tabela, os seguintes objetos auxiliares são criados no Sybase.  
  
Os seguintes objetos são criados no Sybase no banco de dados SSMATESTER2005db ou SSMATESTER2008db e em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados ssmatesterdb_syb.  
  
|Name|Tipo|Descrição|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|Disparador|Gatilho de auditoria de alterações na tabela verificada.|  
|USER_TABLE$ Aud|Tabela|Tabela onde as linhas excluídas e substituídas são salvos.|  
|USER_TABLE$AudID|Tabela|Tabela onde as linhas novas e alteradas são salvos.|  
|USER_TABLE|Exibir|Representação simplificada de modificações de tabela.|  
|USER_TABLE$ novo|Exibir|Representação simplificada de linhas inseridas e substituídas.|  
|USER_TABLE$new_id|Exibir|Identificação de linhas inseridas e alteradas.|  
|USER_TABLE$ antigo|Exibir|Representação simplificada de linhas excluídas e substituídas.|  
  
O seguinte objeto é criado no banco de dados da tabela verificado no Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Name|Tipo|Descrição|  
|--------|--------|---------------|  
|USER_TABLE$ Trg|Disparador|Gatilho de auditoria de alterações na tabela verificada.|  
  
### <a name="test-object-calls"></a>Chamadas de objeto de teste  
Nesta etapa, o SSMA testador invoca cada objeto selecionado para o teste, compara os resultados e mostra o relatório.  
  
### <a name="finalization"></a>Finalização  
Durante a finalização SSMA testador limpa os objetos auxiliares criados na **inicialização** etapa.  
  
## <a name="next-step"></a>Próxima etapa  
[Exibir relatórios de caso de teste &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Selecionando e Configurando objetos a testar &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[Selecionar e configurar os objetos afetados pelo &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[Testar objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
