---
title: 'Ibcpsession:: Bcpreadfmt (OLE DB) | Microsoft Docs'
description: 'Usando ibcpsession:: Bcpreadfmt para ler dados de um arquivo de formato (OLE DB)'
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 46139cddfb91c974f78547794bec55251abce25c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790825"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Lê informações de formato relativas a cada coluna no arquivo de formato.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Remarks  
 O método **BCPReadFmt** é usado para ler dados de um arquivo de formato que especifica o formato de dados no arquivo de dados. Este método é capaz de detectar a versão correta do arquivo de formato. Ele pode detectar automaticamente se o arquivo de formato está em xml ou formato de texto de estilo antigo e se comporta adequadamente. As versões de arquivo de formato com suporte pelo Driver do OLE DB para SQL Server BCP são versão 6.0 ou mais recente.  
  
 Depois que o método **BCPReadFmt** lê os valores de formato, ele faz as chamadas apropriadas aos métodos [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) e [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md). Não há necessidade de o usuário analisar um arquivo de formato e fazer essas chamadas.  
  
 Para salvar um arquivo de formato, chame o método [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) . As chamadas ao método **BCPReadFmt** podem referenciar formatos salvos. Como alternativa, o utilitário de cópia em massa (**bcp**) pode salvar formatos de dados definidos pelo usuário em arquivos que podem ser referenciados pelo método **BCPReadFmt** .  
  
 O **BCP_OPTION_DELAYREADFMT** valor de *eOption* parâmetro do [ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) modifica o comportamento de ibcpsession:: Bcpreadfmt.  
  
## <a name="arguments"></a>Argumentos  
 *pwszFormatFile*[in]  
 O caminho e o nome do arquivo que contém os valores de formato do arquivo de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_FAIL  
 Um erro específico do provedor ocorreu. Para obter informações detalhadas, use a interface [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) .  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o método [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) não foi chamado antes desse método.  
  
## <a name="see-also"></a>Consulte Também  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
