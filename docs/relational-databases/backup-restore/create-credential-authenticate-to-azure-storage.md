---
title: Criar credencial – autenticar no Armazenamento do Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 21ed98a3b770023140a414062f1b4d0941514579
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075990"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>Criar credencial - autenticar no Armazenamento do Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use a caixa de diálogo **Backup para URL – Criar Credencial** para criar uma nova Credencial do SQL.  
  
 Ao usar essa caixa de diálogo para criar uma credencial, você deve fornecer um Certificado de Gerenciamento do Windows Azure adicionado ao repositório de certificados local ou a um perfil de publicação baixado em seu computador para validar a assinatura e as informações de conta de armazenamento.  
  
 **CREDENCIAL DO SQL**  
 Especifica o nome da Credencial do SQL que você quer criar.  
  
## <a name="windows-azure-credentials"></a>Credenciais do Windows Azure  
 **Certificado de Gerenciamento**  
 Use essa opção para especificar um certificado do repositório de certificados local que corresponde ao certificado de gerenciamento do Windows Azure. Para obter mais informações sobre o certificado de gerenciamento do Windows Azure, consulte [Criar e carregar um Certificado de Gerenciamento para o Windows Azure](https://go.microsoft.com/fwlink/?LinkId=320781).  
  
 **Assinatura**  
 Selecione, digite ou cole a ID de assinatura do Windows Azure que corresponde ao certificado de gerenciamento do repositório local de certificados.  
  
 **Perfil de Publicação**  
 Use essa opção se você tiver um perfil de publicação baixado no seu computador. Se você usar essa opção, a ID da assinatura e o certificado serão automaticamente populados.  
  
> [!CAUTION]  
>  No momento, o SQL Server oferece suporte à versão do perfil de publicação 2.0. Para baixar a versão com suporte do perfil de publicação, consulte [Download do perfil de publicação 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
  
## <a name="storage-account"></a>Conta de Armazenamento  
 Selecione a conta de armazenamento que você deseja usar para armazenar os arquivos de backup.  
  
  
