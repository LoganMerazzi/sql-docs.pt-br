---
title: Patches de Software da Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], Oraclesoftware patches
- Oracle software patches [ODBC]
ms.assetid: 1275157b-f4e1-4c24-b273-c02555e261c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fce38aabddfc3891314940d4b7cb21f02965c083
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100773"
---
# <a name="oracle-software-patches"></a>Patches de software da Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Patches para os produtos de servidor Oracle e o componente de cliente são necessários para o funcionamento adequado de vários produtos e tecnologias Microsoft, incluindo o Microsoft ODBC Driver para o Oracle, o Microsoft OLE DB Provider for Oracle, informações da Internet Services (IIS), serviços de componentes (ou Microsoft Transaction Server, se você estiver usando o Windows NT), e assim por diante.  
  
> [!NOTE]  
>  As instruções a seguir não podem ser completamente precisas, porque o site FTP do Oracle está sujeitas a alterações.  
  
### <a name="to-download-the-oracle-software-patches"></a>Para baixar os patches de software da Oracle  
  
1.  Conecte-se ao site de FTP público no oracle ftp.oracle.com. A ID de usuário é "anonymous" e a senha é seu endereço de email.  
  
2.  Navegue até o seguinte diretório: /server/wgt_tech/server/windowsNT.  
  
3.  Para baixar patches mais relevantes para o Windows 95, Windows 98 e Windows NT/Windows 2000, navegue até o subdiretório para sua versão do Oracle - 7.3 ou 8.0. Os dois subdiretórios são /73patchsets e /80patchsets.  
  
4.  Para baixar patches para a tecnologia de rede da Oracle, SQL * Net ou Net8, navegue até o diretório a seguir: / rede.  
  
 Acessar este site FTP do seu navegador da Web pode não funcionar. Se você tiver problemas, tente usar um cliente FTP "tradicional" ou usar o prompt de comando do DOS.  
  
> [!NOTE]  
>  Como o Oracle correções de bugs em versões atuais e, em seguida, retrofits-las em versões anteriores, usando os patches de software, é recomendável que você baixe o patch mais recente disponível. Isso é especialmente verdadeiro para os componentes de cliente do servidor Oracle. Se você tiver dúvidas sobre como instalar esses patches, contate o suporte da Oracle.
