---
title: SqlLocalDB Utility | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- SqlLocalDB utility [SQL Server]
- local database runtime utility
- LocalDB, SqlLocalDB Utility
ms.assetid: d785cdb7-1ea0-4871-bde9-1ae7881190f5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f13a16e7c8f507914abe8529e02b76161072c5bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035395"
---
# <a name="sqllocaldb-utility"></a>Utilitário SqlLocalDB
  Use o `SqlLocalDB` utilitário para criar uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../includes/ssexpcurrent-md.md)] **LocalDB**. O `SqlLocalDB` utilitário (SqlLocalDB.exe) é uma ferramenta de linha de comando simples para permitir que os usuários e desenvolvedores criar e gerenciar uma instância do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB**. Para obter informações sobre como usar **LocalDB**, consulte [SQL Server 2014 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SqlLocalDB.exe   
{  
      [ create   | c ] <instance-name><instance-version> [-s ]  
    | [ delete   | d ] <instance-name>  
    | [ start    | s ] <instance-name>  
    | [ stop     | p ] <instance-name>  [ -i ] [ -k ]  
    | [ share    | h ] ["<user_SID>" | "<user_account>" ] "<private-name>""<shared-name>"  
    | [ unshare  | u ] "<shared-name>"  
    | [ info     | i ] <instance-name>  
    | [ versions | v ]  
    | [ trace    | t ] [ on | off ]  
    | [ help     | -? ]  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **create** | **c** ] *\<instance-name>* *\<instance-version>* [ **-s** ]  
 Cria uma nova instância do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. `SqlLocalDB` usa a versão do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] binários especificados pela  *\<versão da instância >* argumento. O número da versão é especificado em formato numérico com pelo menos um decimal. Os números de versões secundárias (pacotes de serviço) são opcionais. Por exemplo, os seguintes dois números de versão são aceitáveis: 11.0 ou 11.0.1186. A versão especificada deve ser estalada no computador. Se não especificado, o número de versão padrão para a versão do `SqlLocalDB` utilitário. Adicionando **-s** inicia a nova instância de **LocalDB**.  
  
 [ **share** | **h** ]  
 Compartilha a instância privada especificada do **LocalDB** que usa o nome compartilhado especificado. Se a SID ou o nome de conta do usuário for omitido, o valor padrão será o usuário atual.  
  
 [ **unshared** | **u** ]  
 Interrompe o compartilhamento da instância especificada compartilhada do **LocalDB**.  
  
 [ **delete** | **d** ] *\<instance-name>*  
 Exclui a instância especificada do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**.  
  
 [ **start** | **s** ] " *\<instance-name>* "  
 Inicia a instância especificada do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. Quando tem êxito, a instrução retorna o endereço de pipe nomeado do **LocalDB**.  
  
 [ **stop** | **p** ] *\<instance-name>* [ **-i** ] [ **-k** ]  
 Interrompe a instância especificada do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**. Adicionando **-i** solicita o desligamento da instância com o `NOWAIT` opção. Adicionando **-k** elimina o processo da instância sem contatá-lo.  
  
 [ **info** | **i** ] [ *\<instance-name>* ]  
 Lista todas as instâncias do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** de propriedade do usuário atual.  
  
 *\<instance-name>* retorna o nome, a versão, o estado (Executando ou Parado), a hora da última inicialização da instância especificada do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** e o nome do pipe local do **LocalDB**.  
  
 [ **trace** | **t** ] **on** | **off**  
 **rastreamento na** habilita rastreamento para o `SqlLocalDB` chamadas à API para o usuário atual. **trace off** desabilita o rastreamento.  
  
 **-?**  
 Retorna descrições breves de cada `SqlLocalDB` opção.  
  
## <a name="remarks"></a>Comentários  
 O argumento *instance name* deve seguir as regras de identificadores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou deve ser colocado entre aspas duplas.  
  
 A execução de SqlLocalDB sem argumentos retorna o texto da ajuda.  
  
 Operações diferentes de iniciar podem ser executados apenas em uma instância que pertence ao usuário conectado no momento.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-an-instance-of-localdb"></a>A. Criando uma instância do LocalDB  
 O exemplo a seguir cria uma instância do [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** denominada `DEPARTMENT` que usa os binários do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e inicia a instância.  
  
```  
SqlLocalDB.exe create "DEPARTMENT" 12.0 -s  
```  
  
### <a name="b-working-with-a-shared-instance-of-localdb"></a>B. Trabalhando com uma instância compartilhada do LocalDB  
 Abrir um prompt de comando usando privilégios de administrador.  
  
```  
SqlLocalDB.exe create "DeptLocalDB"  
SqlLocalDB.exe share "DeptLocalDB" "DeptSharedLocalDB"  
SqlLocalDB.exe start "DeptLocalDB"  
SqlLocalDB.exe info "DeptLocalDB"  
REM The previous statement outputs the Instance pipe name for the next step  
sqlcmd -S np:\\.\pipe\LOCALDB#<use your pipe name>\tsql\query  
CREATE LOGIN NewLogin WITH PASSWORD = 'Passw0rd!!@52';   
GO  
CREATE USER NewLogin;  
GO  
EXIT  
```  
  
 Execute o código a seguir para conectar-se à instância compartilhada do **LocalDB** usando o logon `NewLogin` .  
  
```  
sqlcmd -S (localdb)\.\DeptSharedLocalDB -U NewLogin -P Passw0rd!!@52  
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server 2014 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
  
