---
ms.openlocfilehash: 327fd6bac9bc1036a0dd07f7b955ee92cb7e40c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223539"
---
  A partir do SQL Server 2005, o comportamento de esquemas mudou. Como resultado, o código que pressupõe que esquemas sejam equivalentes a usuários de banco de dados pode não retornar mais resultados corretos. Exibições antigas do catálogo, incluindo sysobjects, não devem ser usadas em um banco de dados no qual uma das instruções DDL a seguir já tenha sido utilizada: CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION. Nesses bancos de dados você deve usar as exibições do catálogo novas. As exibições do catálogo novas levam em conta a separação de entidades e esquemas apresentada no SQL Server 2005. Para mais informações sobre exibições do catálogo, consulte [Exibições do catálogo &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md).
   