---
title: 'Tarefa 2: Carregando dados do fornecedor no MDS usando o suplemento do MDS para Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1831fc9ea79027e24d752d05e3b50d3a58d6e06f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008085"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Tarefa 2: Carregando dados do fornecedor no MDS usando o Suplemento MDS para Excel
  Nesta tarefa, você publica os dados limpos e do fornecedor para **MDS** usando o **suplemento do MDS para Excel**. Criar uma entidade chamada **Supplier** no **fornecedores** modelo que você criou na lição anterior. A entidade terá um atributo para cada coluna no arquivo do Excel. Os atributos de código e o nome da entidade Supplier correspondem do **SupplierID** e **Supplier Name** colunas no Excel.  
  
1.  Abra **limpos e correspondidos Suppliers.xls** na **Excel**.  
  
2.  Pressione **CTRL + A** para selecionar todos os dados. É **importante** que você selecione todos os dados na planilha.  
  
3.  Clique em **Dados Mestres** na barra de menus.  
  
4.  Clique em **criar entidade** botão na faixa de opções.  
  
     ![Excel - guia de dados mestre - botão Criar entidade](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - guia de dados mestre - botão Criar entidade")  
  
5.  Na caixa de diálogo **Gerenciar Conexões** , se você não visualizar a conexão com o **servidor MDS local** em **Conexões existentes**, siga este procedimento:  
  
    1.  Selecione **Criar uma nova conexão**e clique no botão **Nova** .  
  
    2.  No **adicionar nova Conexão** caixa de diálogo, digite **servidor MDS Local** para **descrição** e **http://localhost/MDS** para  **Endereço do servidor MDS**e clique em **Okey** para fechar a caixa de diálogo.  
  
6.  Em **gerenciar conexões** caixa de diálogo, selecione **servidor MDS Local** (http://localhost/MDS), clique em **teste** para testar a conexão. Clique em **OK** na caixa de mensagem.  
  
7.  Clique em **conectar** para se conectar ao servidor MDS.  
  
8.  No **criar entidade** caixa de diálogo, selecione **fornecedores** para o **modelo**.  
  
9. Certifique-se de que **VERSION_1** é selecionado para **versão**.  
  
10. Digite **Supplier** para **novo nome da entidade**.  
  
11. Selecione **SupplierID** para **a coluna que contém um identificador exclusivo** campo (você também pode gerar um código automaticamente). Basicamente, você está mapeando o **SupplierID** coluna **Excel** para o **código** atributo de **Supplier** entidade.  
  
12. Selecione **Supplier Name** para **a coluna que contém os nomes** campo. Basicamente, você está mapeando o **Supplier Name** coluna **Excel** para o **nome** atributo do **Supplier** entidade. O **código** e **nome** atributos são obrigatórios para uma entidade no MDS.  
  
     ![Criar caixa de diálogo entidade](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "criar caixa de diálogo de entidade")  
  
13. Clique em **Okey** para criar a entidade no MDS, publique os dados mestres para a entidade e fechar **criar entidade** caixa de diálogo.  
  
14. Agora, você deve ver uma nova planilha denominada **Supplier**, que é o nome da entidade, adicionada à sua planilha do Excel e na parte superior da planilha, você deve ver que a planilha está conectada ao servidor MDS. Observe que a planilha original (denominada **Planilha1**) ainda existe.  
  
     ![Excel - guias fornecedor e Planilha1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - guias fornecedor e Planilha1")  
  
     ![Excel - mostrando detalhes de Conexão do MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - mostrando detalhes de Conexão do MDS")  
  
15. Manter **Excel** abrir.  
  
## <a name="next-task"></a>Próxima tarefa  
 [Tarefa 3: Verificando os dados no Master Data Manager](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  