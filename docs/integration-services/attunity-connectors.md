---
title: Microsoft Connectors para Oracle e Teradata da Attunity (SSIS) | Microsoft Docs
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ''
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4bdd68dccdcf8c2b317c81b120feb6949bb96c6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027568"
---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Microsoft Connectors para Oracle e Teradata da Attunity para SSIS (Integration Services)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Você pode baixar os conectores para o Integration Services da Attunity que otimizam o desempenho ao carregar dados de ou para Oracle ou Teradata em um pacote do SSIS.

## <a name="download-the-latest-attunity-connectors"></a>Baixar os conectores Attunity mais recentes

Obtenha a versão mais recente dos conectores aqui:  
[Microsoft Connectors v5.0 para Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>Problema – os conectores da Attunity não estão visíveis na caixa de ferramentas do SSIS

Para ver os conectores da Attunity na caixa de ferramentas do SSIS, sempre é necessário instalar a versão dos conectores que se destina à mesma versão do SQL Server que a versão do SSDT (SQL Server Data Tools) instalado em seu computador. (Você também pode ter versões anteriores dos conectores instalados.) Esse requisito é independente da versão do SQL Server que você deseja usar como destino em seus pacotes e projetos do SSIS.

Por exemplo, se você instalou a versão mais recente do SSDT, você tem a versão 17 do SSDT com um número de build que começa com 14. Essa versão do SSDT adiciona suporte ao SQL Server 2017. Para ver e usar os conectores da Attunity no desenvolvimento de pacotes do SSIS – mesmo que você deseje usar uma versão anterior do SQL Server como destino – você também precisará instalar a versão mais recente dos conectores da Attunity, versão 5.0. Essa versão dos conectores também adiciona suporte ao SQL Server 2017.

Verifique a versão instalada do SSDT no Visual Studio de **Ajuda** | **Sobre o Microsoft Visual Studio** ou em **Programas e Recursos** no Painel de Controle. Em seguida, instale a versão correspondente dos conectores da Attunity da tabela a seguir.

|Versão do SSDT|Número de build do SSDT|Versão do SQL Server de destino|Versão necessária do Connectors|
|---------|---------|---------|---------|
|17|Inicia com 14|SQL Server 2017|[Microsoft Connectors v5.0 para Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|Inicia com 13|SQL Server 2016|[Microsoft Connectors v4.0 para Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>Baixar o SSDT (SQL Server Data Tools) mais recente

Obtenha a versão mais recente do SSDT aqui:  
[Baixar o SQL Server Data Tools (SSDT)](..//ssdt/download-sql-server-data-tools-ssdt.md)
