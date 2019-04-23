---
title: Serialização de XML de objetos de banco de dados CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- serialization
- XML serialization [CLR integration]
- common language runtime [SQL Server], XML serialization
- XmlSerializer class
ms.assetid: ac84339b-9384-4710-bebc-01607864a344
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 646d15dc3091323e6e7db2af757640122fb2f0fd
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158472"
---
# <a name="xml-serialization-from-clr-database-objects"></a>Serialização XML de objetos de banco de dados CLR
  A serialização XML é necessária em dois cenários:  
  
-   Invocação de serviços da Web de objetos CLR (Common Language Runtime).  
  
-   Conversão de um UDT (tipo definido pelo usuário) em XML.  
  
 A execução de serialização XML invocando a classe `XmlSerializer` normalmente gera um assembly de serialização adicional que é sobrecarregado no projeto com o assembly de origem. Entretanto, por questões de segurança, essa sobrecarga é desabilitada no CLR. Portanto, para chamar um serviço web ou realizar a conversão de UDT em XML dentro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o assembly deve ser criado manualmente usando uma ferramenta chamada **Sgen.exe** fornecido com o .NET Framework que gera o necessário assemblies de serialização. Ao invocar `XmlSerializer`, o assembly de serialização precisa ser criado manualmente seguindo estas etapas:  
  
1.  Execute o **Sgen.exe** ferramenta que é fornecida com o SDK do .NET Framework para criar o assembly que contém os serializadores XML para o assembly de origem.  
  
2.  Registre o assembly gerado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução `CREATE ASSEMBLY`.  
  
 Para obter informações sobre erros que você pode receber ao executar a serialização XML, consulte o artigo Microsoft Support a seguir: ["Não é possível carregar o assembly de serialização gerado dinamicamente"](https://support.microsoft.com/kb/913668).  
  
 Para obter informações sobre tipos de dados não suportados pelo XMLSerializer, consulte o suporte a associação de esquemas XML na documentação do .NET Framework.  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a dados de objetos de banco de dados CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
  
