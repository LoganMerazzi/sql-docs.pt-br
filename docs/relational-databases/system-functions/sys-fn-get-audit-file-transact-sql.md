---
title: sys.fn_get_audit_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_audit_file_TSQL
- sys.fn_get_audit_file_TSQL
- fn_get_audit_file
- sys.fn_get_audit_file
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_get_audit_file function
- fn_get_audit_file function
ms.assetid: d6a78d14-bb1f-4987-b7b6-579ddd4167f5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 350b1eca94f8041a0a38105c650e1c0ec7e1f617
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046278"
---
# <a name="sysfngetauditfile-transact-sql"></a>sys.fn_get_audit_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações de um arquivo de auditoria criado por uma auditoria de servidor no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
fn_get_audit_file ( file_pattern,   
    { default | initial_file_name | NULL },   
    { default | audit_record_offset | NULL } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_pattern*  
 Especifica o diretório ou caminho e o nome de arquivo do conjunto de arquivos de auditoria que será lido. É do tipo **nvarchar (260)** . 
 
 - **SQL Server**:
    
    Esse argumento deve incluir um caminho (letra de unidade ou compartilhamento de rede) e um nome de arquivo, podendo conter um caractere curinga. Um único asterisco (*) pode ser usado para coletar vários arquivos de um conjunto de arquivos de auditoria. Por exemplo:  
  
    -   **\<caminho >\\ \***  - coletar todos os arquivos de auditoria no local especificado.  
  
    -   **\<caminho > \LoginsAudit_{GUID}** - coletar todos os arquivos que têm o nome especificado e o par GUID de auditoria.  
  
    -   **\<caminho > \LoginsAudit_{GUID}_00_29384.sqlaudit** -coletar um arquivo de auditoria específicas.  
  
 - **Banco de dados SQL do Azure**:
 
    Esse argumento é usado para especificar uma URL de blob (incluindo o ponto de extremidade de armazenamento e o contêiner). Embora ele não oferece suporte a um caractere curinga, você pode usar um prefixo de nome de arquivo parcial (blob) (em vez do nome de blob completo) para coletar vários arquivos (blobs) que começam com esse prefixo. Por exemplo:
 
      - **\<Storage_endpoint\>/\<contêiner\>/\<ServerName\>/\<DatabaseName\> /**  -coleta todos os arquivos de auditoria (blobs) do banco de dados específico.    
      
      - **\<Storage_endpoint\>/\<contêiner\>/\<ServerName\>/\<DatabaseName\> / \< AuditName\>/\<CreationDate\>/\<FileName\>. xel** -coleta um arquivo de auditoria específicos (blob).
  
> [!NOTE]  
>  Indicar um caminho sem um padrão de nome de arquivo irá gerar um erro.  
  
 *initial_file_name*  
 Especifica o caminho e o nome de um arquivo especificado no conjunto de arquivos de auditoria a partir do qual iniciar a leitura dos registros de auditoria. É do tipo **nvarchar (260)** .  
  
> [!NOTE]  
>  O *initial_file_name* argumento deve conter entradas válidas ou deve conter um padrão | Valor nulo.  
  
 *audit_record_offset*  
 Especifica um local conhecido com o arquivo especificado para o initial_file_name. Quando esse argumento for usado, a função começará a leitura a partir do primeiro registro do buffer imediatamente após o deslocamento especificado.  
  
> [!NOTE]  
>  O *audit_record_offset* argumento deve conter entradas válidas ou deve conter um padrão | Valor nulo. É do tipo **bigint**.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 A tabela a seguir descreve o conteúdo do arquivo de auditoria que pode ser retornado por essa função.  
  
| Nome da coluna | type | Descrição |  
|-------------|------|-------------|  
| action_id | **varchar(4)** | A identificação da ação. Não permite valor nulo. |  
| additional_information | **nvarchar(4000)** | Informações exclusivas que se aplicam somente a um evento são retornadas como XML. Um número pequeno de ações auditável contém esse tipo de informação.<br /><br /> Um nível de pilha TSQL será exibido em formato XML para ações que tenham pilha TSQL associada a elas. O formato XML será:<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> O nest_level do quadro indica o nível de aninhamento atual do quadro. O nome do Módulo é representado em formato de três partes (database_name, schema_name e object_name).  O nome do módulo será analisado para escape de caracteres de xml inválido, como `'\<'`, `'>'`, `'/'`, `'_x'`. Eles serão de saída como `_xHHHH\_`. O HHHH representa o código UCS-2 hexadecimal de quatro dígitos do caractere<br /><br /> Permite valor nulo. Retornará NULL quando o evento não reportar informações adicionais. |
| affected_rows | **bigint** | **Aplica-se ao**: Somente a banco de dados SQL do Azure<br /><br /> Número de linhas afetadas pela instrução executada. |  
| application_name | **nvarchar(128)** | **Aplica-se ao**: Azure SQL DB + SQL Server (começando com o 2017)<br /><br /> Nome do aplicativo cliente que executou a instrução que causou o evento de auditoria |  
| audit_file_offset | **bigint** | **Aplies para**: Apenas o SQL Server<br /><br /> O deslocamento de buffer no arquivo que contém o registro de auditoria. Não permite valor nulo. |  
| audit_schema_version | **int** | Sempre 1 |  
| class_type | **varchar(2)** | O tipo de entidade auditável no qual a auditoria ocorre. Não permite valor nulo. |  
| client_ip | **nvarchar(128)** | **Aplica-se ao**: Azure SQL DB + SQL Server (começando com o 2017)<br /><br />    IP do aplicativo cliente de origem |  
| connection_id | GUID | **Aplica-se ao**: Instância de banco de dados SQL e gerenciado do Azure<br /><br /> ID da conexão no servidor |
| data_sensitivity_information | nvarchar(4000) | **Aplica-se ao**: Somente a banco de dados SQL do Azure<br /><br /> Tipos de informações e rótulos de confidencialidade retornados pela consulta auditada, com base nas colunas confidenciais no banco de dados. Saiba mais sobre [banco de dados do SQL Azure descobrir dados e classificação](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification) |
| database_name | **sysname** | O contexto do banco de dados no qual a ação aconteceu. Permite valor nulo. Retorna NULL para auditorias que ocorrem no nível do servidor. |  
| database_principal_id | **int** |ID do contexto do usuário de banco de dados no qual a ação é executada. Não permite valor nulo. Retornará 0 se isso não se aplicar. Por exemplo, uma operação de servidor.|
| database_principal_name | **sysname** | Usuário atual. Permite valor nulo. Retorna NULL se não disponível. |  
| duration_milliseconds | **bigint** | **Aplica-se ao**: Instância de banco de dados SQL e gerenciado do Azure<br /><br /> Duração da execução de consulta em milissegundos |
| event_time | **datetime2** | Data e hora em que a ação auditável é acionada. Não permite valor nulo. |  
| file_name | **varchar(260)** | O caminho e nome do arquivo de log de auditoria que deu origem ao registro. Não permite valor nulo. |
| is_column_permission | **bit** | Sinalizador que indica se esta é uma permissão no nível de coluna. Não permite valor nulo. Retorna 0 quando permission_bitmask = 0.<br /> 1 = true<br /> 0 = false |
| object_id | **int** | A ID da entidade na qual a auditoria ocorreu. Isso inclui o seguinte:<br /> Objetos de servidor<br /> Bancos de dados<br /> Objetos de banco de dados<br /> Objetos de esquema<br /> Não permite valor nulo. Retornará 0 se a entidade for o próprio Servidor ou se a auditoria não for realizada no nível de um objeto. Por exemplo, Autenticação. |  
| object_name | **sysname** | O nome da entidade na qual a auditoria ocorreu. Isso inclui o seguinte:<br /> Objetos de servidor<br /> Bancos de dados<br /> Objetos de banco de dados<br /> Objetos de esquema<br /> Permite valor nulo. Retornará NULL se a entidade for o próprio Servidor ou se a auditoria não for realizada no nível de um objeto. Por exemplo, Autenticação. |
| permission_bitmask | **varbinary(16)** | Em algumas ações, são as permissões que foram concedidas, negadas ou revogadas. |
| response_rows | **bigint** | **Aplica-se ao**: Instância de banco de dados SQL e gerenciado do Azure<br /><br /> Número de linhas retornadas no conjunto de resultados. |  
| schema_name | **sysname** | O contexto do esquema no qual a ação aconteceu. Permite valor nulo. Retorna NULL para auditorias ocorrendo fora de um esquema. |  
| sequence_group_id | **varbinary** | **Aplica-se ao**: SQL Server somente (começando com 2016)<br /><br />  Identificador exclusivo |  
| sequence_number | **int** | Rastreia a sequência de registros dentro de um único registro de auditoria que é muito grande para se ajustar no buffer de gravação das auditorias. Não permite valor nulo. |  
| server_instance_name | **sysname** | Nome da instância de servidor no qual a auditoria ocorreu. O formato servidor\instância padrão é usado. |  
| server_principal_id | **int** | ID do contexto de logon em que a ação é executada. Não permite valor nulo. |  
| server_principal_name | **sysname** | Logon atual. Permite valor nulo. |  
| server_principal_sid | **varbinary** | SID do logon atual. Permite valor nulo. |  
| session_id | **smallint** | Identificação da sessão em que ocorreu o evento. Não permite valor nulo. |  
| session_server_principal_name | **sysname** | Entidade de servidor para a sessão. Permite valor nulo. |  
| instrução | **nvarchar(4000)** | Instrução TSQL, se existir. Permite valor nulo. Retorna NULL se não aplicável. |  
| succeeded | **bit** | Indica se a ação que acionou o evento foi bem-sucedida. Não permite valor nulo. Para todos os demais eventos que não são eventos de logon, reporta somente se a verificação de permissões foi bem-sucedida ou não, e não a operação.<br /> 1 = Êxito<br /> 0 = falha |
| target_database_principal_id | **int** | O banco de dados principal no qual a operação GRANT/DENY/REVOKE é executada. Não permite valor nulo. Retorna 0 se não aplicável. |  
| target_database_principal_name | **sysname** | Usuário de destino da ação. Permite valor nulo. Retorna NULL se não aplicável. |  
| target_server_principal_id | **int** | Diretor de Servidor que o GRANT/operação do DENY/REVOKE é executada em. Não permite valor nulo. Retorna 0 se não aplicável. |  
| target_server_principal_name | **sysname** | Logon de destino da ação. Permite valor nulo. Retorna NULL se não aplicável. |  
| target_server_principal_sid | **varbinary** | SID do logon de destino. Permite valor nulo. Retorna NULL se não aplicável. |  
| transaction_id | **bigint** | **Aplica-se ao**: SQL Server somente (começando com 2016)<br /><br /> Identificador exclusivo para identificar vários eventos de auditoria em uma transação |  
| user_defined_event_id | **smallint** | **Aplica-se ao**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], instância de BD SQL do Azure e gerenciado<br /><br /> Id de evento definido pelo usuário passado como um argumento para **sp_audit_write**. **NULO** para eventos do sistema (padrão) e diferente de zero para evento definido pelo usuário. Para obter mais informações, consulte [sp_audit_write &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md). |  
| user_defined_information | **nvarchar(4000)** | **Aplica-se ao**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], instância de BD SQL do Azure e gerenciado<br /><br /> Usado para registrar quaisquer informações adicionais que o usuário deseja registrar no log de auditoria usando o **sp_audit_write** procedimento armazenado. |  

  
## <a name="remarks"></a>Comentários  
 Se o *file_pattern* argumento passado para **fn_get_audit_file** faz referência a um caminho ou arquivo não existir, ou se o arquivo não for um arquivo de auditoria, o **MSG_INVALID_AUDIT_FILE**mensagem de erro é retornada.  
  
## <a name="permissions"></a>Permissões

- **SQL Server**: Requer a permissão **CONTROL SERVER** .  
- **Banco de dados SQL do Azure**: Requer o **banco de dados de controle** permissão.     
  - Administradores de servidor podem acessar os logs de auditoria de todos os bancos de dados no servidor.
  - Administradores de servidor não podem acessar somente os logs de auditoria do banco de dados atual.
  - Os BLOBs que não atendem aos critérios acima serão ignorados (uma lista de blobs ignorados será exibida na mensagem de saída de consulta), e a função retornará os logs somente de blobs para o qual o acesso é permitido.  
  
## <a name="examples"></a>Exemplos

- **SQL Server**

  Este exemplo lê de um arquivo chamado `\\serverName\Audit\HIPAA_AUDIT.sqlaudit`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPAA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Banco de Dados SQL do Azure**

  Este exemplo lê de um arquivo chamado `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`:  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  Este exemplo lê a partir do mesmo arquivo, como mostrado acima, mas com outras cláusulas de T-SQL (**superior**, **ORDER BY**, e **onde** cláusula para filtrar os registros de auditoria retornados a função):
  
  ```  
  SELECT TOP 10 * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default)
  WHERE server_principal_name = 'admin1'
  ORDER BY event_time
  GO
  ```  

  Este exemplo lê todos os logs de auditoria do servidores que começam com `Sh`: 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

Para obter um exemplo completo de como criar uma auditoria, consulte [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).

Para obter informações sobre como configurar a auditoria de banco de dados SQL, consulte [Introdução à auditoria de banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-auditing).
  
## <a name="see-also"></a>Consulte também  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
