---
title: Suporte a transações distribuídas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- distributed transactions [OLE DB]
- MS DTC
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
- ITransactionJoin interface
- MS DTC, about distributed transaction support
ms.assetid: d250b43b-9260-4ea4-90cc-57d9a2f67ea7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b35715487638a21e71f76788650b3238a3c9290c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213503"
---
# <a name="supporting-distributed-transactions"></a>Dando suporte a transações distribuídas
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Consumidores do provedor de dados OLE DB nativos podem usar o **itransactionjoin:: Jointransaction** método participem de uma transação distribuída coordenada pelo Microsoft Distributed Transaction Coordinator (MS DTC).  
  
 O MS DTC expõe objetos COM que permitem que os clientes iniciem e participem de transações coordenadas através de várias conexões com vários repositórios de dados. Para iniciar uma transação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client usa o MS DTC **ITransactionDispenser** interface. O membro **BeginTransaction** de **ITransactionDispenser** retorna uma referência a um objeto de transação distribuída. Essa referência é passada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client usando **JoinTransaction**.  
  
 O MS DTC dá suporte à confirmação e à anulação assíncronas de transações distribuídas. Para obter a notificação do status da transação assíncrona, o consumidor implementa a interface **ITransactionOutcomeEvents** e a conecta a um objeto de transação do MS DTC.  
  
 Para transações distribuídas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB do Native Client provedor implementa **itransactionjoin:: Jointransaction** parâmetros da seguinte maneira.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*punkTransactionCoord*|Um ponteiro para um objeto de transação do MS DTC.|  
|*IsoLevel*|Ignorado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client. O nível de isolamento para transações coordenadas pelo MS DTC é determinado quando o consumidor faz a aquisição de um objeto de transação do MS DTC.|  
|*IsoFlags*|Deve ser 0. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retornará XACT_E_NOISORETAIN se qualquer outro valor é especificado pelo consumidor.|  
|*POtherOptions*|Se não for NULL, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client solicita o objeto de opções da interface. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client retornará XACT_E_NOTIMEOUT se o objeto de opções *ulTimeout* membro não é zero. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client ignora o valor da *szDescription* membro.|  
  
 Este exemplo coordena a transação usando o MS DTC.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*       pIDBCreateSession   = NULL;  
ITransactionJoin*       pITransactionJoin   = NULL;  
IDBCreateCommand*       pIDBCreateCommand   = NULL;  
IRowset*                pIRowset            = NULL;  
  
// Transaction dispenser and transaction from MS DTC.  
ITransactionDispenser*  pITransactionDispenser = NULL;  
ITransaction*           pITransaction       = NULL;  
  
    HRESULT             hr;  
  
// Get the command creation interface for the session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
// Get a transaction dispenser object from MS DTC and  
// start a transaction.  
if (FAILED(hr = DtcGetTransactionManager(NULL, NULL,  
    IID_ITransactionDispenser, 0, 0, NULL,  
    (void**) &pITransactionDispenser)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
if (FAILED(hr = pITransactionDispenser->BeginTransaction(  
    NULL, ISOLATIONLEVEL_READCOMMITTED, ISOFLAG_RETAIN_DONTCARE,  
    NULL, &pITransaction)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
  
// Join the transaction.  
if (FAILED(pIDBCreateCommand->QueryInterface(IID_ITransactionJoin,  
    (void**) &pITransactionJoin)))  
    {  
    // Process failure to get an interface, release any references, and  
    // then return.  
    }  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) pITransaction, 0, 0, NULL)))  
    {  
    // Process join failure, release any references, and then return.  
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
    // Get error from update, then abort.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, 0, 0)))  
        {  
        // Get error from failed commit.  
        //  
        // If a distributed commit fails, application logic could  
        // analyze failure and retry. In this example, terminate. The   
        // consumer must resolve this somehow.  
        pITransaction->Abort(NULL, FALSE, FALSE);  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Un-enlist from the distributed transaction by setting   
// the transaction object pointer to NULL.  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) NULL, 0, 0, NULL)))  
    {  
    // Process failure, and then return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Transactions](transactions.md)  
  
  
