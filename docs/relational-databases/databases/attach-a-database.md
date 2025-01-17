---
title: Anexar um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.attachdatabase.f1
helpviewer_keywords:
- database attaching [SQL Server]
- attaching databases [SQL Server]
ms.assetid: b4efb0ae-cfe6-4d81-a4b4-6e4916885caa
author: stevestein
ms.author: sstein
ms.openlocfilehash: ca1ff898841b946c0823b71b065f360a59e69696
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071700"
---
# <a name="attach-a-database"></a>Anexar um banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico descreve como anexar um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você pode usar este recurso para copiar, mover ou atualizar um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   O banco de dados primeiro deve ser desanexado. A tentativa de anexar um banco de dados que não foi desanexado retornará um erro. Para obter mais informações, veja [Desanexar um banco de dados](../../relational-databases/databases/detach-a-database.md).  
  
-   Quando você anexa um banco de dados, todos os arquivos de dados (arquivos MDF e LDF) devem estar disponíveis. Se algum arquivo de dados tiver um caminho diferente de quando o banco de dados foi inicialmente criado ou anexado pela última vez, você deverá especificar o caminho atual do arquivo.  
  
-   Quando você anexar um banco de dados, se os arquivos MDF e LDF estiverem localizados em diretórios diferentes e um dos caminhos incluir \\\\?\GlobalRoot, a operação falhará.  
  
###  <a name="Recommendations"></a> Anexar é a melhor opção?  
Recomendamos que você mova os bancos de dados utilizando o procedimento de realocação planejada `ALTER DATABASE`, em vez de utilizar desanexação e anexação, ao mover arquivos de banco de dados dentro da mesma instância. Para obter mais informações, veja [Mover bancos de dados de usuário](../../relational-databases/databases/move-user-databases.md). 
 
Não recomendamos o uso de ações de desanexar e anexar para Backup e Recuperação. Não há backups de log de transações e é possível excluir arquivos acidentalmente.
  
###  <a name="Security"></a> Segurança  
As permissões de acesso ao arquivo são definidas durante algumas operações de banco de dados, inclusive desanexar ou anexar um banco de dados. Para obter informações sobre permissões de arquivo definidas sempre que um banco de dados é desanexado e anexado, veja [Protegendo dados e arquivos de log](https://technet.microsoft.com/library/ms189128.aspx) nos Manuais Online do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (ainda é uma leitura válida!) 
  
Não é recomendável anexar ou restaurar bancos de dados de origem desconhecida ou não confiável. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados. Para saber mais sobre como anexar bancos de dados e informações sobre alterações que são feitas em metadados ao anexar um banco de dados, veja [Anexar e desanexar bancos de dados(SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
####  <a name="Permissions"></a> Permissões  
Requer permissão `CREATE DATABASE`, `CREATE ANY DATABASE` ou `ALTER ANY DATABASE`.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  

### <a name="to-attach-a-database"></a>Para anexar um banco de dados  
  
1.  No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e clique para expandir a exibição dessa instância no SSMS.  
  
2.  Clique com o botão direito do mouse em **Bancos de dados** e clique em **Anexar**.  
  
3.  Na caixa de diálogo **Anexar Banco de Dados** , para especificar o banco de dados a ser anexado, clique em **Adicionar**. Na caixa de diálogo **Localizar Arquivos de Banco de Dados** , selecione a unidade de disco onde o banco de dados reside e expanda a árvore de diretório para localizar e selecionar o arquivo .mdf do banco de dados, por exemplo:  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\AdventureWorks2012_Data.mdf`  
  
    > [!IMPORTANT]  
    > Trying to select a database that is already attached generates an error.  
  
     **Databases to attach**  
     Displays information about the selected databases.  
  
     \<no column header>  
     Displays an icon indicating the status of the attach operation. The possible icons are described in the **Status** description, below).  
  
     **MDF File Location**  
     Displays the path and file name of the selected MDF file.  
  
     **Database Name**  
     Displays the name of the database.  
  
     **Attach As**  
     Optionally, specifies a different name for the database to attach as.  
  
     **Owner**  
     Provides a drop-down list of possible database owners from which you can optionally select a different owner.  
  
     **Status**  
     Displays the status of the database according to the following table.  
  
    |Ícone|Texto de status|Descrição|  
    |----------|-----------------|-----------------|  
    |(No icon)|(Nenhum texto)|A operação de anexação não foi iniciada ou pode estar pendente para esse objeto. Esse é o padrão quando a caixa de diálogo é aberta.|  
    |Triângulo verde apontando para a direita|Em andamento|A operação de anexação foi iniciada mas não está completa.|  
    |Sinal de verificação verde|Êxito|O objeto foi anexado com êxito.|  
    |Círculo vermelho contendo uma cruz branca|Erro|A operação de anexação encontrou um erro e não foi concluída com êxito.|  
    |Círculo que contém dois quadrantes pretos (à esquerda e à direita) e dois quadrantes brancos (em cima e em baixo)|Stopped (parado)|A operação de anexação não foi completada com êxito porque o usuário interrompeu a operação.|  
    |Círculo que contém uma seta curvada que aponta para o sentido anti-horário|Revertida|A operação de anexação teve êxito, mas foi revertida devido a um erro ao se anexar outro objeto.|  
  
     **Message**  
     Displays either a blank message or a "File not found" hyperlink.  
  
     **Add**  
     Find the necessary main database files. When the user selects an .mdf file, applicable information is automatically filled in the respective fields of the **Databases to attach** grid.  
  
     **Remove**  
     Removes the selected file from the **Databases to attach** grid.  
  
     **"** *<database_name>* **" database details**  
     Displays the names of the files to be attached. To verify or change the pathname of a file, click the **Browse** button (**...**).  
  
    > [!NOTE]  
    > If a file does not exist, the **Message** column displays "Not found." If a log file is not found, it exists in another directory or has been deleted. You need to either update the file path in the **database details** grid to point to the correct location or remove the log file from the grid. If an .ndf data file is not found, you need to update its path in the grid to point to the correct location.  
  
     **Original File Name**  
     Displays the name of the attached file belonging to the database.  
  
     **File Type**  
     Indicates the type of file, **Data** or **Log**.  
  
     **Current File Path**  
     Displays the path to the selected database file. The path can be edited manually.  
  
     **Message**  
     Displays either a blank message or a "**File not found**" hyperlink.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
### <a name="to-attach-a-database"></a>Para anexar um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Use a instrução [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) com a cláusula `FOR ATTACH`.  
  
     Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo anexa os arquivos do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] e renomeia o banco de dados como `MyAdventureWorks`.  
  
    ```sql  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),   
        (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')   
        FOR ATTACH;  
    ```  
  
    > [!NOTE]  
    > Se desejar, você poderá usar o procedimento armazenado [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) ou [sp_attach_single_file_db](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md) . No entanto, esses procedimentos armazenados estendidos são removidos de uma versão futura do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez dessa função, recomendamos usar `CREATE DATABASE ... FOR ATTACH` .  
  
##  <a name="FollowUp"></a> Acompanhamento: Depois de atualizar um banco de dados do SQL Server  
Após a atualização de um banco de dados usando o método anexar, o banco de dados se torna logo disponível e é atualizado automaticamente. Se o banco de dados tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices dependendo da configuração da propriedade de servidor **Opção de Atualização de Texto Completo** . Se a opção de atualização for definida como **Importar** ou **Recriar**, os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida como **Importar**, se não houver um catálogo de texto completo disponível, os índices de texto completo associados serão recompilados.  
  
Se o nível de compatibilidade de um banco de dados de usuário for 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade for 90 ou inferior antes da atualização, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]
> Se você estiver conectando um banco de dados de uma instância que está executando o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou anterior com a CDA (captura de dados de alterações) habilitada, você também precisará executar o comando abaixo para atualizar os metadados da CDA (captura de dados de alterações).
  
```sql
USE <database name>
EXEC sys.sp_cdc_vupgrade  
``` 
 
## <a name="see-also"></a>Consulte Também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) 
 <br>[Gerenciar metadados ao disponibilizar um banco de dados em outro servidor](manage-metadata-when-making-a-database-available-on-another-server.md)  
 [Desanexar um banco de dados](../../relational-databases/databases/detach-a-database.md)  
  
  
