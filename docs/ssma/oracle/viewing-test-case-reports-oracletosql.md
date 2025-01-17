---
title: Exibir relatórios de caso de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 75ce91d7948b53522f6ac861a078f8f902b23ab7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086796"
---
# <a name="viewing-test-case-reports-oracletosql"></a>Exibir relatórios de caso de teste (OracleToSQL)
O relatório de caso de teste mostra os resultados da verificação de teste e as informações de teste geral. Em caso de falha de teste, informações sobre todos os dados incompatíveis em objetos verificados também são exibidas.  
  
## <a name="report-structure"></a>Estrutura de relatório  
A parte superior do relatório mostra essas estatísticas:  
  
-   O número total de objetos testados e o número de objetos para o qual o teste foi bem-sucedido.  
  
-   O número total de tabelas verificadas e chaves estrangeiras e o número de tabelas e chaves estrangeiras combinadas com sucesso.  
  
-   A hora de início, hora de término do caso de teste e o tempo total decorrido para execução.  
  
O restante do relatório mostra informações em quatro categorias:  
  
**Erros de pré-requisitos**  
Mostra os erros que ocorreram no **etapa de pré-requisitos.** Normalmente, ele será ignorado.  
  
**Inicialização**  
Mostra o status de execução como **sucesso** ou **falha**.  
  
**Objetos de resultado do teste**  
Uma comparação dos resultados (êxito ou falha) e a incompatibilidade com o SSMA testador detectado em caso de falha.  
  
**Finalização**  
Mostra o status de execução como **sucesso** ou **falha**.  
  
## <a name="see-also"></a>Consulte também  
[Executar casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testar objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
