---
title: ASSEMBLYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASSEMBLYPROPERTY_TSQL
- ASSEMBLYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASSEMBLYPROPERTY statement
- assemblies [CLR integration], properties
ms.assetid: cf03d1b1-724c-48bf-a8df-3fe2586b150a
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9556834a173302e19358f5333b059d7b4f902519
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Retorna informações sobre uma propriedade de um assembly.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
## <a name="arguments"></a>Argumentos  
*nome_do_assembly*  
É o nome do assembly.
  
*Property_Name*  
É o nome de uma propriedade sobre a qual recuperar informações. *Property_Name* pode ser um dos valores a seguir.
  
|Valor|Description|  
|---|---|
|**CultureInfo**|Localidade do assembly.|  
|**PublicKey**|Chave pública ou token de chave pública do assembly.|  
|**MvID**|Número de identificação de versão completo do assembly gerado por compilador.|  
|**VersionMajor**|Componente principal (primeira parte) do número de identificação de versão de quatro partes do assembly.|  
|**VersionMinor**|Componente secundário (segunda parte) do número de identificação de versão de quatro partes do assembly.|  
|**VersionBuild**|Componente de compilação (terceira parte) do número de identificação de versão de quatro partes do assembly.|  
|**VersionRevision**|Componente de revisão (quarta parte) do número de identificação de versão de quatro partes do assembly.|  
|**SimpleName**|É o nome simples do assembly.|  
|**Arquitetura**|Arquitetura de processador do assembly.|  
|**CLRName**|Cadeia de caracteres canônica que codifica o nome simples, o número de versão, a cultura, a chave pública e a arquitetura do assembly. Esse valor identifica exclusivamente o assembly no lado CLR (Common Language Runtime).|  
  
## <a name="return-type"></a>Tipo de retorno
**sql_variant**
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir presume que um assembly de `HelloWorld` esteja registrado no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Para obter mais informações, consulte [exemplo Hello World](http://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7).
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ASSEMBLYPROPERTY ('HelloWorld' , 'PublicKey');  
```  
  
## <a name="see-also"></a>Consulte também
[CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
[DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)
  
  
