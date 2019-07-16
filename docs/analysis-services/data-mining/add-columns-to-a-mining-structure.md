---
title: Adicionar colunas a uma estrutura de mineração | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4c09d4b263dc4e4274888f6cbd8bf1f27103dd8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210211"
---
# <a name="add-columns-to-a-mining-structure"></a>Adicionar colunas a uma estrutura de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Use o Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para adicionar colunas a uma estrutura de mineração depois de defini-la no Assistente de Mineração de Dados. É possível adicionar qualquer coluna existente na exibição de fonte de dados que foi usada para definir a estrutura de mineração.  
  
> [!NOTE]  
>  Você pode adicionar várias cópias de colunas em uma estrutura de mineração, porém deve evitar o uso de mais de uma instância da coluna dentro do mesmo modelo, a fim de impedir correlações falsas entre a coluna de origem e a coluna derivada.  
  
### <a name="to-add-a-column-to-a-mining-structure"></a>Para adicionar uma coluna a uma estrutura de mineração  
  
1.  Selecione a guia **Estrutura de Mineração** no Designer de Mineração de Dados.  
  
2.  Clique com o botão direito do mouse na estrutura de mineração e selecione **Adicionar uma Coluna**.  
  
     A caixa de diálogo **Selecionar uma Coluna** é exibida.  
  
3.  Em **Tabela de Origem**, selecione a tabela na exibição de fonte de dados em que reside a coluna.  
  
4.  Em **Coluna de origem**, selecione a coluna que você quer adicionar à estrutura de mineração.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Se você adicionar uma coluna existente, uma cópia será incluída na estrutura, e o nome anexado com um "1". Você pode alterar o nome da coluna copiada para algo mais descritivo digitando um novo nome na propriedade **Nome** da coluna da estrutura de mineração.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções da estrutura de mineração](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
