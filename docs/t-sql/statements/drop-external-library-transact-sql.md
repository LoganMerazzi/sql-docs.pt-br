---
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2702be0133925e8c7069c8abb11e82c8c4773743
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583329"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Exclui uma biblioteca de pacote existente. As bibliotecas de pacotes são usadas por tempos de execução externos com suporte, tais como do R, Python ou Java.

> [!NOTE]
> No SQL Server 2017, há compatibilidade apenas com a linguagem R e a plataforma Windows. Há suporte para R, Python e Java nas plataformas Windows e Linux no SQL Server 2019 CTP 2.4. 

## <a name="syntax"></a>Sintaxe

```sql
DROP EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ];
```

### <a name="arguments"></a>Argumentos

**library_name**

Especifica o nome de uma biblioteca de pacotes existente.

As bibliotecas estão no escopo do usuário. Os nomes de bibliotecas devem ser exclusivos no contexto de um usuário ou proprietário específico.

**owner_name**

Especifica o nome do usuário ou da função que é a proprietária da biblioteca externa.

Os proprietários de banco de dados podem excluir bibliotecas criadas por outros usuários.

## <a name="permissions"></a>Permissões

Para excluir uma biblioteca, é necessário ter o privilégio ALTER ANY EXTERNAL LIBRARY. Por padrão, todos os proprietários de bancos de dados ou do objeto também podem excluir uma biblioteca externa.

### <a name="return-values"></a>Valores retornados

Uma mensagem informativa é retornada se a instrução foi bem-sucedida.

## <a name="remarks"></a>Remarks

Ao contrário de outras instruções `DROP` no SQL Server, essa instrução dá suporte à especificação de uma cláusula de autorização opcional. Isso permite que o **dbo** ou os usuários na função **db_owner** removam uma biblioteca de pacote carregada por um usuário normal no banco de dados.

## <a name="examples"></a>Exemplos

Adicione o pacote do R personalizado, chamado `customPackage`, a um banco de dados:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM (CONTENT = 'C:\temp\customPackage_v1.1.zip')
WITH (LANGUAGE = 'R');
GO
```

Exclua a biblioteca `customPackage`.

```sql
DROP EXTERNAL LIBRARY customPackage;
```

## <a name="see-also"></a>Confira também

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

