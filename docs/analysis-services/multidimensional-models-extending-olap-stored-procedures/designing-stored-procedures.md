---
title: Projetando procedimentos armazenados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a617df9d88bde17c08fb4d2235ad751a5609e2d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68181090"
---
# <a name="designing-stored-procedures"></a>Projetando procedimentos armazenados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Tanto o Analysis Management Objects (AMO) do modelo de objeto administrativo como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® Data Objects (Multidimensional) (ADO MD) do modelo de objeto orientado a cliente estão disponíveis nos procedimentos armazenados.  
  
 Os procedimentos armazenados devem estar no escopo (do servidor ou do banco de dados) para serem visíveis no nível da linguagem MDX que serão chamadas. No entanto, uma vez um chamado o procedimento armazenado, seu escopo não fica limitado a ações sob seu pai. Um procedimento armazenado pode fazer alterações ou modificações em qualquer lugar do servidor, sujeito apenas às limitações de segurança do processo do usuário que o chama ou às limitações da transação em que está operando.  
  
 Procedimentos de escopo de servidor ficam disponíveis em todos os contextos no servidor. Procedimentos armazenados de escopo de banco de dados ficam visíveis apenas no contexto do banco de dados no qual foram definidos.  
  
 Como toda função MDX, o procedimento armazenado deve ser resolvido antes que a sessão MDX possa prosseguir; os procedimentos armazenados bloqueiam as sessões MDX durante sua execução. A menos que exista um motivo específico para parar uma sessão MDX à espera de uma interação do usuário, qualquer interação do usuário (como caixas de diálogo) não são aconselhadas.  
  
## <a name="dependent-assemblies"></a>Assemblies dependentes  
 Todos os assemblies dependentes devem ser carregados em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para serem localizados pelo CLR (Common Language Runtime). O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] armazena os assemblies dependentes na mesma pasta do assembly principal, de modo que o CLR resolve automaticamente todas as referências das funções para as funções desses assemblies.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de Assemblies de modelo multidimensional](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definindo procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
