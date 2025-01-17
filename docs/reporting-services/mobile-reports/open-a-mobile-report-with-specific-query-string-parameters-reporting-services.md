---
title: Abrir um relatório móvel com parâmetros de cadeia de consulta específicos | Microsoft Docs
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7204574d10b674c7cea4e08fb570c3550fe33e03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62499970"
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>Abrir um relatório móvel com parâmetros de cadeia de consulta específicos | Reporting Services
Se você tiver um relatório móvel [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] com parâmetros e uma fonte de dados [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)], poderá incluir parâmetros de cadeia de consulta na URL do relatório para que abra automaticamente com os valores especificados. 
1.  Crie um [relatório móvel com parâmetros](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md).

2. Abra o relatório no Publicador de Relatórios Móveis e selecione a guia Dados. 

2. Encontre o nome do conjunto de dados na guia, na parte inferior da tabela, e o nome do campo desejado. 
    
    ![mobile-report-publisher-parameter-data-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  A sintaxe da URL depende de sua fonte de dados. 

     **Para uma fonte de dados do SQL Server Analysis Services**: compile uma URL com um parâmetro de cadeia de caracteres de consulta neste formato:

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    Por exemplo:
    
    `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **Para uma fonte de dados do SQL Server**: o parâmetro de cadeia de caracteres de consulta é praticamente o mesmo, mas tem o símbolo \@ na frente do nome do campo:

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    Por exemplo:
    
      `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  Essa URL abrirá o relatório no servidor, automaticamente filtrado para o valor de parâmetro especificado.

    ![mobile-report-publisher-parameter-web-portal-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>Confira também

[Adicionar parâmetros a um relatório móvel](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

