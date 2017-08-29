---
title: Desenvolvendo um enumerador ForEach personalizado | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom foreach enumerators [Integration Services]
- custom foreach enumerators [Integration Services], about custom foreach enumerators
- foreach enumerators [Integration Services]
ms.assetid: bffe26e0-1b9a-47ad-bae6-6b708cb4cf4f
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 193fc8958826ac2bc382d5717a4f72690607a217
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-custom-foreach-enumerator"></a>Desenvolvendo um enumerador de ForEach personalizado
  O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] usa enumeradores foreach para iterar sobre os itens de uma coleção e executar as mesmas tarefas para cada elemento. O [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui vários enumeradores foreach que dão suporte às coleções mais usadas, como todos os arquivos de uma pasta, todas as tabelas de um banco de dados ou todos os elementos de uma lista armazenada em uma variável de pacote. Se os enumeradores de foreach e as coleções fornecidos não satisfizerem seus requisitos completamente, você poderá criar um enumerador de foreach personalizado.  
  
 Para criar um enumerador de foreach personalizado, é preciso criar uma classe que herde da classe base <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>, aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> em sua nova classe e substituir os métodos e propriedades importantes da classe base, incluindo o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>.  
  
## <a name="in-this-section"></a>Nesta seção  
 Esta seção descreve como criar, configurar e codificar um enumerador foreach personalizado e sua interface de usuário personalizada.  
  
 [Criação de um enumerador de Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)  
 Descreve como criar as classes para um projeto de enumerador foreach personalizado.  
  
 [Codificando um enumerador Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
 Descreve como implementar um enumerador de foreach personalizado anulando os métodos e propriedades da classe base.  
  
 [Desenvolvendo uma Interface de usuário para um enumerador ForEach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
 Descreve como implementar a classe de interface do usuário e o formulário usado para configurar o enumerador foreach personalizado.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
### <a name="information-common-to-all-custom-objects"></a>Informações comuns a todos os objetos personalizados  
 Para obter informações comuns a todos os tipos de objetos personalizados que você pode criar no [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os tópicos a seguir:  
  
 [Desenvolvendo objetos personalizados para o Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Descreve as etapas básicas para implementar todos os tipos de objetos personalizados para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Persistência de objetos personalizados](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Descreve a persistência personalizada e explica quando ela é necessária.  
  
 [Compilando, implantando e depurando objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Descreve as técnicas para compilar, assinar, implantar e depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Informações sobre outros objetos personalizados  
 Para obter informações sobre os outros tipos de objetos personalizados que você pode criar em [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], consulte os seguintes tópicos:  
  
 [Desenvolvendo uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Aborda como programar tarefas personalizadas.  
  
 [Desenvolvendo um Gerenciador de Conexão personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Aborda como programar gerenciadores de conexões personalizados.  
  
 [Desenvolvendo um provedor de Log personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Aborda como programar provedores de log personalizados.  
  
 [Desenvolvendo um componente de fluxo de dados personalizados](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 Aborda como programar origens, transformações e destinos de fluxos de dados personalizados.  
 