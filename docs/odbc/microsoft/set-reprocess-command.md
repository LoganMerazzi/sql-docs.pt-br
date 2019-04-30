---
title: Comando SET REPROCESS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41877986d5d0e8afdfb30841860df360efd26da0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159375"
---
# <a name="set-reprocess-command"></a>Comando SET REPROCESS
Especifica quantas vezes ou para saber como longo para bloquear um arquivo ou um registro após uma tentativa malsucedida de bloqueio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>Argumentos  
 PARA *nAttempts*[segundos]  
 Especifica o número de vezes ou o número de segundos para tentar bloquear um arquivo ou registro após a tentativa inicial bem-sucedida. O valor padrão é 0; o valor máximo é de 32.000.  
  
 SEGUNDOS Especifica que o Visual FoxPro tenta bloquear um arquivo de registro ou de *nAttempts* segundos. Ele está disponível apenas quando *nAttempts* é maior que zero.  
  
 Por exemplo, se *nAttempts* é 30, Visual FoxPro tenta bloquear um registro ou arquivos de até 30 vezes. Se você incluir também segundos (definir REPROCESSAR a 30 segundos), do Visual FoxPro continuamente tenta bloquear um arquivo ou registro de até 30 segundos.  
  
 Se uma rotina de ON ERROR está em vigor e tentativas por um comando para bloquear o registro ou arquivo não tiverem êxito, a rotina de ON ERROR é executada. No entanto, se o bloqueio de tentativas de uma função, uma rotina de ON ERROR não será executada e a função retornará False (. F.).  
  
 Se uma rotina de ON ERROR não está em vigor, um comando tenta bloquear o registro ou arquivo e o bloqueio não pode ser colocado, um erro será gerado. Se uma função tenta colocar o bloqueio, o alerta não será exibido e a função retornará False (. F.).  
  
 Se *nAttempts* é 0 (o valor padrão) e emitir um comando ou função que tenta bloquear um arquivo ou registro, do Visual FoxPro tenta bloquear o registro ou arquivo indefinidamente. Se o registro ou o arquivo se torna disponível para bloquear enquanto espera, o bloqueio e a mensagem do sistema está desmarcada. Se uma função tentar colocar o bloqueio, a função retorna True (. T.).  
  
 Se uma rotina de ON ERROR está em vigor e um comando está tentando bloquear o registro ou o arquivo, a rotina de ON ERROR prevalece sobre tentativas adicionais para bloquear o registro ou arquivo. A rotina de ON ERROR é executada imediatamente. Do Visual FoxPro não tenta fazer registro adicional ou bloqueios de arquivo e não exibe a mensagem do sistema.  
  
 Se *nAttempts* é 1, do Visual FoxPro tenta bloquear o registro ou arquivo indefinidamente e uma rotina de ON ERROR não é executada.  
  
 Se um bloqueio foi colocado por outro usuário no arquivo que você está tentando bloquear ou registro, você deve aguardar até que o usuário libera o bloqueio.  
  
 COMO AUTOMÁTICO  
 Especifica que o Visual FoxPro tenta bloquear o registro ou arquivo indefinidamente. (O REPROCESSAMENTO conjunto como -2 é um comando equivalente.)  
  
## <a name="remarks"></a>Comentários  
 A primeira tentativa de bloquear um arquivo ou registro nem sempre é bem-sucedida. Com frequência, um registro ou o arquivo está bloqueado por outro usuário na rede. SET REPROCESS determina se o Visual FoxPro facilita adicional tenta bloquear o registro ou o arquivo quando a tentativa inicial for bem-sucedida. Você pode especificar quantas vezes tentativas adicionais são feitas ou quanto tempo as tentativas são feitas. Uma rotina de ON ERROR afeta como malsucedido bloqueio tentativas são tratadas.
