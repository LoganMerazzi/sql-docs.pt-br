---
title: sp_addumpdevice (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addumpdevice_TSQL
- sp_addumpdevice
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], defining
- sp_addumpdevice
ms.assetid: c2d2ae49-0808-46d8-8444-db69a69d0ec3
author: stevestein
ms.author: sstein
ms.openlocfilehash: ccd72de184115929483a43fd69d133abe0e195af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117913"
---
# <a name="spaddumpdevice-transact-sql"></a>sp_addumpdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  

Adiciona um dispositivo de backup a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addumpdevice [ @devtype = ] 'device_type'   
    , [ @logicalname = ] 'logical_name'   
    , [ @physicalname = ] 'physical_name'  
      [ , { [ @cntrltype = ] controller_type |  
          [ @devstatus = ] 'device_status' }  
      ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @devtype = ] 'device_type'` É o tipo de dispositivo de backup. *device_type* está **varchar(20)** , sem padrão e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**disk**|Arquivo de disco rígido como dispositivo de backup.|  
|**tape**|Qualquer dispositivo de fita com suporte no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.<br /><br /> Observação: O suporte a dispositivos de backup em fita será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.|  
  
`[ @logicalname = ] 'logical_name'` É o nome lógico do dispositivo de backup usado nas instruções BACKUP e restauração. *logical_name* está **sysname**, sem padrão, e não pode ser NULL.  
  
`[ @physicalname = ] 'physical_name'` É o nome físico do dispositivo de backup. Os nomes físicos devem seguir as regras para nomes de arquivo do sistema operacional ou convenções universais de nomenclatura de dispositivos de rede e devem incluir um caminho completo. *physical_name* está **nvarchar (260)** , sem nenhum padrão de valor e não pode ser NULL.  
  
 Ao criar um dispositivo de backup em um local de rede remota, certifique-se de que o nome com o qual o [!INCLUDE[ssDE](../../includes/ssde-md.md)] foi iniciado tenha os recursos adequados de gravação no computador remoto.  
  
 Se você adicionar um dispositivo de fita, esse parâmetro deve ser o nome físico atribuído ao dispositivo de fita local pelo Windows; Por exemplo,  **\\ \\. \TAPE0** para o primeiro dispositivo de fita no computador. O dispositivo de fita deve ser anexado ao computador servidor; não pode ser usado remotamente. Inclua os nomes que contêm caracteres não alfanuméricos entre aspas.  
  
> [!NOTE]  
>  Esse procedimento insere no nome físico especificado no catálogo. O procedimento não tenta acessar nem criar o dispositivo.  
  
`[ @cntrltype = ] 'controller_type'` Obsoleto. Se especificado, esse parâmetro será ignorado. Há suporte apenas pela compatibilidade com versões anteriores. Novos usos de **sp_addumpdevice** devem omitir esse parâmetro.  
  
`[ @devstatus = ] 'device_status'` Obsoleto. Se especificado, esse parâmetro será ignorado. Há suporte apenas pela compatibilidade com versões anteriores. Novos usos de **sp_addumpdevice** devem omitir esse parâmetro.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_addumpdevice** adiciona um dispositivo de backup para o **sys. backup_devices** exibição do catálogo. O dispositivo pode ser referenciado logicamente em instruções BACKUP e RESTORE. **sp_addumpdevice** não realiza qualquer acesso ao dispositivo físico. O acesso ao dispositivo especificado ocorre apenas quando uma instrução BACKUP ou RESTORE é executada. A criação de um dispositivo de backup lógico pode simplificar as instruções BACKUP e RESTORE, em que a especificação do nome do dispositivo é uma alternativa que usa uma cláusula "TAPE = " ou "DISK = " para especificar o caminho do dispositivo.  
  
 Os problemas de propriedade e de permissões podem interferir no uso dos dispositivos de backup de disco ou de arquivos. Verifique se as permissões de arquivo adequadas foram fornecidas à conta do Windows em que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] foi iniciado.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] oferece suporte a backups de fita para dispositivos de fita que têm suporte no Windows. Para obter mais informações sobre dispositivos de fita com suporte no Windows, consulte a lista de compatibilidade de hardware para Windows. Para exibir os dispositivos de fita disponíveis no computador, use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Use somente as fitas recomendadas para a unidade de fita específica, sugeridas pelo fabricante de unidades. Ao usar unidades DAT (fita de áudio digital), use DDS (Digital Data Storage) de fitas DAT com qualidade para computador.  
  
 **sp_addumpdevice** não pode ser executado dentro de uma transação.  
  
 Para excluir um dispositivo, use [sp_dropdevice](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md) ou[SQL Server Management Studio](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa **diskadmin** .  
  
 Requer permissão para gravar no disco.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-adding-a-disk-dump-device"></a>A. Adicionando um dispositivo de despejo de disco  
 O exemplo a seguir adiciona um dispositivo de backup de disco denominado `mydiskdump`, com o nome físico `c:\dump\dump1.bak`.  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'mydiskdump', 'c:\dump\dump1.bak';  
```  
  
### <a name="b-adding-a-network-disk-backup-device"></a>B. Adicionando um dispositivo de backup de disco de rede  
 O exemplo a seguir mostra a adição de um dispositivo de backup de disco remoto denominado `networkdevice`. O nome sob o qual o [!INCLUDE[ssDE](../../includes/ssde-md.md)] foi iniciado deve ter permissões para aquele arquivo remoto (`\\<servername>\<sharename>\<path>\<filename>.bak`).  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'networkdevice',  
    '\\<servername>\<sharename>\<path>\<filename>.bak';  
```  
  
### <a name="c-adding-a-tape-backup-device"></a>C. Adicionando um dispositivo de backup em fita  
 O exemplo a seguir adiciona o dispositivo `tapedump1` ao nome físico `\\.\tape0`.  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0';  
```  
  
### <a name="d-backing-up-to-a-logical-backup-device"></a>D. Fazendo backup em um dispositivo de backup lógico  
 O exemplo a seguir cria um dispositivo de backup lógico, `AdvWorksData`, para um arquivo de disco de backup. O exemplo faz backup do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nesse dispositivo de backup lógico.  
  
```  
USE master;  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksData',   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\BACKUP\AdvWorksData.bak';  
GO  
BACKUP DATABASE AdventureWorks2012   
 TO AdvWorksData  
   WITH FORMAT;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
