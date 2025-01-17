---
title: Permissões de objeto de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e652d2c42c61e1694c1f8adfa7976f3c1eda8406
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055741"
---
# <a name="model-object-permissions-master-data-services"></a>Permissões de objeto de modelo (Serviços de Dados Mestre)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  As permissões do objeto de modelo são obrigatórias. Elas determinam os atributos que um usuário pode acessar na área funcional **Explorer** da interface do usuário.  
  
 Por exemplo, se você atribuir uma permissão **Atualizar** de usuário à entidade Produto, o usuário poderá atualizar todos os atributos dessa entidade. Se você atribuir a permissão **Atualizar** a um único atributo, o usuário só poderá atualizar esse atributo.  
  
 Para determinar a segurança atribuída em cada valor de atributo individual, permissões de objeto modelo são combinadas com permissões de membro de hierarquia, que determinam os membros que um usuário pode acessar.  
  
 Para conceder a um usuário acesso a uma área funcional, que não seja o **Explorer**, esse usuário precisa ser o administrador de modelo, o que também envolve a atribuição de permissões de Administrador no objeto de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 As permissões de objeto de modelo são atribuídas na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], na área funcional **Permissões para Usuário e Grupo** da guia **Modelos**. Nesta guia, o modelo é representado como uma estrutura de árvore. Quando você atribui uma permissão a um objeto na árvore, todos os objetos abaixo herdam a permissão. Você pode substituir essa herança atribuindo permissões aos objetos individuais.  
  
 Você pode atribuir uma combinação permissões Ler, Criar, Atualizar e Excluir ou Negar para objetos de modelo. Se você não atribuir nenhuma permissão na guia **Modelos** , o usuário não poderá exibir modelos nem dados no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="best-practice"></a>Prática recomendada  
 Em geral, é necessário atribuir a permissão **ALL** ao objeto modelo e atribuir explicitamente a permissão aos objetos subjacentes.  
  
## <a name="external-resources"></a>Recursos externos  
 Postagem do blog, [Aprimoramentos de Segurança](https://go.microsoft.com/fwlink/p/?LinkId=615376), em msdn.com.  
  
## <a name="see-also"></a>Consulte também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões de modelo &#40;Master Data Services&#41;](../master-data-services/model-permissions-master-data-services.md)   
 [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)   
 [Permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
