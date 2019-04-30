---
title: 'Tarefa 6: Adicionar origem do Excel ao fluxo de dados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 644b80d6a547c58b058c4c932a261762a0235430
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156680"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>Tarefa 6: Adicionar a origem do Excel ao fluxo de dados
  Nesta tarefa, você adicionará uma Origem do Excel ao fluxo de dados para ler dados do fornecedor do arquivo de origem do Excel. A Origem do Excel extrai dados de planilhas ou intervalos em pastas de trabalho do Microsoft Excel. Consulte o tópico [Origem do Excel](../integration-services/data-flow/excel-source.md) para obter mais detalhes.  
  
1.  Arraste e solte **Origem do Excel** de **Outras Origens** na **Caixa de Ferramentas do SSIS** para a guia **Fluxo de Dados** .  
  
2.  Clique com o botão direito do mouse em **Origem do Excel** na guia **Fluxo de Dados** e clique em **Renomear**.  
  
3.  Digite **Ler Dados do Fornecedor de Arquivo do Excel** e pressione **ENTER**.  
  
4.  Clique duas vezes em **Ler Dados do Fornecedor de Arquivo do Excel** para iniciar a caixa de diálogo de **Editor de Origem do Excel** .  
  
5.  Na caixa de diálogo **Editor de Origem do Excel** , clique em **Novo** para criar uma conexão do Excel.  
  
6.  Na caixa de diálogo **Gerenciador de Conexões do Excel** , clique em **Procurar**e selecione o arquivo **Suppliers.xls** na pasta **Tutorial do EIM** . Confirme se a opção **Microsoft Excel 97-2003** está selecionada na caixa **Versão do Excel** e clique em **OK**.  
  
     ![Caixa de diálogo Gerenciador de Conexão do Excel](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "caixa de diálogo Gerenciador de Conexão do Excel")  
  
7.  Na caixa de diálogo **Editor de Origem do Excel** , selecione **IncomingSuppliers$** na caixa de listagem **Nome da planilha do Excel** .  
  
     ![Nome da planilha do Excel - fornecedores de entrada $](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "nome da planilha do Excel - fornecedores de entrada $")  
  
8.  Clique em **Visualizar** para visualizar os dados no arquivo do Excel.  
  
9. Clique em **OK** para fechar a caixa de diálogo.  
  
10. Arraste e solte a transformação **Limpeza DQS** em **Outras Transformações** na **Caixa de Ferramentas do SSIS** para a guia **Fluxo de Dados** em **Ler Dados do Fornecedor de Arquivo do Excel**. A transformação Limpeza DQS usa o DQS (Data Quality Services) para corrigir dados aplicando regras aprovadas na base de dados de conhecimento. Essa transformação, em tempo de execução, cria um projeto de limpeza DQS no servidor DQS. Consulte o tópico [Transformação Limpeza DQS](https://msdn.microsoft.com/library/ee677619.aspx) para obter mais detalhes.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 7: A transformação de limpeza do DQS adição ao fluxo de dados](../integration-services/data-flow/data-flow.md)  
  
  
