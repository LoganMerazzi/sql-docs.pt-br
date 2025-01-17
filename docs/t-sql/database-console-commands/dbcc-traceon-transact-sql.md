---
title: DBCC TRACEON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_TRACEON_TSQL
- TRACEON
- DBCC TRACEON
- TRACEON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC TRACEON statement
- trace flags [SQL Server], enabling
ms.assetid: 93085324-ebaa-4e38-aac8-5e57b4b0d36d
author: pmasl
ms.author: umajay
ms.openlocfilehash: 6e3a4a360f4a317139908b57421e420e8cd68402
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040599"
---
# <a name="dbcc-traceon-transact-sql"></a>DBCC TRACEON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Habilita os sinalizadores de rastreamento especificados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC TRACEON ( trace# [ ,...n ][ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
*trace#*  
É o número do sinalizador de rastreamento a ser ativado.  
  
*n*  
É um espaço reservado que indica que vários sinalizadores de rastreamento podem ser especificados.  
  
-1  
Ativa globalmente os sinalizadores de rastreamento especificados.  
  
WITH NO_INFOMSGS  
Suprime todas as mensagens informativas.  
  
## <a name="remarks"></a>Remarks  
Em um servidor de produção, para evitar comportamento imprevisível, recomendamos que você habilite sinalizadores de rastreamento no servidor usando somente um dos seguintes métodos:
-   Use a opção de inicialização de linha de comando **-T** do Sqlservr.exe. Essa é a prática mais recomendada, porque assegura que todas as instruções sejam executadas com o sinalizador de rastreamento habilitado. Isso inclui comandos em scripts de inicialização. Para obter mais informações, consulte [sqlservr Application](../../tools/sqlservr-application.md).  
-   Use DBCC TRACEON **(** _trace#_ [ **,** ... *.n*] **,-1)** somente enquanto usuários ou aplicativos não estiverem executando instruções simultaneamente no sistema.  

Sinalizadores de rastreamento são usados para personalizar certas características que controlam o modo operacional do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sinalizadores de rastreamento, depois de habilitados, permanecem assim no servidor até que sejam desabilitados executando uma instrução DBCC TRACEOFF. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], há dois tipos de sinalizadores de rastreamento: sessão e global. Os sinalizadores de rastreamento de sessão são ativos para uma conexão e são visíveis apenas para essa conexão. Sinalizadores de rastreamento globais são definidos no nível do servidor e são visíveis em todas as conexões no servidor. Para determinar o status dos sinalizadores de rastreamento, use DBCC TRACESTATUS. Para desabilitar sinalizadores de rastreamento, use DBCC TRACEOFF.
  
Depois de ativar um sinalizador de rastreamento que afeta os planos de consulta, execute `DBCC FREEPROCCACHE;` para que os planos armazenados em cache sejam recompilados usando o novo comportamento que afeta o plano.
  
## <a name="result-sets"></a>Conjuntos de resultados  
 DBCC TRACEON retorna o conjunto de resultados seguinte (mensagem):  
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** .
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir desabilita a compactação de hardware para drivers em fita, ativando sinalizadores de rastreamento `3205`. Esse sinalizador é ativado somente para a conexão atual.
  
```sql  
DBCC TRACEON (3205);  
GO  
```  
  
O exemplo a seguir ativa o sinalizador de rastreamento `3205` globalmente.
  
```sql  
DBCC TRACEON (3205, -1);  
GO  
```  
  
O exemplo a seguir ativa os sinalizadores de rastreamento `3205` e `260` globalmente.
  
```sql  
DBCC TRACEON (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACESTATUS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
[Habilitar o comportamento do otimizador de consulta do SQL Server que afeta o plano e pode ser controlado por diferentes sinalizadores de rastreamento em um nível de consulta específico](https://support.microsoft.com/kb/2801413)
  
  
