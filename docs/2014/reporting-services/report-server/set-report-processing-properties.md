---
title: Definir as propriedades do processamento de relatório | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- on-demand reports
- report processing [Reporting Services], execution properties
- snapshots [Reporting Services], running reports from
- cached reports [Reporting Services]
- report snapshots [Reporting Services], running reports from
- report execution snapshots [Reporting Services]
ms.assetid: b5cbc453-5986-423e-af44-1f243ef3edb1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a793fa513ef13c9cafc210a411971a0363f5976d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103237"
---
# <a name="set-report-processing-properties"></a>Definir propriedades de processamento de relatórios
  Propriedades de execução de relatório controlam como um relatório é processado. É necessário definir propriedades de execução individualmente para cada relatório.  
  
 Para definir propriedades de execução de relatório, abra o relatório no Gerenciador de Relatórios e então navegue até a página Propriedades de Execução. Você também pode definir propriedades usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obter mais informações, consulte [Página de propriedades Opções de Processamento &#40;Gerenciador de Relatórios&#41;](../processing-options-properties-page-report-manager.md).  
  
## <a name="report-execution-modes"></a>Modos de execução de relatório  
 É possível executar um relatório sob demanda ou como um instantâneo. A seção a seguir descreve cada tipo de abordagem.  
  
### <a name="running-reports-on-demand"></a>Executando relatórios sob demanda  
 É possível especificar que um relatório consulte uma fonte de dados sempre que um usuário executar o relatório, resultando em relatórios sob demanda que contêm os dados mais atualizados. Uma nova instância do relatório é criada para cada usuário que abre ou solicita o relatório; cada nova instância contém os resultados de uma nova consulta. Com essa abordagem, se dez usuários abrirem o relatório simultaneamente, dez consultas serão enviadas à fonte de dados para processamento.  
  
### <a name="running-reports-on-demand-from-cache"></a>Executando relatórios sob demanda do cache  
 Para aprimorar o desempenho, é possível especificar um relatório (e dados) para serem registrados no cache temporariamente quando um usuário executar um relatório. A cópia armazenada em cache fica subsequentemente disponível a outros usuários que acessam o mesmo relatório. Com essa abordagem, se dez usuários abrirem o relatório, somente a primeira solicitação resultará em processamento de relatório. O relatório é subsequentemente armazenado em cache e os demais nove usuários visualizam o relatório armazenado em cache.  
  
 Relatórios armazenados em cache são removidos do cache em intervalos definidos pelo usuário. Você pode especificar intervalos em minutos ou agendar uma data e hora específica para esvaziar o cache. Para obter mais informações, consulte [Armazenando relatórios em cache &#40;SSRS&#41;](caching-reports-ssrs.md).  
  
### <a name="running-reports-from-snapshots"></a>Executando relatórios de instantâneos  
 Um instantâneo de relatório é um relatório que contém informações e dados sobre layout recuperados em um momento específico. Você pode executar um relatório como instantâneo de relatório para evitar que o relatório seja executado em momentos arbitrários (durante um backup agendado, por exemplo). Um instantâneo de relatório normalmente é criado e, em seguida, atualizado de acordo com um agendamento, permitindo marcar o horário exato em que ocorrerá o processamento de dados e do relatório. Se um relatório basear-se em consultas cujo processamento seja demorado ou que utilizem dados de uma fonte de dados que prefira que não seja acessada durante determinadas horas, você deverá executar o relatório como instantâneo.  
  
 Um instantâneo de relatório é armazenado em um banco de dados do servidor de relatórios, do qual é posteriormente recuperado quando um usuário ou processo (por exemplo, uma assinatura) solicita o relatório. Quando um instantâneo de relatório é atualizado, ele é substituído por uma nova instância. O servidor de relatório não salva versões anteriores de um instantâneo de relatório, a menos que você defina especificamente opções para adicioná-lo ao histórico de relatórios. Para obter mais informações, consulte [Criar, modificar e excluir instantâneos no Histórico de Relatórios](create-modify-and-delete-snapshots-in-report-history.md).  
  
 Nem todos os relatórios podem ser configurados para execução como instantâneos. Não é possível criar um instantâneo para um relatório que solicite aos usuários credenciais ou que use a segurança integrada do Windows para obter dados para o relatório. Se você desejar executar como instantâneo um relatório com parâmetros, deverá especificar um parâmetro padrão a ser usado na criação do instantâneo. Ao contrário dos relatórios executados sob demanda, não é possível especificar um valor de parâmetro diferente para um instantâneo de relatório quando o relatório está aberto. A escolha de outro parâmetro resultaria em uma nova solicitação de processamento de relatório, o que não é permitido.  
  
 Em alguns casos, a configuração de um relatório sob demanda para que seja executado como instantâneo pode desativar assinaturas. A condição a seguir fará com que um servidor de relatório desative assinaturas existentes definidas quando o relatório foi configurado para execução sob demanda:  
  
-   O relatório usa parâmetros de consulta e você seleciona um valor específico como parâmetro padrão para atender aos requisitos de execução do relatório como instantâneo.  
  
-   Assinaturas já existentes são configuradas para usarem valores de parâmetros diferentes do valor de parâmetro padrão especificado para o instantâneo.  
  
 Quando existir essa condição, o servidor de relatório desativará a assinatura na próxima vez em que a assinatura for agendada para execução. Abra a assinatura e salve-a a fim de reativá-la. Quando você abrir a assinatura, o servidor de relatórios atualizará os valores de parâmetros de assinatura para aqueles especificados para o relatório. Para obter mais informações sobre assinaturas, consulte [Assinaturas e entrega &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Definir opções de processamento &#40;Reporting Services no modo integrado do SharePoint&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Configurar propriedades de execução de um relatório &#40;Gerenciador de Relatórios&#41;](../reports/configure-execution-properties-for-a-report-report-manager.md)   
 [Conceitos do Reporting Services &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)   
 [Como: Adicionar um instantâneo ao histórico de relatórios](add-a-snapshot-to-report-history-report-manager.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
