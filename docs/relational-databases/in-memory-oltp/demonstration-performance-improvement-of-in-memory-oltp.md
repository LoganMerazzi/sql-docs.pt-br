---
title: 'Demonstração: melhoria do desempenho do OLTP in-memory | Microsoft Docs'
ms.custom: ''
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7cec13fc9bcfe30aa34f46afb23c7f8755f0c477
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069641"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>Demonstração: aprimoramento do desempenho do OLTP na memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  O exemplo de código neste tópico mostra o desempenho rápido de tabelas com otimização de memória. A melhoria de desempenho é evidente quando os dados em uma tabela com otimização de memória são acessados de [!INCLUDE[tsql](../../includes/tsql-md.md)]tradicional, interpretado. Essa melhoria do desempenho é ainda maior quando os dados em uma tabela com otimização de memória são acessados de um NCSProc (procedimento armazenado compilado nativamente).  
 
Para ver uma demonstração mais abrangente de possíveis aprimoramentos de desempenho do OLTP in-memory, consulte [Demonstração do desempenho do OLTP in-memory v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0). 
  
 O exemplo de código neste artigo é de thread único e não aproveita os benefícios de simultaneidade do OLTP in-memory. Uma carga de trabalho que usa a simultaneidade apresentará um maior ganho de desempenho. O exemplo de código mostra apenas um aspecto da melhoria de desempenho, ou seja, a eficiência do acesso a dados para INSERT.  
  
 A melhoria de desempenho oferecida por tabelas com otimização de memória é feita completamente quando os dados em uma tabela com otimização de memória são acessados de um NCSProc.  
  
## <a name="code-example"></a>Exemplo de código  
 As subseções a seguir descrevem cada etapa.  
  
### <a name="step-1a-prerequisite-if-using-includessnoversionincludesssnoversion-mdmd"></a>Etapa 1a: pré-requisito se estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 As etapas nesta primeira subseção aplicam-se apenas se você estiver executando no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e não se aplicam se você estiver executando no [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Faça o seguinte:  
  
1.  Use o SQL Server Management Studio (SSMS.exe) para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Qualquer outra ferramenta semelhante a SSMS.exe é aceitável.  
  
2.  Crie manualmente um diretório chamado **C:\data\\** . O código Transact-SQL de exemplo espera que o diretório já exista.  
  
3.  Execute o T-SQL curto para criar o banco de dados e seu grupo de arquivos com otimização de memória.  
  
```sql  
go  
CREATE DATABASE imoltp;    --  Transact-SQL  
go  
  
ALTER DATABASE imoltp ADD FILEGROUP [imoltp_mod]  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
ALTER DATABASE imoltp ADD FILE  
    (name = [imoltp_dir], filename= 'c:\data\imoltp_dir')  
    TO FILEGROUP imoltp_mod;  
go  
  
USE imoltp;  
go  
```  
  
### <a name="step-1b-prerequisite-if-using-includesssdsfullincludessssdsfull-mdmd"></a>Etapa 1b: pré-requisito se estiver usando [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
 Esta subseção aplica-se apenas se você estiver usando o [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Faça o seguinte:  
  
1.  Decida qual banco de dados de teste existente será usado para o exemplo de código.  
  
2.  Se você optar por criar um novo banco de dados de teste, use o [portal do Azure](https://portal.azure.com) para criar um banco de dados denominado **imoltp**.  
  
 Se você quiser instruções sobre como usar o portal do Azure para isso, veja [Introdução ao Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-get-started).  
  
### <a name="step-2-create-memory-optimized-tables-and-ncsproc"></a>Etapa 2: criar tabelas com otimização de memória e NCSProc  
 Essa etapa cria tabelas com otimização de memória e um NCSProc (procedimento armazenado compilado nativamente). Faça o seguinte:  
  
1.  Use SSMS.exe para conectar-se ao novo banco de dados.  
  
2.  Execute o comando T-SQL a seguir no banco de dados.  
  
```sql  
go  
DROP PROCEDURE IF EXISTS ncsp;  
DROP TABLE IF EXISTS sql;  
DROP TABLE IF EXISTS hash_i;  
DROP TABLE IF EXISTS hash_c;  
go  
  
CREATE TABLE [dbo].[sql] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
);  
go  
  
CREATE TABLE [dbo].[hash_i] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE TABLE [dbo].[hash_c] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE PROCEDURE ncsp  
    @rowcount INT,  
    @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[hash_c] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
END;  
go  
```  
  
### <a name="step-3-run-the-code"></a>Etapa 3: executar o código  
 Agora você pode executar as consultas que demonstrarão o desempenho de tabelas com otimização de memória. Faça o seguinte:  
  
1.  Use o SSMS.exe para executar o comando T-SQL a seguir no banco de dados.  
  
     Ignore qualquer velocidade ou outros dados de desempenho gerados por essa primeira execução. A primeira execução assegura que várias operações exclusivamente avulsas sejam executadas, como alocações iniciais de memória.  
  
2.  Novamente, use o SSMS.exe para executar novamente o comando T-SQL a seguir no banco de dados.  
  
```sql  
go  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Inserts, one at a time.  
  
DECLARE @starttime DATETIME2 = sysdatetime();  
DECLARE @timems INT;  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
  
-- Harddrive-based table and interpreted Transact-SQL.  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[sql] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'A: Disk-based table and interpreted Transact-SQL: '  
    + cast(@timems AS VARCHAR(10)) + ' ms';  
  
-- Interop Hash.  
  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
    BEGIN;  
      INSERT INTO [dbo].[hash_i] VALUES (@i, @c);  
      SET @i += 1;  
    END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'B: memory-optimized table with hash index and interpreted Transact-SQL: '  
    + cast(@timems as VARCHAR(10)) + ' ms';  
  
-- Compiled Hash.  
  
SET @starttime = sysdatetime();  
  
EXECUTE ncsp @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'C: memory-optimized table with hash index and native SP:'  
    + cast(@timems as varchar(10)) + ' ms';  
go  
  
DELETE sql;  
DELETE hash_i;  
DELETE hash_c;  
go  
```  
  
 A seguir estão as estatísticas de tempo de saída geradas por nossa segunda execução de teste.  
  
```sql  
10453 ms , A: Disk-based table and interpreted Transact-SQL.  
5626 ms , B: memory-optimized table with hash index and interpreted Transact-SQL.  
3937 ms , C: memory-optimized table with hash index and native SP.  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
