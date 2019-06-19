---
title: Suporte a transações locais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- SQL Server Native Client OLE DB provider, transactions
- local transactions [OLE DB]
ms.assetid: 78f2e5fc-b6fb-4eda-9f71-991a4d6c4902
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b75104940cca183005f8a465ea19d0a517247c25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213812"
---
# <a name="supporting-local-transactions"></a>Dando suporte a transações locais
  Uma sessão delimita o escopo da transação para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transação local do provedor OLE DB do Native Client. Quando, na direção de um consumidor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client envia uma solicitação para uma instância conectada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a solicitação constitui uma unidade de trabalho para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client. Transações locais sempre quebram uma ou mais unidades de trabalho em um único [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessão do provedor OLE DB do Native Client.  
  
 Usando o padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmação automática do provedor OLE DB do Native Client, uma única unidade de trabalho é tratado como o escopo de uma transação local. Apenas uma unidade participa da transação local. Quando uma sessão é criada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client inicia uma transação para a sessão. Na conclusão bem-sucedida de uma unidade de trabalho, o trabalho é confirmado. Em caso de falha, qualquer trabalho começado é revertido e o erro é relatado ao consumidor. Em ambos os casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client inicia uma nova transação local para a sessão, de modo que todo o trabalho é realizado em uma transação.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client pode direcionar um controle mais preciso sobre o escopo de transação local usando o **ITransactionLocal** interface. Quando uma sessão do consumidor inicia uma transação, todas as unidades de trabalho da sessão entre o ponto inicial da transação e as eventuais chamadas do método **Commit** ou **Abort** são tratadas como uma unidade atômica. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client inicia uma transação quando instruído a fazer isso pelo consumidor implicitamente. Se o consumidor não solicitar retenção, a sessão reverterá para o comportamento pai em nível de transação, geralmente o modo de confirmação automática.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao provedor de OLE DB do Native Client **itransactionlocal:: Starttransaction** parâmetros da seguinte maneira.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*isoLevel*[in]|O nível de isolamento a ser usado com esta transação. Em transações locais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client dá suporte para o seguinte:<br /><br /> -   ISOLATIONLEVEL_UNSPECIFIED<br />-   ISOLATIONLEVEL_CHAOS<br />-   ISOLATIONLEVEL_READUNCOMMITTED<br />-   ISOLATIONLEVEL_READCOMMITTED<br />-   ISOLATIONLEVEL_REPEATABLEREAD<br />-   ISOLATIONLEVEL_CURSORSTABILITY<br />-   ISOLATIONLEVEL_REPEATABLEREAD<br />-   ISOLATIONLEVEL_SERIALIZABLE<br />-   ISOLATIONLEVEL_ISOLATED<br />-   ISOLATIONLEVEL_SNAPSHOT **Note:**  Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], ISOLATIONLEVEL_SNAPSHOT é válido para o *isoLevel* argumento ou não o controle de versão está habilitado para o banco de dados. Porém, ocorrerá um erro se o usuário tentar executar uma instrução e o controle de versão não estiver habilitado e/ou o banco de dados não for somente leitura. Além disso, o erro XACT_E_ISOLATIONLEVEL ocorrerá se ISOLATIONLEVEL_SNAPSHOT for especificado como o *isoLevel* quando conectado a uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|*isoFlags*[in]|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retornará um erro para qualquer valor diferente de zero.|  
|*pOtherOptions*[in]|Se não for NULL, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client solicita o objeto de opções da interface. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client retornará XACT_E_NOTIMEOUT se o objeto de opções *ulTimeout* membro não é zero. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client ignora o valor da *szDescription* membro.|  
|*pulTransactionLevel*[out]|Se não for NULL, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retornará o nível aninhado da transação.|  
  
 Para transações locais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB do Native Client provedor implementa **ITransaction:: Abort** parâmetros da seguinte maneira.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*pboidReason*[in]|Ignorado se definido. Pode ser NULL com segurança.|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando for falso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client reverte ao modo de confirmação automática para a sessão.|  
|*fAsync*[in]|Anulação assíncrona não é compatível com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retornará XACT_E_NOTSUPPORTED se o valor não é FALSE.|  
  
 Para transações locais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB do Native Client provedor implementa **ITransaction:: Commit** parâmetros da seguinte maneira.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando for falso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client reverte ao modo de confirmação automática para a sessão.|  
|*grfTC*[in]|Fase um retorna e assíncrono não são suportados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retorna XACT_E_NOTSUPPORTED para qualquer valor diferente de XACTTC_SYNC.|  
|*grfRM*[in]|Deve ser 0.|  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor OLE DB do Native Client na sessão são preservados em uma confirmação local ou anular a operação com base nos valores das propriedades do conjunto de linhas DBPROP_ABORTPRESERVE e DBPROP_COMMITPRESERVE. Por padrão, essas propriedades são VARIANT_FALSE e todos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor OLE DB do Native Client na sessão são perdidos após uma operação de confirmação ou anulação.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client não implementa o **ITransactionObject** interface. Uma tentativa do consumidor de recuperar uma referência na interface retorna E_NOINTERFACE.  
  
 Este exemplo usa **ITransactionLocal**.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*   pIDBCreateSession   = NULL;  
ITransaction*       pITransaction       = NULL;  
IDBCreateCommand*   pIDBCreateCommand   = NULL;  
IRowset*            pIRowset            = NULL;  
  
HRESULT             hr;  
  
// Get the command creation and local transaction interfaces for the  
// session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
if (FAILED(hr = pIDBCreateCommand->QueryInterface(IID_ITransactionLocal,  
    (void**) &pITransaction)))  
    {  
    // Process error. Release any references and return.  
    }  
  
// Start the local transaction.  
if (FAILED(hr = ((ITransactionLocal*) pITransaction)->StartTransaction(  
    ISOLATIONLEVEL_REPEATABLEREAD, 0, NULL, NULL)))  
    {  
    // Process error from StartTransaction. Release any references and  
    // return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then terminate.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, XACTTC_SYNC, 0)))  
        {  
        // Get error from failed commit.  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Transações](transactions.md)   
 [Trabalhando com isolamento de instantâneo](../native-client/features/working-with-snapshot-isolation.md)  
  
  
