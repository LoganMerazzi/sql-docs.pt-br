---
title: Geral (caixa de diálogo de opções de armazenamento) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.storage.f1
ms.assetid: ee1fac79-ae15-4c3c-9a98-33db04388817
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3c7ddd5311232ae12b3eb9f66adc0cd1f5714b32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081004"
---
# <a name="general-storage-options-dialog-box-analysis-services---multidimensional-data"></a>Geral (caixa de diálogo Opções de Armazenamento) (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Geral** da caixa de diálogo **Opções de Armazenamento** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir configurações de modo de armazenamento e cache pró-ativo para uma dimensão, cubo, grupo de medidas ou partição.  
  
> [!NOTE]  
>  Você deve estar familiarizado com a funcionalidade de modo de armazenamento e de cache pró-ativo para modificar essas configurações. Para obter mais informações, consulte [Cache pró-ativo &#40;Partições&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Modo de armazenamento**|Seleciona o modo de armazenamento a ser usado para o objeto.<br /><br /> **MOLAP**<br /> O objeto usa armazenamento MOLAP (OLAP multidimensional).<br /><br /> **HOLAP**<br /> O objeto usa armazenamento HOLAP (OLAP híbrido).<br /><br /> **ROLAP**<br /> O objeto usa armazenamento ROLAP (OLAP relacional).|  
|**Habilitar cache pró-ativo**|Habilita o cache pró-ativo.<br /><br /> Observação: Se essa opção não estiver selecionada, todas as opções, exceto **modo de armazenamento** estão desabilitados.|  
|**Atualizar o cache quando os dados forem alterados**|Usa o método de notificação selecionado na guia **Notificações** para atualizar a imagem MOLAP do objeto sempre que uma notificação for recebida. Para obter mais informações sobre a guia **Notificações**, consulte [Notificações &#40;Caixa de diálogo de opções de armazenamento&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md).<br /><br /> Observação: Essa opção estará desabilitada a menos que **Habilitar cache pró-ativo** está selecionado.|  
|**Intervalo de silêncio**|Define o intervalo mínimo e unidades de tempo no qual o objeto não tem atividades antes do cache pró-ativo começar a criar a nova imagem MOLAP para o objeto.<br /><br /> Observação: Essa opção estará desabilitada a menos que **atualizar o cache quando os dados forem alterados** está selecionado.|  
|**Substituição do intervalo de silêncio**|Define o intervalo máximo e unidades de tempo no qual, após uma notificação ser recebida para o objeto, o cache pró-ativo começa a criar a nova imagem MOLAP para o objeto, independentemente da atividade atual do objeto. Notificações recebidas depois que esse intervalo foi atingido não cancelam o processo de imagem MOLAP disparado por esse intervalo.<br /><br /> Observação: Essa opção estará desabilitada a menos que **atualizar o cache quando os dados forem alterados** está selecionado. Observe também que essa opção não deve ser definida se **modo de armazenamento** é definido como **HOLAP**.|  
|**Descartar cache desatualizado**|Especifica o período entre o início da criação de um novo cache MOLAP e a remoção do cache MOLAP existente.<br /><br /> Observação: Essa opção estará desabilitada a menos que **Habilitar cache pró-ativo** está selecionado. Observe também que essa opção não deve ser definida se **modo de armazenamento** estiver definida como HOLAP.|  
|**Latência**|Seleciona o intervalo e as unidades de tempo do período entre o início da criação de um novo cache MOLAP e a remoção do cache MOLAP existente.<br /><br /> Observação: Essa opção estará desabilitada a menos que **descartar cache desatualizado** está selecionado. Observe também que essa opção não deve ser definida se **modo de armazenamento** é definido como **HOLAP**.|  
|**Atualizar o cache periodicamente**|Atualiza a imagem MOLAP regularmente, independentemente da notificação.<br /><br /> Observação: Essa opção estará desabilitada a menos que **Habilitar cache pró-ativo** está selecionado. Observe também que essa opção não deve ser definida se **modo de armazenamento** é definido como **HOLAP**.|  
|**Intervalo de recriação**|Seleciona o intervalo e as unidades de tempo do período em que, após uma nova imagem MOLAP ser criada, o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] inicia o processo da imagem MOLAP novamente para o objeto, independentemente da notificação. Notificações recebidas depois que esse intervalo foi atingido não cancelam o processo de imagem MOLAP disparado por esse intervalo.<br /><br /> Observação: Essa opção estará desabilitada a menos que **atualizar o cache periodicamente** está selecionado. Observe também que essa opção não deve ser definida se **modo de armazenamento** é definido como **HOLAP**.|  
|**Colocar online imediatamente**|Coloca os objetos online imediatamente. Se essa opção estiver definida, os objetos usarão o armazenamento ROLAP subjacente para resolver consultas enquanto o cache MOLAP estiver sendo recriado. Se essa opção não estiver definida, os objetos serão colocados online apenas após o cache MOLAP ser concluído.|  
|**Habilitar agregações ROLAP**|Usa exibições materializadas na fonte de dados subjacente para armazenar agregações.<br /><br /> Observação: Se a fonte de dados subjacente não oferece suporte a exibições materializadas, ocorrerá um erro quando o objeto for processado.|  
|**Aplicar configurações a dimensões**|Aplica configurações de modo de armazenamento e de cache pró-ativo a dimensões associadas.|  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de opções de armazenamento &#40;Analysis Services - dados multidimensionais&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)   
 [Notificações &#40;caixa de diálogo de opções de armazenamento&#41; &#40;Analysis Services - dados multidimensionais&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)  
  
  
