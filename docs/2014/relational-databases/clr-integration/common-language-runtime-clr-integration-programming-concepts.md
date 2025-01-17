---
title: Conceitos de programação de integração do Common Language Runtime (CLR) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ffd706cdb17bd73281ee4a62842362b09c6311ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922550"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>Conceitos de programação da Integração CLR (Common Language Runtime)
  A partir do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] apresenta a integração do componente CLR do .NET Framework para o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Isso significa que você pode agora gravar procedimentos armazenados, gatilhos, tipos definidos pelo usuário, funções definidas pelo usuário, agregações definidas pelo usuário e funções de streaming com valor de tabela, usando qualquer linguagem do .NET Framework, incluindo o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET e o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#.  
  
 O namespace Microsoft.SqlServer.Server inclui a funcionalidade principal para programação de CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Porém, o namespace Microsoft.SqlServer.Server é documentado no .NET Framework SDK. Esta documentação não é incluída em Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Por padrão, o .NET Framework é instalado com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], mas não o .NET Framework SDK. Sem o SDK instalado no computador e incluído na coleção de Manuais Online, os links para o conteúdo do SDK desta seção não funciona. Instale o .NET Framework SDK. Uma vez instalado, adicione o SDK à coleta de Manuais Online e ao sumário seguindo as instruções em [instalar o SDK do .NET Framework](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx).  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Common Language Runtime &#40;CLR&#41; visão geral da integração](common-language-runtime-integration-overview.md)  
 Fornece uma visão geral breve do CLR e descreve como e por que essa tecnologia foi usada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Descreve os benefícios de usar o CLR para criar objetos de banco de dados.  
  
 [Assemblies &#40;Mecanismo de Banco de Dados&#41;](assemblies-database-engine.md)  
 Descreve como os assemblies são usados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para implantar funções, procedimentos armazenados, gatilhos e agregações e tipos definidos pelo usuário, escritos em uma das linguagens de código gerenciado hospedadas pelo CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework, e não escritos no [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 [Criando objetos de banco de dados com o Common Language Runtime &#40;CLR&#41; integração](database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 Descreve os tipos de objetos que podem ser compilados usando o CLR e examina os requisitos para compilar objetos de banco de dados de CLR.  
  
 [Acesso aos dados dos objetos de banco de dados CLR](data-access/data-access-from-clr-database-objects.md)  
 Descreve como uma rotina de CLR pode acessar dados armazenados em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Segurança da integração CLR](security/clr-integration-security.md)  
 Descreve o modelo de segurança da integração CLR.  
  
 [Depurando objetos de banco de dados CLR](debugging-clr-database-objects.md)  
 Descreve limitações e requisitos para depurar objetos de banco de dados de CLR.  
  
 [Implantando objetos de banco de dados CLR](deploying-clr-database-objects.md)  
 Descreve a implantação de assemblies para servidores de produção.  
  
 [Gerenciamento de assemblies de integração CLR](assemblies/managing-clr-integration-assemblies.md)  
 Descreve como criar e descartar assemblies de integração CLR.  
  
 [Monitorando e solucionando problemas de objetos de banco de dados gerenciado](monitoring-and-troubleshooting-managed-database-objects.md)  
 Fornece informações sobre as ferramentas que podem ser usadas para monitorar e solucionar problemas em objetos de bancos de dados gerenciados e assemblies que são executados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Cenários de uso e exemplos para a integração do CLR &#40;Common Language Runtime&#41;](../../database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
 Descreve casos de uso e exemplos de códigos que usam objetos CLR.  
  
## <a name="see-also"></a>Consulte também  
 [Assemblies &#40;mecanismo de banco de dados&#41;](assemblies-database-engine.md)   
 [Instalar o SDK do .NET Framework](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
