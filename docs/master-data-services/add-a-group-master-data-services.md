---
title: Adicionar um grupo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- groups [Master Data Services], adding
- adding groups [Master Data Services]
ms.assetid: c7a88381-3b2c-4af7-9cf7-3a930c1abdee
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 725e43685f56c2a52c585acb7624064c85e01b4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047933"
---
# <a name="add-a-group-master-data-services"></a>Adicionar um grupo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Adicione um grupo à lista **Grupos** do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para iniciar o processo de atribuição de permissão ao aplicativo Web. Antes que um usuário do grupo possa acessar o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], é necessário atribuir a permissão de grupo a uma ou mais áreas funcionais e objetos de modelo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Permissões de Usuário e Grupo** .  
  
### <a name="to-add-a-group"></a>Para adicionar um grupo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Permissões de Usuário e Grupo**.  
  
2.  Na página **Usuários** , na barra de menus, clique em **Gerenciar Grupos**.  
  
3.  Clique em **Adicionar grupos**.  
  
4.  Digite o nome do grupo precedido pelo nome de domínio do Active Directory ou pelo nome do computador do servidor, como em *domain\group_name* ou *computer\group_name*.  
  
5.  Opcionalmente, clique em **Verificar nomes**.  
  
6.  Clique em **OK**.  
  
    > [!NOTE]  
    >  Quando o usuário acessar o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]pela primeira vez, seu nome será adicionado à lista de usuários do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Atribuir permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/assign-functional-area-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Segurança &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
