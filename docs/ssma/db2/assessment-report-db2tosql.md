---
title: Relatório de avaliação (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e13eba0-e3cf-4205-974f-c00f982061de
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 017bb1a123c7465efd7ad895bb34fec8b87a707e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938301"
---
# <a name="assessment-report-db2tosql"></a>Relatório de avaliação (DB2ToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco de dados para [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, e também pode ajudar a estimar a complexidade e custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecionar objetos a ser convertido no Gerenciador de metadados de código-fonte, clique com botão direito **esquemas** ou **sinônimos**e, em seguida, selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
  
|||  
|-|-|  
|Termo|Definição|  
|**Estatísticas de conversão**|Mostra as estatísticas de conversão pelo tipo de instrução. Esse painel fica visível quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.|  
|**Objetos por categorias**|Mostra o número de objetos por categoria. Esse painel fica visível apenas quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.|  
|**Estatísticas**|Mostra as estatísticas de conversão para o objeto selecionado. Esse painel é visível somente quando um objeto individual com o código é selecionado no painel esquerdo. Talvez você precise expandir **estatísticas**, que está imediatamente acima a **origem** painel para exibir esse painel.|  
|**Source**|Mostra o código do DB2 para o objeto selecionado e destaca o código que não foi convertido em [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esse painel é visível somente quando um objeto individual com o código é selecionado no painel esquerdo.<br /><br />Clique para definir ou limpar indicadores, os números de linha. Use os botões na parte superior do painel para navegar por meio do código.|  
|**Target (destino)**|Mostra a conversão do resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] código para o objeto selecionado e mensagens de erro para o código que não foi convertido. Esse painel é visível somente quando um objeto individual com o código é selecionado no painel esquerdo.<br /><br />Clique para definir ou limpar indicadores, os números de linha. Use os botões na parte superior do painel para navegar por meio do código.|  
|**Painel mensagens**|Mostra os erros, avisos e mensagens informativas que foram geradas durante a criação do relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erros**, **avisos**, ou **informações**, expanda a categoria de mensagens e, em seguida, clique em uma mensagem.|  
  
