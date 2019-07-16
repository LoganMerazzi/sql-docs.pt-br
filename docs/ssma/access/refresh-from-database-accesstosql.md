---
title: Atualização do banco de dados (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3b671f49-c4cc-44fd-801e-e738a8c79415
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 209ed616f3993a0a93b802ddeca39a7065485afc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051535"
---
# <a name="refresh-from-database-accesstosql"></a>Atualização do banco de dados (AccessToSQL)
O **Refresh do banco de dados** caixa de diálogo permite que você selecione quais objetos para atualizar a partir do banco de dados do Access. Linhas na caixa de diálogo são codificadas por cores com base no estado de metadados:  
  
-   Se os metadados do objeto foi alterado localmente e no banco de dados do Access, a linha é azul.  
  
-   Se os metadados do objeto foi alterado no banco de dados do Access, mas não no SSMA, a linha será amarela.  
  
-   Se os metadados do objeto foi alterado localmente, mas não no banco de dados de acesso, a linha está verde.  
  
-   Se o objeto é novo no banco de dados do Access, a linha é rosa.  
  
Você pode especificar configurações de atualização do objeto padrão no **configurações do projeto** caixa de diálogo. Para obter mais informações, consulte [configurações do projeto &#40;carregamento de objetos&#41; &#40;AccessToSQL&#41;](../../ssma/access/project-settings-loading-objects-accesstosql.md)  
  
Para acessar o **de atualização do banco de dados** diálogo caixa, em qualquer **banco de dados** nó no Gerenciador de metadados de acesso e clique em **atualização do banco de dados**.  
  
