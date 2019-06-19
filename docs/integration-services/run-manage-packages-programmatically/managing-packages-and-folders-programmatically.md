---
title: Gerenciar pacotes e pastas programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f38f79f90a1ec39a013efc4efd03a13f96e51a72
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65719118"
---
# <a name="managing-packages-and-folders-programmatically"></a>Gerenciando pacotes e pastas programaticamente

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


<a name="top"></a> Ao trabalhar de forma programática com pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], convém determinar se um pacote ou pasta individual existe ou então gerenciar as pastas em que os pacotes estão armazenados. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece diversos métodos para atender a esses requisitos.    
    
##  <a name="exists"></a> Determinando se existe um pacote ou pasta    
 Para determinar programaticamente se existe um pacote salvo, chame um dos métodos a seguir antes de tentar carregar e executar o pacote:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|    
    
 Para determinar programaticamente se existe uma pasta, chame um dos métodos a seguir antes de tentar listar os pacotes armazenados na pasta:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|    
    
 [Voltar ao Início](#top)    
    
##  <a name="managing"></a> Gerenciar pacotes e pastas    
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece métodos adicionais para gerenciar pacotes e as pastas nas quais eles são armazenados.    
    
###  <a name="managing_rempkg"></a> Remover um pacote    
 Para remover um pacote salvo programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [Voltar ao Início](#top)    
    
###  <a name="managing_create"></a> Criar uma pasta    
 Para criar uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [Voltar ao Início](#top)    
    
###  <a name="managing_remfldr"></a> Remover uma pasta    
 Para remover uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [Voltar ao Início](#top)    
    
###  <a name="managing_rename"></a> Renomear uma pasta    
 Para renomear uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [Voltar ao Início](#top)    
    
## <a name="see-also"></a>Consulte Também    
 [Gerenciamento de Pacotes &#40;Serviço SSIS&#41;](../../integration-services/service/package-management-ssis-service.md)     
 [Enumerar pacotes disponíveis programaticamente](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  
