---
title: 'Tarefa 9: Adicionando Union All transformar para combinar registros corretos e corrigidos | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 93b160b6e513ad866126df8b401b82ee1270be84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489645"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>Tarefa 9: Adicionar a Transformação Unir Tudo para combinar registros corretos e corrigidos
  Nesta tarefa, você adiciona a Transformação Unir Tudo ao fluxo de dados. A transformação Union All combina várias entradas em apenas uma saída. No cenário, isso combina registros Corretos e Corrigidos em um fluxo.  
  
1.  Arrastar e soltar **Union All** transformar de **comuns** seção o **caixa de ferramentas do SSIS** para o **de fluxo de dados** guia e coloque-o sob **Escolher registros corretos e corrigidos**.  
  
2.  Clique com botão direito **Union All** transformar na **fluxo de dados** guia e, em seguida, clique em **Renomear**. Tipo de **combinar registros corretos e corrigidos**e pressione **ENTER**.  
  
     ![Combinar corretos e corrigidos Reocrds](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "combinar Reocrds corretos e corrigidos")  
  
3.  Conectar-se **escolher registros corretos e corrigidos** à **combinar registros corretos e corrigidos** no **de fluxo de dados** guia usando o conector azul. Você deve ver a **seleção de saída e entrada** caixa de diálogo.  
  
4.  No **entrada saída** caixa de diálogo, selecione **correto** para **saída** e clique em **Okey**.  
  
     ![Caixa de diálogo de seleção de saída de entrada](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "caixa de diálogo de seleção de saída de entrada")  
  
5.  Mova o conector chamado **corrija** para a esquerda arrastando e soltando o ponto no final do conector para a esquerda.  
  
     ![Conectar corrigir a combinar correto e corrigido](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "conectar corrigir a combinar correto e corrigido")  
  
6.  Se você selecionar **escolher registros corretos e corrigidos** transformar, você deverá visualizar outro conector azul. Arraste o conector azul para **combinar registros corretos e corrigidos**.  
  
     ![Conectar corrigido a combinar correto e corrigido](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "conectar corrigido a combinar correto e corrigido")  
  
7.  Isso **conector** deve ser chamado **corrigido**. Uma vez que você tem apenas duas condições **corrija** e **corrigido**, e uma condição já foi usada, o **seleção de saída e entrada** caixa de diálogo não é exibida no momento. Se os conectores se sobrepuserem, mova um deles para esquerda e o outro para direita arrastando o conector para a esquerda ou direita.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 10: Adicionando a transformação grupo difuso para identificar duplicatas](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
