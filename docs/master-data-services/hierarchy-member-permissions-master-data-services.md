---
title: Permissões de membro de hierarquia (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], permissions
- permissions [Master Data Services], members
ms.assetid: b3880eed-1bf6-4f65-ab23-b08c194cc858
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 497bbda56028394547414aff5b360473445da9c1
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65485882"
---
# <a name="hierarchy-member-permissions-master-data-services"></a>Permissões de membro de hierarquia (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  As permissões de membro de hierarquia são opcionais e devem ser usadas somente quando você desejar que um usuário tenha acesso limitado a membros específicos. Se você não atribuir permissões na guia **Membros da Hierarquia** , as permissões do usuário serão baseadas somente nas permissões atribuídas na guia **Modelos** .  
  
 As permissões de membros de hierarquia são atribuídas na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na área funcional **Usuário e Permissões de Grupo** da guia **Membros da Hierarquia** . Estas permissões determinam quais membros um usuário pode acessar na área funcional do **Gerenciador** da interface do usuário.  
  
 Na guia **Membros da Hierarquia** , cada hierarquia é representada como uma estrutura de árvore. Quando você atribuir permissão para um nó na árvore, todos os filhos herdam essa permissão a menos que ela seja atribuída explicitamente a um nível inferior.  
  
> [!NOTE]  
>  Quando você atribuir permissão para um nó em uma hierarquia, todos os membros de todos os outros nós no mesmo nível ou superior serão recusados implicitamente.  
  
 No **Gerenciador**, as permissões de membro são aplicadas em todos lugares em que o membro é exibido. Por exemplo, um membro com permissão de **leitura** pode ler quaisquer entidades, hierarquias e coleções às quais pertença.  
  
 As permissões de membro de hierarquia aplicam-se à versão do modelo que recebe as permissões, e a qualquer cópia futura da versão. Elas não se aplicam a versões anteriores a que você está atribuindo.  
  
|Permissão|Descrição|  
|----------------|-----------------|  
|**leitura**|Os membros são exibidos.<br /><br /> <br /><br /> Observação: Se você atribuir apenas a permissão **Leitura** a **Raiz**, os membros de **Raiz** serão somente leitura; porém, em hierarquias e coleções explícitas, o usuário poderá mover os membros para **Raiz** e adicionar novos membros a **Raiz**.|  
|**Criar**|A permissão Criar não está disponível na permissão de membro da hierarquia.|  
|**Update (atualizar)**|Os membros são exibidos e o usuário pode alterá-los. O usuário também pode mover os membros em qualquer hierarquia explícita ou coleções a que os membros pertencem.|  
|**Delete (excluir)**|Os membros são exibidos e o usuário pode excluí-los.|  
|**Deny**|Os membros não são exibidos.|  
  
 Na guia **Membros da Hierarquia** , as permissões que você atribui não entram em vigor imediatamente. A frequência com que as permissões são aplicadas depende da **Configuração de intervalo de processamento da segurança de membro** na tabela de Configurações do Sistema no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . É possível aplicar permissões de membros imediatamente seguindo as etapas em [Aplicar permissões de membros imediatamente &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md).  
  
> [!NOTE]  
>  Não é possível atribuir permissões de membro de hierarquia a hierarquias recursivas, hierarquias derivadas com delimitações explícitas e a hierarquias derivadas com níveis ocultos.  
  
## <a name="possible-overlapping-permissions"></a>Permissões sobrepostas possíveis  
 Ao atribuir permissão para membros, pode ser necessário resolver permissões sobrepostas.  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>Quando um membro pertence a várias hierarquias  
 Duas ou mais hierarquias podem conter o mesmo membro.  
  
-   Se um nó de hierarquia receber permissão **Atualizar** e outra receber **Leitura**, então os membros no nó serão **Leitura**.  
  
-   Se as permissões **Atualizar** e **Criar** forem atribuídas a um nó da hierarquia e outro receber as permissões **Atualizar** e **Excluir** , então os membros do nó poderão ser atualizados.  
  
-   Se uma combinação de permissões **Criar**/**Ler**/**Atualizar**/**Excluir** for atribuída a um nó de hierarquia e outro nó receber permissões **Negar** , o acesso aos membros do nó será negado.  
  
## <a name="external-resources"></a>Recursos externos  
 Postagem do blog, [Aprimoramentos de Segurança](https://go.microsoft.com/fwlink/p/?LinkId=615376), em msdn.com.  
  
## <a name="see-also"></a>Consulte também  
 [Atribuir permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Hierarquias &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md)   
 [Aplicar permissões de membros imediatamente &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md)  
  
  
