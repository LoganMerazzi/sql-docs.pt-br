---
title: Opções de configuração de servidor access check cache | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: cc290a3fbde8426c1728a03b4ec9ddeaf4d5144f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782479"
---
# <a name="access-check-cache-server-configuration-options"></a>Opções access check cache de configuração de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Quando objetos de banco de dados são acessados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a verificação de acesso é armazenada em cache em uma estrutura interna chamada **cache de resultado de verificação de acesso**. As opções **cota de cache de verificação de acesso** e a **contagem de compartimentos de cache de acesso** controlam o número de entradas e o número de compartimentos de hash usados para o **cache de resultado de verificação de acesso**. Em circunstâncias raras, o desempenho pode ser melhorado alterando essas opções.  
  
 Os valores padrão de 0 indicam aquele o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está gerenciando essas opções. A Microsoft recomenda a alteração dessas opções apenas quando orientadas pelos Serviços de Atendimento ao Cliente da Microsoft.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
