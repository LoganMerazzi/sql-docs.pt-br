---
title: Caixa de diálogo Erros de Sintaxe SQL Encontrados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.sqlsyntaxerrorsencountered
- vdtsql.chm:69641
ms.assetid: bc9e5784-227e-4c5d-8084-24274fa6c14a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2f44636f7ccf2b8aad7794403199acfe68637b15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105671"
---
# <a name="sql-syntax-errors-encountered-dialog-box-visual-database-tools"></a>Caixa de diálogo Erros de Sintaxe SQL Encontrados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Essa caixa de diálogo o notifica que o designer não pode analisar a instrução SQL no painel SQL.  
  
Essa caixa de diálogo aparece quando você digita ou edita uma instrução SQL no painel SQL; então, você pode alterar para outro painel, verificar a consulta ou tentar executar a consulta e uma das seguintes condições é aplicada:  
  
-   A instrução SQL está incompleta ou contém um ou mais erros de sintaxe.  
  
-   A instrução SQL é válida mas não tem suporte nos painéis gráficos (por exemplo, uma consulta de União).  
  
-   A instrução SQL é válida mas contém sintaxe específica para a conexão de dados que você está usando.  
  
> [!TIP]  
> Você pode verificar se uma instrução é válida usando o botão **Verificar Sintaxe SQL** na barra de ferramentas **Consulta** .  
  
A caixa de diálogo exibe uma mensagem com a razão pela qual a instrução SQL não pôde ser analisada. Clique em **OK** para continuar.  
  
## <a name="see-also"></a>Consulte Também  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
