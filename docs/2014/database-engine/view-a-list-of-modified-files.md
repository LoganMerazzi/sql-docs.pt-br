---
title: Exibir uma lista de arquivos modificados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckinWindow
helpviewer_keywords:
- listing modified files
- modified files list [SQL Server]
- checking in files
ms.assetid: 1b053719-8500-4300-a169-fffca5801dd0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c35062e6dfa339d0cd37f3905dc801f0f47becba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773422"
---
# <a name="view-a-list-of-modified-files"></a>Exibir uma lista de arquivos modificados
  Você pode usar o **check-ins pendentes** janela para exibir constantemente uma lista dos arquivos com check-out na solução atual e, em seguida, fazer check-in desses arquivos com um único botão clique em.  
  
### <a name="to-view-a-list-of-modified-files"></a>Para exibir uma lista de arquivos modificados  
  
1.  Sobre o **modo de exibição** menu, clique em **check-ins pendentes**.  
  
2.  Para verificar nos arquivos selecionados, clique em **Fazer Check-In**. Como alternativa, você pode encaixar a **check-ins pendentes** janela no lado direito do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] ambiente para que você pode verificar os arquivos quando tiver terminado de trabalhar.  
  
     **Fazer Check-in**  
     Faz o check-in na solução.  
  
     **Comentários**  
     Associa um comentário de texto sem-formatação ao check-in pendente. É criado um comentário e associado a cada versão de um projeto e armazenado no banco de dados de controle de código-fonte.  
  
     **Opções**  
     Especifica as ações de controle do código-fonte deve tomar quando você clica o **Fazer Check-In** botão.  
  
    -   **Mantenha todos Check-Out**  
  
         Especifica que suas alterações devem ser gravadas no provedor do controle do código-fonte mas que os arquivos devem permanecer check-out.  
  
     **Sort**  
     Especifica a ordem de classificação para as colunas exibidas na lista Itens.  
  
     **Colunas**  
     Exibe uma lista das colunas que você pode adicionar à lista Itens da janela.  
  
     **Exibição de árvore**  
     Exibe a hierarquia da pasta e do arquivo para a solução ou projeto que você está fazendo o check-in.  
  
     **Modo de exibição simples**  
     Exibe os arquivos dos quais está fazendo check-in como listas simples na conexão de controle do código-fonte.  
  
     **Comparar versões**  
     Abre o Visual SourceSafe **opções de diferença** caixa de diálogo, que compara um arquivo selecionado em seu projeto de ambiente de desenvolvimento para qualquer outro arquivo selecionado e mostra as diferenças, se houver.  
  
     **Desfazer check-out**  
     Reverte o check-out de todos os itens selecionados na **check-ins pendentes** janela.  
  
     **Nome**  
     Exibe uma lista dos itens disponíveis para fazer check-in. Os itens mostram as caixas de seleção ao seu lado selecionadas. Se você não quiser fazer o check-in em um item específico, desmarque a caixa de seleção próxima a ele.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar check-ins](../../2014/database-engine/manage-checkins.md)   
 [Gerenciar check-outs](../../2014/database-engine/manage-checkouts.md)  
  
  
