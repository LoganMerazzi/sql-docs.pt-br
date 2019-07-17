---
title: sp_serveroption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_serveroption_TSQL
- sp_serveroption
dev_langs:
- TSQL
helpviewer_keywords:
- 7343 (Database Engine error)
- sp_serveroption
ms.assetid: 47d04a2b-dbf0-4f15-bd9b-81a2efc48131
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1fcd6f158908893ce5eb86c24a3bb3882867bc2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104377"
---
# <a name="spserveroption-transact-sql"></a>sp_serveroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define opções de servidor para servidores remotos e servidores vinculados.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_serveroption [@server = ] 'server'   
      ,[@optname = ] 'option_name'       
      ,[@optvalue = ] 'option_value' ;  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server = ] 'server'` É o nome do servidor para o qual definir a opção. *server* é **sysname**, sem padrão.  
  
`[ @optname = ] 'option_name'` É a opção de definir para o servidor especificado. *option_name* está **varchar (** 35 **)** , sem padrão. *option_name* pode ser qualquer um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**compatível com agrupamento**|Afeta a execução da Consulta Distribuída nos servidores vinculados. Se essa opção é definida como **verdadeira**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pressupõe que todos os caracteres no servidor vinculado são compatíveis com o servidor local, em relação à sequência de agrupamento e conjunto de caracteres (ou ordem de classificação). Isso permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envie comparações sobre colunas de caracteres ao provedor. Se essa opção não estiver definida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre avaliará comparações sobre colunas de caracteres localmente.<br /><br /> Essa opção deve ser definida somente se você tiver certeza de que a fonte de dados correspondente ao servidor vinculado tem o mesmo conjunto de caracteres e ordem de classificação do servidor local.|  
|**nome de agrupamento**|Especifica o nome do agrupamento usado pela fonte de dados remota se **usar agrupamento remoto** é **verdadeiro** e a fonte de dados não é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados. O nome deve ser uma das ordenações que têm suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Use essa opção ao acessar uma origem de dados OLE DB diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas cuja ordenação coincide com uma das ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> O servidor vinculado deve fornecer suporte a uma única ordenação a ser usada para todas as colunas naquele servidor. Não defina essa opção se o servidor vinculado fornecer suporte a várias ordenações dentro de uma única fonte de dados ou se a ordenação do servidor vinculado não puder ser determinada para corresponder a uma das ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**tempo limite de conexão**|Segundos de valuein de tempo limite para conexão a um servidor vinculado.<br /><br /> Se **0**, use o **sp_configure** padrão.|  
|**acesso a dados**|Habilita e desabilita um servidor vinculado para o acesso às consultas distribuídas. Pode ser usado apenas para **sys** adicionadas por meio de entradas **sp_addlinkedserver**.|  
|**dist**|Distribuidor.|  
|**validação de esquema lenta**|Determina se o esquema de tabelas remotas será verificado.<br /><br /> Se **verdadeira**, ignorar a verificação do esquema de tabelas remotas no início da consulta.|  
|**pub**|Editor.|  
|**tempo limite da consulta**|O valor do tempo limite para consultas em um servidor vinculado.<br /><br /> Se **0**, use o **sp_configure** padrão.|  
|**rpc**|Habilita RPC a partir do servidor fornecido.|  
|**RPC out**|Habilita RPC para o servidor fornecido.|  
|**sub**|Assinante.|  
|**system**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**usar agrupamento remoto**|Determina se a ordenação de uma coluna remota ou de um servidor local será usada.<br /><br /> Se **verdadeira**, o agrupamento de colunas remotas é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fontes de dados e o agrupamento especificado em **nome do agrupamento** é usado para não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fontes de dados.<br /><br /> Se **falsos**, consultas distribuídas sempre usarão o agrupamento padrão do servidor local, enquanto **nome do agrupamento** e o agrupamento de colunas remotas serão ignorados. O padrão é **false**. (O **falsos** valor é compatível com a semântica dos agrupamentos usada em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.)|  
|**promoção de transação de proc remoto**|Use esta opção para proteger as ações de um procedimento servidor a servidor por meio de uma transação do MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ). Quando essa opção for TRUE (ou ON) chamar um procedimento armazenado remoto inicia uma transação distribuída e inscreverá a transação com o MS DTC. A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que chama o procedimento armazenado remoto é o que origina a transação e controla a conclusão da transação. Quando as instruções subsequentes COMMIT TRANSACTION ou ROLLBACK TRANSACTION são emitidas para a conexão, a instância controladora solicita que o MS DTC gerencie a conclusão da transação distribuída em todas os computadores envolvidos.<br /><br /> Depois que uma transação distribuída [!INCLUDE[tsql](../../includes/tsql-md.md)] foi iniciada, é possível fazer chamadas de procedimento armazenado remoto a outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que foram definidas como servidores vinculados. Os servidores vinculados são todos inscritos na transação de distribuição do [!INCLUDE[tsql](../../includes/tsql-md.md)], e o MS DTC garante que a transação seja completada em cada servidor vinculado.<br /><br /> Se essa opção estiver definida como FALSE (ou OFF), uma transação local não será promovida a uma transação distribuída durante a chamada de um procedimento remoto em um servidor vinculado.<br /><br /> Se antes de fazer uma chamada de procedimento de servidor a servidor, a transação já for uma transação distribuída, essa opção não terá efeito. A chamada de procedimento em relação ao servidor vinculado executará sob a mesma transação distribuída.<br /><br /> Se antes de fazer uma chamada de procedimento armazenado de servidor a servidor não houver nenhuma transação ativa, essa opção não terá efeito. Em seguida, o procedimento executa em relação ao servidor vinculado sem transações ativas.<br /><br /> O valor padrão dessa opção é TRUE (ou ON).|  
  
`[ @optvalue = ] 'option_value'` Especifica ou não o *option_name* deve ser habilitada (**verdadeiro** ou **na**) ou desabilitado (**FALSE** ou **desativar**). *option_value* está **varchar (** 10 **)** , sem padrão.  
  
 *option_value* pode ser um inteiro não negativo para o **tempo limite de conexão** e **tempo limite de consulta** opções. Para o **nome do agrupamento** opção *option_value* pode ser um nome de agrupamento ou NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Se o **compatível com agrupamento** opção for definida como TRUE, o **nome do agrupamento** será definido automaticamente como NULL. Se **nome do agrupamento** é definido como um valor não nulo, **compatível com agrupamento** será definido automaticamente como FALSE.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER ANY LINKED SERVER no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir configura um servidor vinculado correspondente a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `SEATTLE3`, para que seja compatível com ordenação com a instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Distribuído procedimentos armazenados de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
