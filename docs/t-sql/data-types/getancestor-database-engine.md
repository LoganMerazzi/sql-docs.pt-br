---
title: GetAncestor (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetAncestor_TSQL
- GetAncestor
dev_langs:
- TSQL
helpviewer_keywords:
- GetAncestor [Database Engine]
ms.assetid: b96a986f-d5e4-4034-8013-de7974594ee9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f13f076309cfc1b78ab5b76676cbf7ec3eb82f87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077981"
---
# <a name="getancestor-database-engine"></a>GetAncestor (Mecanismo do Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna uma **hierarchyid** que representa o *n*º ancestral de *this*.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Transact-SQL syntax  
child.GetAncestor ( n )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetAncestor ( int n )  
```  
  
## <a name="arguments"></a>Argumentos  
*n*  
Um **int**, que representa o número de níveis para elevar na hierarquia.
  
## <a name="return-types"></a>Tipos de retorno
**Tipo de retorno do SQL Server: hierarchyid**
  
**Tipo de retorno do CLR: SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
Usado para testar se cada nó da saída possui o nó atual como um ancestral no nível específico.
  
Se um número maior que [GetLevel()](../../t-sql/data-types/getlevel-database-engine.md) for passado, NULL será retornado.
  
Se um número negativo for passado, ocorrerá uma exceção.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-finding-the-child-nodes-of-a-parent"></a>A. Localizando os nós filho de um pai  
`GetAncestor(1)` retorna os funcionários que têm `david0` como o ancestral imediato (seu pai). O exemplo a seguir usa `GetAncestor(1)`.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(1) = @CurrentEmployee ;  
```  
  
### <a name="b-returning-the-grandchildren-of-a-parent"></a>B. Retornando os netos de um pai  
`GetAncestor(2)` retorna os funcionários que estão dois níveis abaixo na hierarquia a partir do nó atual. Estes funcionários são os netos do nó atual. O exemplo a seguir usa `GetAncestor(2)`.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\ken0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(2) = @CurrentEmployee ;  
```  
  
### <a name="c-returning-the-current-row"></a>C. Retornando a linha atual  
Para retornar o nó atual usando `GetAncestor(0)`, execute o código a seguir.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(0) = @CurrentEmployee ;  
```  
  
### <a name="d-returning-a-hierarchy-level-if-a-table-isnt-present"></a>D. Retornando um nível de hierarquia se uma tabela não existir  
`GetAncestor` retornará o nível selecionado na hierarquia mesmo uma tabela não esteja presente. Por exemplo, o código a seguir especifica um funcionário atual e retorna a `hierarchyid` do ancestral do funcionário atual sem fazer referência a uma tabela.
  
```sql
DECLARE @CurrentEmployee hierarchyid ;  
DECLARE @TargetEmployee hierarchyid ;  
SELECT @CurrentEmployee = '/2/3/1.2/5/3/' ;  
SELECT @TargetEmployee = @CurrentEmployee.GetAncestor(2) ;  
SELECT @TargetEmployee.ToString(), @TargetEmployee ;  
```  
  
### <a name="e-calling-a-common-language-runtime-method"></a>E. Chamando um método de tempo de execução de linguagem comum  
O snippet de código a seguir chama o método `GetAncestor()`.
  
```sql
this.GetAncestor(1)  
```  
  
## <a name="see-also"></a>Confira também
[IsDescendantOf &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/isdescendantof-database-engine.md)  
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  