---
title: Adicionar itens existentes a um projeto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 084b3879-e96b-45a7-b421-6a4b0db2b92b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 58d94afea9c6801d75a67f6f9136441d536eb696
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62956141"
---
# <a name="add-existing-items-to-a-project"></a>Adicionar itens existentes a um projeto
  Adicione novos itens a um projeto para estender a funcionalidade do aplicativo. Um item existente pode ser uma consulta ou um arquivo diverso. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tem dois tipos de projeto: Projeto de Script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Projeto de Script do Analysis Services. O tipo de projeto determina os arquivos de consulta que você pode adicionar ao projeto. Por exemplo, você pode adicionar uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] (um arquivo com uma extensão .sql) a um projeto de script do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas não pode adicioná-lo a um Projeto de Script do Analysis Services. Para associar extensões de arquivo adicionais a um tipo de projeto, consulte [associar extensões de arquivo para um Editor de código](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md).  
  
### <a name="to-add-an-existing-query-or-a-miscellaneous-file-to-a-project"></a>Para adicionar uma consulta existente ou um arquivo diverso a um projeto  
  
1.  No Gerenciador de Soluções, selecione um projeto de destino.  
  
2.  No menu **Projeto** , clique em **Adicionar Item Existente**.  
  
     **Look in**  
     Localize os arquivos ou pastas a adicionar ao seu projeto nesta lista. Em XML Web Services e aplicativos Web ASP.NET, os arquivos se localizam no servidor Web.  
  
     **Área de Trabalho**  
     Exibe os arquivos e pastas localizadas na área de trabalho.  
  
     **Meus Projetos**  
     Exibe os arquivos e pastas no local padrão **Meus Projetos** .  
  
     **Meu Computador**  
     Exibe o conteúdo de sua pasta **Meu Computador** .  
  
     **Nome do arquivo**  
     Use esta opção para filtrar os arquivos e pastas a serem exibidos. Insira o nome completo ou parcial do arquivo a filtrar; use um asterisco (`*`) como curinga.  
  
    > [!NOTE]  
    >  Navegue na Web e em locais de rede inserindo a URL ou o caminho de rede na caixa **Nome do arquivo** . Por exemplo, **http://mywebsite** exibe os arquivos disponíveis no local da Web meusite e **\\ \meuservidor\meucompartilhamento** exibe os arquivos disponíveis no local meucompartilhamento em meuservidor.  
  
     **Arquivos do tipo**  
     Use esta opção para filtrar arquivos com base na extensão de arquivo. Cada produto lista filtros padrões dos tipos de arquivo mais comuns.  
  
     **Adicionar**  
     Use este botão suspenso para adicionar o item ao projeto e abrir o item em seu editor padrão.  
  
    -   **Adicionar**  
  
         Copia o item existente na sua pasta de projeto no disco e adiciona o item sob o projeto selecionado no Gerenciador de Soluções. Nenhuma alteração feita ao item é refletida no item no local original. Esse é o editor padrão do tipo de arquivo.  
  
    -   **Adicionar Como Vínculo**  
  
         Adiciona o arquivo selecionado ao projeto e abre-o com o editor padrão do tipo de arquivo. Essa opção abre o arquivo originalmente selecionado e não copia o arquivo na pasta de projeto.  
  
3.  Na adição de arquivos de consulta, a caixa de diálogo de conexão solicitará que você especifique uma conexão para a consulta. Você poderá clicar em **Cancelar** na caixa de diálogo de conexão se não quiser associar uma conexão à consulta.  
  
4.  O arquivo será adicionado à pasta **Consultas** ou **Arquivos Diversos** do projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de soluções](solution-explorer.md)   
 [Adicionar novos itens a um projeto](add-new-items-to-a-project.md)   
 [Remover ou excluir um item ou projeto](remove-or-delete-an-item-or-project.md)  
  
  
