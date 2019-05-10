---
title: Criar um índice (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d694a105-69b1-4ff6-99d3-1f408b916b81
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 008c1915c793eedb27d70cac27e135c2c7e753c4
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65477085"
---
# <a name="create-an-index-master-data-services"></a>Criar um índice (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Crie um índice personalizado em uma lista de atributos que você consulta com frequência para melhorar o desempenho da consulta.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional Administração do Sistema. Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 **Para criar um índice**  
  
1.  No Master Data Manager, clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , selecione um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , na **grade** , selecione a linha para a entidade para a qual você deseja criar o índice.  
  
4.  Clique em **Índices**.  
  
5.  Na caixa **Nome** , digite um nome para o índice.  
  
6.  Escolha **É Exclusivo** se quiser criar um índice exclusivo. Para obter mais informações sobre tipos de índice, consulte [Índice personalizado &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
  
7.  Clique nos atributos na caixa **Atributos Disponíveis** e clique na seta **Adicionar** . Para adicionar todos os atributos, clique na seta **Adicionar Tudo** .  
  
8.  Clique em **Salvar**.  
  
 Para cada índice criada, uma linha com quatro colunas é adicionada à grade. A tabela a seguir descreve as colunas.  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|Status|O status do índice.<br /><br /> Quando você clica em **Salvar**, a imagem ![Ícone para o status de atualização](../master-data-services/media/mds-statusicon-updating.png "Ícone para o status de atualização") é exibida, indicando que o índice está sendo atualizado.<br /><br /> Se houver erros ao criar ou editar um índice, a imagem ![Ícone para o status de erro](../master-data-services/media/mds-statusicon-error.png "Ícone para o status de erro") será exibida.<br /><br /> Caso contrário, o status será OK e a imagem ![Ícone para o status OK](../master-data-services/media/mds-statusicon-ok.png "Ícone para o status OK") será exibida.|  
|Nome|O nome do índice.|  
|É Exclusivo|Especifica se o índice é exclusivo.|  
|Sobre atributos|Mostra os nomes de exibição de atributos nos quais o índice é definido.|  
  
 Quando você clica em um índice, as informações a seguir são exibidas.  
  
-   **Criado por**: O nome do usuário que criou o índice.  
  
-   **Em**: A data e a hora em que o índice foi criado.  
  
-   **Atualizado por**: O nome do usuário que atualizou o índice pela última vez.  
  
-   **Em**: A data e a hora em que o índice foi atualizado pela última vez.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Editar e excluir um índice &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Índice personalizado &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)  
  
  
