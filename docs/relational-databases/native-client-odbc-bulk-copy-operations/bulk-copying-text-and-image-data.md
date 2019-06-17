---
title: Cópia de dados de texto e imagem em massa | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5032f6d038130fc78405949a171a39a6f0ec1842
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014018"
---
# <a name="bulk-copying-text-and-image-data"></a>Copiando em massa dados de texto e imagem
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Grandes **texto**, **ntext**, e **imagem** valores são copiados em massa usando o [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) função. Você codificar [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para o **texto**, **ntext**, ou **imagem** coluna com um *pData* ponteiro definido como NULL indicando que os dados serão fornecidos com **bcp_moretext**. É importante especificar o comprimento exato de dados fornecidos para cada **texto**, **ntext**, ou **imagem** coluna em cada linha copiada em massa. Se o comprimento dos dados para uma coluna for diferente do comprimento da coluna especificado na [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md), use [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) para definir o comprimento para o valor adequado. Um [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) envia todos os não -**texto**, não-**ntext**e não-**imagem** dados; você, em seguida, chamar **bcp_moretext** para enviar o **texto**, **ntext**, ou **imagem** dados em unidades separadas. Funções de cópia em massa determinam que todos os dados foram enviados para a atual **texto**, **ntext**, ou **imagem** coluna quando a soma dos comprimentos de dados enviados por meio de **bcp_moretext** é igual ao comprimento especificado no último **bcp_collen** ou **bcp_bind**.  
  
 **bcp_moretext** não tem nenhum parâmetro para identificar uma coluna. Quando houver vários **texto**, **ntext**, ou **imagem** colunas em uma linha **bcp_moretext** opera o **texto**, **ntext**, ou **imagem** colunas iniciando com a coluna com o número ordinal mais baixo e continuando para a coluna com o número ordinal mais alto. **bcp_moretext** vai de uma coluna para a próxima quando a soma dos comprimentos de dados enviados é igual ao comprimento especificado no último **bcp_collen** ou **bcp_bind** para a coluna atual.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações de cópia em massa &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
