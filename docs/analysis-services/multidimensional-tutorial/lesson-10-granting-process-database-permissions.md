---
title: Concedendo permissões de banco de dados do processo | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 75a3410dfaf97f2f20a84b0cf390fd71dbed0e32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403958"
---
# <a name="lesson-10---granting-process-database-permissions"></a>Lição 10: concedendo permissões de banco de dados de processo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Depois da instalação de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], todos os membros da função do administrador de servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nessa instância têm permissões em todo o servidor para executar qualquer tarefa na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Por padrão, nenhum outro usuário tem qualquer permissão para administrar ou exibir objetos na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
Um membro da função de administrador de servidor pode conceder acesso administrativo aos usuários no servidor tornando-os membros da função. Um membro da função de administrador de servidor também pode conceder acesso mais limitado aos usuários. Para isso, ele deve conceder permissões de acesso ou administrativas totais ou limitadas no nível de banco de dados. Permissões administrativas limitadas incluem permissões para processar ou ler definição no nível de banco de dados, cubo ou dimensão.  
  
Nas tarefas deste tópico, você definirá uma função de segurança Processar objetos de banco de dados que concede aos membros dessa função permissão para processar todos os objetos de banco de dados, mas não para exibir dados contidos nesse banco de dados.  
  
## <a name="defining-a-process-database-objects-security-role"></a>Definindo uma função de segurança Processar objetos de banco de dados  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Funções** e clique em **Nova Função** para abrir o Designer de Função.  
  
2.  Clique na caixa de seleção **Processar banco de dados** .  
  
3.  Na janela Propriedades, altere a propriedade **Nome** dessa nova função para **Função Processar objetos de banco de dados**.  
  
    ![Designer de função](../media/l10-security-1.png "Designer de função")  
  
4.  Alterne para a guia **Associação** do Designer de Função e clique em **Adicionar**.  
  
5.  Insira as contas dos usuários ou grupos do domínio do Windows que serão membros dessa função. Clique em **Verificar Nomes** para verificar as informações das contas e clique em **OK**.  
  
6.  Alterne para a guia **Cubos** do Designer de Função.  
  
    Observe que os membros dessa função têm permissão para processar este banco de dados, mas não para acessar os dados no cubo do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e também não têm acesso ao cubo/detalhamento local, conforme mostrado na imagem a seguir:  
  
    ![Guia cubos do Designer de função](../media/l10-security-2.png "guia cubos do Designer de função")  
  
7.  Alterne para a guia **Dimensões** do Designer de Função.  
  
    Observe que os membros dessa função têm permissões para processar todos os objetos da dimensão neste banco de dados e, por padrão, têm permissão de leitura para acessar cada objeto de dimensão no banco de dados do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
8.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
    Você definiu e implantou com êxito a função de segurança Processar objetos de banco de dados. Depois que o cubo for implantado no ambiente de produção, os administradores desse cubo poderão adicionar usuários a essa função, conforme necessário para delegar responsabilidades de processamento a determinados usuários.  
  
> [!NOTE]  
> Um projeto completo para a Lição 10 pode ser obtido por meio do download e instalação dos exemplos. Para obter mais informações, consulte [Instalar dados de exemplo e projetos para o tutorial de modelagem multidimensional do Analysis Services](install-sample-data-and-projects.md).  
  
## <a name="see-also"></a>Consulte também  
[Funções e permissões &#40;Analysis Services&#41;](../multidimensional-models/roles-and-permissions-analysis-services.md)  
  
  
  
