---
title: sp_cursorexecute (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fcc62c09d42adb10f8984a8f48d8b70e2f5c78de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62723991"
---
# <a name="spcursorexecute-transact-sql"></a>sp_cursorexecute (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria e popula um cursor com base no plano de execução criado por sp_cursorprepare. Neste procedimento, associado a sp_cursorprepare, tem a mesma função que sp_cursoropen, mas é dividido em duas fases. sp_cursorprepare é invocado pela especificação de ID = 4 em um pacote do protocolo TDS.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorexecute prepared_handle, cursor  
    [ , scrollopt[ OUTPUT ]  
    [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,bound param][,...n]]]]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *prepared_handle*  
 É a instrução preparada *manipular* valor retornado por sp_cursorprepare. *prepared_handle* é um parâmetro obrigatório que chama uma **int** valor de entrada.  
  
 *cursor*  
 É o identificador de cursor gerado pelo SQL Server. *cursor* é um parâmetro obrigatório que deve ser fornecido em todos os procedimentos subsequentes que atuam no cursor, por exemplo, sp_cursorfetch  
  
 *scrollopt*  
 Opção de rolagem. *scrollopt* é um parâmetro opcional que requer um **int** valor de entrada. O sp_cursorexecute*scrollopt* parâmetro tem as mesmas opções de valor que sp_cursoropen.  
  
> [!NOTE]  
>  Não há suporte para o valor PARAMETERIZED_STMT.  
  
> [!IMPORTANT]  
>  Se um *scrollopt* valor não for especificado, o valor padrão será KEYSET, independentemente do *scrollopt* valor especificado em sp_cursorprepare.  
  
 *ccopt*  
 Opção de controle de moeda. *ccopt* é um parâmetro opcional que requer um **int** valor de entrada. O sp_cursorexecute*ccopt* parâmetro tem as mesmas opções de valor que sp_cursoropen.  
  
> [!IMPORTANT]  
>  Se um *ccopt* valor não for especificado, o valor padrão será OPTIMISTIC, independentemente do *ccopt* valor especificado em sp_cursorprepare.  
  
 *rowcount*  
 É um parâmetro opcional que significa o número de linhas de buffer de busca a ser usado com AUTO_FETCH. O padrão é 20 linhas. *número de linhas* tem um comportamento diferente quando atribuído como um valor de entrada versus um valor de retorno.  
  
|Como valor de entrada|Como valor de retorno|  
|--------------------|---------------------|  
|Quando AUTO_FETCH é especificado com cursores FAST_FORWARD *rowcount* representa o número de linhas a serem colocadas no buffer de busca.|Representa o número de linhas no conjunto de resultados. Quando o *scrollopt* valor AUTO_FETCH é especificado, *rowcount* retorna o número de linhas que foram buscadas no buffer de busca.|  
  
 *bound_param*  
 Significa o uso opcional de parâmetros adicionais.  
  
> [!NOTE]  
>  Quaisquer parâmetros após o quinto são passados para o plano de instrução como parâmetros de entrada.  
  
## <a name="code-return-value"></a>Valor de retorno do código  
 *número de linhas* pode retornar os valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|-1|Número de linhas desconhecidas.|  
|-n|Uma população assíncrona está em vigor.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="scrollopt-and-ccopt-parameters"></a>Parâmetros scrollopt e ccopt  
 *scrollopt* e *ccopt* são úteis quando os planos em cache são adquiridos por preempção para o cache do servidor, que significa que o identificador preparado que identifica a instrução deve ser recompilado. O *scrollopt* e *ccopt* valores de parâmetro devem corresponder aos valores enviados na solicitação original a sp_cursorprepare.  
  
> [!NOTE]  
>  PARAMETERIZED_STMT não deve ser atribuído a *scrollopt*.  
  
 A falha ao fornecer valores correspondentes resultará na recompilação dos planos, negando as operações de preparação e execução.  
  
## <a name="rpc-and-tds-considerations"></a>Considerações sobre RPC e TDS  
 O sinalizador de entrada RPC RETURN_METADATA pode ser definido como 1 para solicitar que os metadados da lista de seleção de cursor sejam retornados no fluxo TDS.  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
