---
title: Habilitar ou desabilitar a coleta de dados de uso e relatório de falhas
titleSuffix: Azure Data Studio
description: Este artigo explica como controlar se os dados de relatório de falhas e uso são coletados e enviados à Microsoft.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 71ed86e9ad076a41099eaf4e56fe67a25b5f2c21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958942"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Habilitar ou desabilitar a coleta de dados de uso para [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Como desabilitar o relatório de telemetria

[!INCLUDE[name-sos](../includes/name-sos-short.md)] coleta dados de uso e os envia à Microsoft para ajudar a melhorar nossos produtos e serviços. Para saber mais, leia as [declaração de privacidade](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Se você não quiser enviar dados de uso à Microsoft, você pode definir as *telemetry.enableTelemetry* definir como *falso*.

Para silenciar todos os eventos de telemetria da [!INCLUDE[name-sos](../includes/name-sos-short.md)], da **arquivo** > **preferências** > **configurações**, adicione a seguinte opção:

```json
    "telemetry.enableTelemetry": false
```

**Aviso importante**: Essa opção requer a reinicialização do [!INCLUDE[name-sos](../includes/name-sos-short.md)] entrem em vigor. 

## <a name="how-to-disable-crash-reporting"></a>Como desabilitar o relatório de falhas

Para desabilitar o relatório de falhas, de **arquivo** > **preferências** > **configurações**, adicione a seguinte opção:

```json
    "telemetry.enableCrashReporter": false
```

**Aviso importante**: Essa opção requer a reinicialização do [!INCLUDE[name-sos](../includes/name-sos-short.md)] entrem em vigor.

## <a name="additional-resources"></a>Recursos adicionais
- [Configurações de espaço de trabalho e usuário](settings.md)
