---
title: Importar dados do Excel para Master Data Services (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 89fce454-a816-4b33-a26a-d1b9741d269b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 093f8a471210b73b8c3cdaf1b2bb083b31980c52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092285"
---
# <a name="import-data-from-excel-to-master-data-services-mds-add-in-for-excel"></a>Importar dados do Excel para Master Data Services (suplemento do MDS para Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], publique dados no repositório do MDS quando terminar seu trabalho no Excel e desejar salvar as alterações para que outros usuários tenham acesso a elas.  
  
> [!NOTE]
>  -   Quando você publicar alterações, os comentários das células gerenciadas pelo MDS serão excluídos.  
> -   Uma fórmula não tem suporte em uma célula gerenciada por MDS. Uma fórmula em uma célula gerenciada por MDS é tratada como um valor de texto.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   A planilha ativa deve conter dados gerenciados no MDS e você deve ter feito alterações ou adições aos dados gerenciados no MDS.  
  
-   Se você for adicionar membros, não precisará especificar um valor de **Código** se os códigos da entidade forem gerados automaticamente. Para obter mais informações, consulte [Criação automática de código &#40;Master Data Services&#41;](../../master-data-services/automatic-code-creation-master-data-services.md).  
  
### <a name="to-publish-data-to-the-mds-repository"></a>Para publicar dados no repositório do MDS  
  
1.  No grupo **Publicar e Validar** , clique em **Publicar**.  
  
2.  Opcional. Se a caixa de diálogo **Publicar e Anotar** for exibida, opte por compartilhar a mesma anotação (comentário) para todas as atualizações, ou por anotar cada alteração individualmente.  
  
3.  Opcional. Selecione a caixa de seleção **Não mostrar esta caixa de diálogo novamente** . Você sempre pode mostrar a caixa de diálogo no futuro escolhendo **Configurações** e marcando a caixa de seleção **Mostrar a caixa de diálogo Publicar e Anotar ao publicar** .  
  
4.  Clique em **Publicar**.  
  
> [!NOTE]  
>  Se você for adicionar novos membros (linhas) à sua planilha e não conseguir publicá-los com êxito no repositório do MDS, talvez você não tenha a permissão **Atualizar** para todos os atributos da planilha. Na guia **Revisão** , no grupo **Alterações** , clique em **Desproteger Planilha** e tente publicar novamente.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Aplicar regras de negócio &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral: Importando dados do Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)   
 [Validando dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
  
