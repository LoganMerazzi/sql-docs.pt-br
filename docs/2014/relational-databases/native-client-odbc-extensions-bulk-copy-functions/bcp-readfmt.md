---
title: bcp_readfmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_readfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_readfmt function
ms.assetid: 654001c8-ae9f-425c-b820-f0191bf89367
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76ccc4271877b81ae103a89b5df727b74017d9ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62688665"
---
# <a name="bcpreadfmt"></a>bcp_readfmt
  Lê uma definição de formato do arquivo de dados do arquivo de formato especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_readfmt (  
HDBC   
hdbc  
,  
LPCTSTR   
szFormatFile  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *szFormatFile*  
 É o caminho e o nome do arquivo que contém os valores de formato para o arquivo de dados.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Após `bcp_readfmt` lê os valores de formato, fará as chamadas apropriadas aos [bcp_columns](bcp-columns.md) e [bcp_colfmt](bcp-colfmt.md). Não há necessidade de você analisar um arquivo de formato e fazer essas chamadas.  
  
 Para manter um arquivo de formato, chame [bcp_writefmt](bcp-writefmt.md). Chamadas para `bcp_readfmt` podem referenciar formatos salvos. Para obter mais informações, consulte [bcp_init](bcp-init.md).  
  
 Como alternativa, o utilitário de cópia em massa (**bcp**) pode salvar formatos de dados definido pelo usuário em arquivos que podem ser referenciados por `bcp_readfmt`. Para obter mais informações sobre o **bcp** utilitário e a estrutura dos **bcp** arquivos de formato de dados, consulte [importação em massa e importação de dados &#40;do SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 O `BCPDELAYREADFMT` valor da *eOption* parâmetro [bcp_control](bcp-control.md) modifica o comportamento de bcp_readfmt.  
  
> [!NOTE]  
>  O arquivo de formato deve ter sido gerado pela versão 4.2 ou posterior do utilitário **bcp** .  
  
## <a name="example"></a>Exemplo  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, _T("myTable"), _T("myData.csv"),  
   _T("myErrors"),    DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_readfmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   cout << nRowsProcessed << " rows copied to SQL Server\n";  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
