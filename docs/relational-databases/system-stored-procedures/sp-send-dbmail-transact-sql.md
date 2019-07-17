---
title: sp_send_dbmail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sendmail_sp_TSQL
- sendmail_sp
- SP_SEND_DBMAIL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_send_dbmail
ms.assetid: f1d7a795-a3fd-4043-ac4b-c781e76dab47
author: stevestein
ms.author: sstein
ms.openlocfilehash: 52a89c0220bddde6944e759936dc22ad1f3e0ff2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126298"
---
# <a name="spsenddbmail-transact-sql"></a>sp_send_dbmail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Envia uma mensagem de email aos destinatários especificados. A mensagem pode incluir um conjunto de resultados da consulta, anexos de arquivo ou ambos. Quando o email com êxito é colocado na fila do Database Mail, **sp_send_dbmail** retorna o **mailitem_id** da mensagem. Esse procedimento armazenado está no **msdb** banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_send_dbmail [ [ @profile_name = ] 'profile_name' ]  
    [ , [ @recipients = ] 'recipients [ ; ...n ]' ]  
    [ , [ @copy_recipients = ] 'copy_recipient [ ; ...n ]' ]  
    [ , [ @blind_copy_recipients = ] 'blind_copy_recipient [ ; ...n ]' ]  
    [ , [ @from_address = ] 'from_address' ]  
    [ , [ @reply_to = ] 'reply_to' ]   
    [ , [ @subject = ] 'subject' ]   
    [ , [ @body = ] 'body' ]   
    [ , [ @body_format = ] 'body_format' ]  
    [ , [ @importance = ] 'importance' ]  
    [ , [ @sensitivity = ] 'sensitivity' ]  
    [ , [ @file_attachments = ] 'attachment [ ; ...n ]' ]  
    [ , [ @query = ] 'query' ]  
    [ , [ @execute_query_database = ] 'execute_query_database' ]  
    [ , [ @attach_query_result_as_file = ] attach_query_result_as_file ]  
    [ , [ @query_attachment_filename = ] query_attachment_filename ]  
    [ , [ @query_result_header = ] query_result_header ]  
    [ , [ @query_result_width = ] query_result_width ]  
    [ , [ @query_result_separator = ] 'query_result_separator' ]  
    [ , [ @exclude_query_output = ] exclude_query_output ]  
    [ , [ @append_query_error = ] append_query_error ]  
    [ , [ @query_no_truncate = ] query_no_truncate ]   
    [ , [ @query_result_no_padding = ] @query_result_no_padding ]   
    [ , [ @mailitem_id = ] mailitem_id ] [ OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_name = ] 'profile_name'` É o nome do perfil para enviar a mensagem do. O *profile_name* é do tipo **sysname**, com um padrão NULL. O *profile_name* deve ser o nome de um perfil existente do Database Mail. Quando nenhum *profile_name* for especificado, **sp_send_dbmail** usa o perfil privado padrão para o usuário atual. Se o usuário não tiver um perfil particular padrão, **sp_send_dbmail** usa o perfil público padrão para o **msdb** banco de dados. Se o usuário não tem um perfil particular padrão e não houver nenhum perfil público do padrão para o banco de dados **@profile_name** deve ser especificado.  
  
`[ @recipients = ] 'recipients'` É uma lista delimitada por ponto e vírgula de endereços de email para enviar a mensagem. A lista de destinatários é do tipo **varchar (max)** . Embora esse parâmetro é opcional, pelo menos um dos **@recipients** , **@copy_recipients** , ou **@blind_copy_recipients** deve ser especificado, ou **SP _ send_dbmail** retornará um erro.  
  
`[ @copy_recipients = ] 'copy_recipients'` É que uma lista delimitada por ponto e vírgula de emails de endereços para cópia carbono da mensagem para. A lista de destinatários de cópia é do tipo **varchar (max)** . Embora esse parâmetro é opcional, pelo menos um dos **@recipients** , **@copy_recipients** , ou **@blind_copy_recipients** deve ser especificado, ou **SP _ send_dbmail** retornará um erro.  
  
`[ @blind_copy_recipients = ] 'blind_copy_recipients'` É que uma lista delimitada por ponto e vírgula de email de endereços para cópia oculta a mensagem. A lista de destinatários de cópia oculta é do tipo **varchar (max)** . Embora esse parâmetro é opcional, pelo menos um dos **@recipients** , **@copy_recipients** , ou **@blind_copy_recipients** deve ser especificado, ou **SP _ send_dbmail** retornará um erro.  
  
`[ @from_address = ] 'from_address'` É o valor do 'endereço de origem' da mensagem de email. Esse é um parâmetro opcional usado para substituir as configurações no perfil de email. Esse parâmetro é do tipo **varchar (max)** . As configurações de segurança de SMTP determinarão se essas substituições serão aceitas. Se nenhum parâmetro for especificado, o padrão será NULL.  
  
`[ @reply_to = ] 'reply_to'` É o valor do 'endereço de resposta' da mensagem de email. Aceita apenas um endereço de email como um valor válido. Esse é um parâmetro opcional usado para substituir as configurações no perfil de email. Esse parâmetro é do tipo **varchar (max)** . As configurações de segurança de SMTP determinarão se essas substituições serão aceitas. Se nenhum parâmetro for especificado, o padrão será NULL.  
  
`[ @subject = ] 'subject'` É o assunto da mensagem de email. O assunto é do tipo **nvarchar (255)** . Se nenhum assunto for especificado, o padrão será 'SQL Server Message'.  
  
`[ @body = ] 'body'` É o corpo da mensagem de email. O corpo da mensagem é do tipo **nvarchar (max)** , com um padrão NULL.  
  
`[ @body_format = ] 'body_format'` É o formato do corpo da mensagem. O parâmetro é do tipo **varchar(20)** , com um padrão NULL. Quando especificado, os cabeçalhos da mensagem de saída são definidos para indicar que o corpo da mensagem tem o formato especificado. O parâmetro pode conter um dos seguintes valores:  
  
-   TEXT  
  
-   HTML  
  
 Assume TEXT como padrão.  
  
`[ @importance = ] 'importance'` É a importância da mensagem. O parâmetro é do tipo **varchar(6)** . O parâmetro pode conter um dos seguintes valores:  
  
-   Baixa  
  
-   Normal  
  
-   Alta  
  
 Assume Normal como padrão.  
  
`[ @sensitivity = ] 'sensitivity'` É a sensibilidade da mensagem. O parâmetro é do tipo **varchar(12)** . O parâmetro pode conter um dos seguintes valores:  
  
-   Normal  
  
-   Personal  
  
-   Private  
  
-   Confidential  
  
 Assume Normal como padrão.  
  
`[ @file_attachments = ] 'file_attachments'` É uma lista delimitada por ponto e vírgula de nomes de arquivo para anexar à mensagem de email. Os arquivos da lista devem ser especificados como caminhos absolutos. A lista de anexos é do tipo **nvarchar (max)** . Por padrão, o Database Mail limita os anexos de arquivo a 1 MB por arquivo.  
  
`[ @query = ] 'query'` É uma consulta seja executada. Os resultados da consulta podem ser anexados a um arquivo ou incluídos no corpo da mensagem de email. A consulta é do tipo **nvarchar (max)** e pode conter qualquer [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções. Observe que a consulta é executada em uma sessão separada, variáveis locais no script que chamam **sp_send_dbmail** não estão disponíveis para a consulta.  
  
`[ @execute_query_database = ] 'execute_query_database'` É o contexto de banco de dados dentro do qual o procedimento armazenado executa a consulta. O parâmetro é do tipo **sysname**, com um padrão de banco de dados atual. Esse parâmetro só é aplicável se **@query** for especificado.  
  
`[ @attach_query_result_as_file = ] attach_query_result_as_file` Especifica se o conjunto de resultados da consulta é retornado como um arquivo anexado. *attach_query_result_as_file* é do tipo **bit**, com um padrão de 0.  
  
 Quando o valor for 0, os resultados da consulta são incluídos no corpo da mensagem de email, depois do conteúdo do **@body** parâmetro. Quando o valor for 1, os resultados são retornados como um anexo. Esse parâmetro só é aplicável se **@query** for especificado.  
  
`[ @query_attachment_filename = ] query_attachment_filename` Especifica o nome do arquivo a ser usado para o conjunto de resultados do anexo de consulta. *query_attachment_filename* é do tipo **nvarchar (255)** , com um padrão NULL. Esse parâmetro é ignorado quando *attach_query_result* é 0. Quando *attach_query_result* é 1 e esse parâmetro for NULL, o Database Mail cria um nome de arquivo arbitrário.  
  
`[ @query_result_header = ] query_result_header` Especifica se os resultados da consulta incluem cabeçalhos de coluna. O valor query_result_header é do tipo **bit**. Quando o valor é 1, os resultados da consulta contêm cabeçalhos de coluna. Quando o valor é 0, resultados da consulta não incluem cabeçalhos de coluna. Esse parâmetro assume como padrão **1**. Esse parâmetro só é aplicável se **@query** for especificado.  
 
   >[!NOTE]
   > O seguinte erro pode ocorrer durante a configuração @query_result_header como 0 e a configuração @query_no_truncate como 1:
   > <br> Msg 22050, nível 16, estado 1, linha 12: Falha ao inicializar a biblioteca sqlcmd com número de erro -2147024809.
  
`[ @query_result_width = ] query_result_width` É a largura da linha, em caracteres, a ser usado para formatar os resultados da consulta. O *query_result_width* é do tipo **int**, com um padrão de 256. O valor fornecido deve estar entre 10 e 32767. Esse parâmetro só é aplicável se **@query** for especificado.  
  
`[ @query_result_separator = ] 'query_result_separator'` O caractere é usado para separar as colunas na saída da consulta. O separador é do tipo **char(1)** . Usa como padrão ' ' (espaço).  
  
`[ @exclude_query_output = ] exclude_query_output` Especifica se deve retornar a saída da execução da consulta na mensagem de email. **exclude_query_output** é bit, com um padrão de 0. Quando esse parâmetro é 0, a execução do **sp_send_dbmail** procedimento armazenado imprime a mensagem retornada como resultado da execução da consulta no console. Quando esse parâmetro é 1, a execução do **sp_send_dbmail** procedimento armazenado não imprime nenhuma das mensagens de execução de consulta no console.  
  
`[ @append_query_error = ] append_query_error` Especifica se é necessário enviar o email quando um erro é retornado da consulta especificada na **@query** argumento. **append_query_error** está **bit**, com um padrão de 0. Quando esse parâmetro é 1, o Database Mail envia a mensagem de email e inclui a mensagem de erro de consulta no corpo da mensagem de email. Quando esse parâmetro é 0, o Database Mail não envia a mensagem de email, e **sp_send_dbmail** termina com o código de retorno 1, indicando uma falha.  
  
`[ @query_no_truncate = ] query_no_truncate` Especifica se é necessário executar a consulta com a opção que evita truncamento de tipos de dados de comprimento variável grande (**varchar (max)** , **nvarchar (max)** , **varbinary (max)** **xml**, **texto**, **ntext**, **imagem**e tipos de dados definidos pelo usuário). Quando definido, os resultados da consulta não incluem cabeçalhos de coluna. O *query_no_truncate* valor é do tipo **bit**. Quando o valor é 0 ou não especificado, as colunas na consulta são truncadas com 256 caracteres. Quando o valor é 1, as colunas da consulta não são truncadas. Esse parâmetro assume 0 como padrão.  
  
> [!NOTE]  
>  Quando usado com grandes quantidades de dados, o @**query_no_truncate** opção consome recursos adicionais e pode prejudicar o desempenho do servidor.  
  
`[ @query_result_no_padding ] @query_result_no_padding` O tipo é bit. O padrão é 0. Quando definido como 1, os resultados da consulta não são preenchidos, possivelmente reduzindo o tamanho do arquivo. Se você definir @query_result_no_padding como 1 e defina o @query_result_width parâmetro, o @query_result_no_padding parâmetro substitui o @query_result_width parâmetro.  
  
 Nesse caso, não ocorre nenhum erro.  
 
  >[!NOTE]
  > O seguinte erro pode ocorrer ao definir @query_result_no_padding para 1 e fornecendo um parâmetro para @query_no_truncate:
  > <br> Msg 22050, nível 16, estado 1, linha 0: Falha ao executar a consulta porque o @query_result_no_append e @query_no_truncate são mutuamente exclusivas. 
  
 Se você definir a @query_result_no_padding como 1 e definir o @query_no_truncate parâmetro, um erro será gerado.  
  
`[ @mailitem_id = ] mailitem_id [ OUTPUT ]` O parâmetro de saída opcional retorna o *mailitem_id* da mensagem. O *mailitem_id* é do tipo **int**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Um código de retorno de 0 significa êxito. Qualquer outro valor significa falha. O código de erro para a instrução que falhou é armazenado na @@ERROR variável.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Com êxito, retorna a mensagem que "Email enfileirado".  
  
## <a name="remarks"></a>Comentários  
 Antes do uso, o Database Mail deve ser habilitado usando o Assistente de configuração do Database Mail, ou **sp_configure**.  
  
 **sysmail_stop_sp** interrompe o Database Mail, interrompendo os objetos do Service Broker usa o programa externo. **sp_send_dbmail** ainda aceita email quando Database Mail é interrompido usando **sysmail_stop_sp**. Para iniciar o Database Mail, use **sysmail_start_sp**.  
  
 Quando **@profile** não for especificado, **sp_send_dbmail** usa um perfil padrão. Se o usuário que envia a mensagem de email tiver um perfil particular padrão, o Database Mail irá utilizá-lo. Se o usuário não tiver nenhum perfil particular padrão, **sp_send_dbmail** usa o perfil público padrão. Se não houver nenhum perfil privado do padrão para o usuário e nenhum perfil público padrão, **sp_send_dbmail** retornará um erro.  
  
 **sp_send_dbmail** não oferece suporte a mensagens de email sem conteúdo. Para enviar uma mensagem de email, você deve especificar pelo menos um dos **@body** , **@query** , **@file_attachments** , ou **@subject** . Caso contrário, **sp_send_dbmail** retornará um erro.  
  
 O Database Mail usa o contexto de segurança do usuário atual do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para controlar o acesso a arquivos. Portanto, os usuários são autenticados com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação não é possível anexar arquivos usando **@file_attachments** . O Windows não permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forneça credenciais de um computador remoto para outro. Portanto, o Database Mail pode não conseguir anexar arquivos de um compartilhamento de rede caso o comando seja executado de um computador diferente daquele em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado.  
  
 Se os dois **@query** e **@file_attachments** são especificados e o arquivo não pode ser encontrado, a consulta ainda é executada, mas o email não é enviado.  
  
 Quando uma consulta é especificada, o conjunto de resultados é formatado como texto em linha. Dados binários no resultado são enviados em formato hexadecimal.  
  
 Os parâmetros **@recipients** , **@copy_recipients** , e **@blind_copy_recipients** são listas delimitadas por ponto e vírgula de endereços de email. Pelo menos um desses parâmetros deve ser fornecido, ou **sp_send_dbmail** retornará um erro.  
  
 Ao executar **sp_send_dbmail** sem um contexto de transação, o Database Mail inicia e confirma uma transação implícita. Ao executar **sp_send_dbmail** de dentro de uma transação existente, o Database Mail depende do usuário para confirmar ou reverter qualquer alteração. Ele não inicia uma transação interna.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução **sp_send_dbmail** padrão para todos os membros do **DatabaseMailUser** função de banco de dados no **msdb** banco de dados. No entanto, quando o usuário que está enviando a mensagem não tem permissão para usar o perfil para a solicitação **sp_send_dbmail** retornará um erro e não envia a mensagem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-sending-an-e-mail-message"></a>A. Enviando uma mensagem de email  
 Este exemplo envia uma mensagem de email para o seu amigo usando o endereço de email `myfriend@Adventure-Works.com`. O assunto da mensagem é `Automated Success Message`. O corpo da mensagem contém a sentença `'The stored procedure finished successfully'`.  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @body = 'The stored procedure finished successfully.',  
    @subject = 'Automated Success Message' ;  
```  
  
### <a name="b-sending-an-e-mail-message-with-the-results-of-a-query"></a>B. Enviando uma mensagem de email com os resultados de uma consulta  
 Este exemplo envia uma mensagem de email para o seu amigo usando o endereço de email `yourfriend@Adventure-Works.com`. O assunto da mensagem é `Work Order Count` e executa uma consulta que mostra o número de ordens de trabalho com uma `DueDate` menor que dois dias, após 30 de abril de 2004. O Database Mail anexa o resultado como um arquivo de texto.  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @query = 'SELECT COUNT(*) FROM AdventureWorks2012.Production.WorkOrder  
                  WHERE DueDate > ''2004-04-30''  
                  AND  DATEDIFF(dd, ''2004-04-30'', DueDate) < 2' ,  
    @subject = 'Work Order Count',  
    @attach_query_result_as_file = 1 ;  
```  
  
### <a name="c-sending-an-html-e-mail-message"></a>C. Enviando uma mensagem de email HTML  
 Este exemplo envia uma mensagem de email para o seu amigo usando o endereço de email `yourfriend@Adventure-Works.com`. O assunto da mensagem é `Work Order List` e contém um documento HTML que mostra o número de ordens de trabalho com uma `DueDate` menor que dois dias, após 30 de abril de 2004. O Database Mail envia a mensagem no formato HTML.  
  
```  
DECLARE @tableHTML  NVARCHAR(MAX) ;  
  
SET @tableHTML =  
    N'<H1>Work Order Report</H1>' +  
    N'<table border="1">' +  
    N'<tr><th>Work Order ID</th><th>Product ID</th>' +  
    N'<th>Name</th><th>Order Qty</th><th>Due Date</th>' +  
    N'<th>Expected Revenue</th></tr>' +  
    CAST ( ( SELECT td = wo.WorkOrderID,       '',  
                    td = p.ProductID, '',  
                    td = p.Name, '',  
                    td = wo.OrderQty, '',  
                    td = wo.DueDate, '',  
                    td = (p.ListPrice - p.StandardCost) * wo.OrderQty  
              FROM AdventureWorks.Production.WorkOrder as wo  
              JOIN AdventureWorks.Production.Product AS p  
              ON wo.ProductID = p.ProductID  
              WHERE DueDate > '2004-04-30'  
                AND DATEDIFF(dd, '2004-04-30', DueDate) < 2   
              ORDER BY DueDate ASC,  
                       (p.ListPrice - p.StandardCost) * wo.OrderQty DESC  
              FOR XML PATH('tr'), TYPE   
    ) AS NVARCHAR(MAX) ) +  
    N'</table>' ;  
  
EXEC msdb.dbo.sp_send_dbmail @recipients='yourfriend@Adventure-Works.com',  
    @subject = 'Work Order List',  
    @body = @tableHTML,  
    @body_format = 'HTML' ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Objetos de configuração do Database Mail](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
  
