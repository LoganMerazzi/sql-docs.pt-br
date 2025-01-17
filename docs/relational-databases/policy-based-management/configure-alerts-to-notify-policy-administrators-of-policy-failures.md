---
title: Configurar alertas para notificar os administradores de políticas sobre falhas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ef46a36296da926f2cb62599b41774b1d29f5ba1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109826"
---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>Configurar alertas para notificar os administradores de políticas sobre falhas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando as políticas do Gerenciamento Baseado em Políticas são executadas em um dos três modos de avaliação automatizados, se ocorrer uma violação de política, uma mensagem será gravada no log de eventos. Para ser notificado quando essa mensagem for gravada no log de eventos, você pode criar um alerta para detectar a mensagem e executar uma ação. O alerta deve detectar as mensagens como mostra a tabela a seguir.  
  
|Modo de execução|Número da mensagem|  
|--------------------|--------------------|  
|Ao alterar: impedir<br /><br /> (se automático)|34050|  
|Ao alterar: impedir<br /><br /> (se por demanda)|34051|  
|Ao agendar|34052|  
|Ao alterar|34053|  
  
 Para configurar um alerta para responder às mensagens de erro do Gerenciamento Baseado em Políticas, consulte os seguintes tópicos:  
  
-   [Criar um operador](../../ssms/agent/create-an-operator.md)  
  
-   [Criar um alerta usando um número de erro](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Atribuir alertas a um operador](../../ssms/agent/assign-alerts-to-an-operator.md)  
  
## <a name="permissions"></a>Permissões  
 Quando as políticas são avaliadas por demanda, elas são executadas no contexto de segurança do usuário. Para gravar no log de erros, o usuário deve ter permissões ALTER TRACE ou ser um membro da função de servidor fixa sysadmin. As políticas avaliadas por um usuário que tenha menos privilégios não são gravadas no log de eventos e não disparam um alerta.  
  
 Os modos de execução automatizados são executados como um membro da função sysadmin. Isso permite que a política grave no log de erros e gere um alerta.  
  
## <a name="additional-considerations-about-alerts"></a>Considerações adicionais sobre alertas  
 Esteja atento às seguintes considerações adicionais sobre alertas:  
  
-   Os alertas só são gerados para políticas que estiverem habilitadas. Como as políticas **Sob demanda** não podem ser habilitadas, não são gerados alertas para políticas executadas sob demanda.  
  
-   Se a ação que você deseja executar incluir o envio de um email, você deverá configurar uma conta de email. É recomendável usar o Database Mail. Para obter mais informações sobre como configurar o Database Mail, veja [Criar uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md).  
  
  
