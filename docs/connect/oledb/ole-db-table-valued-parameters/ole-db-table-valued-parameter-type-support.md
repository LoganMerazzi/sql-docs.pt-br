---
title: Suporte ao tipo de parâmetro com valor de tabela do OLE DB | Microsoft Docs
description: Suporte para o tipo de parâmetro com valor de tabela do OLE DB
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
author: pmasl
ms.author: pelopes
ms.openlocfilehash: abff9abb82ad0ff54d9b1126541b98babbd6bd76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015315"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>Suporte ao tipo de parâmetro com valor de tabela OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artigo descreve o suporte de tipos OLE DB em parâmetros com valor de tabela.  
  
## <a name="table-valued-parameter-rowset-object"></a>Objeto de conjunto de linhas de parâmetro com valor de tabela  
 É possível criar um objeto de conjunto de linhas especializado para parâmetros com valor de tabela. Você cria o objeto de conjunto de linhas de parâmetro com valor de tabela usando ITableDefinitionWithConstraints:: CreateTableWithConstraints ou IOpenRowset:: OpenRowset. Para fazer isso, defina o membro *eKind* do parâmetro *pTableID* como DBKIND_GUID_NAME e forneça o CLSID_ROWSET_INMEMORY como o membro *guid*. O nome do tipo de servidor para o parâmetro com valor de tabela deve ser especificado no membro *pwszName* de *PTableID* ao usar IOpenRowset:: OPENROWSET. O objeto de conjunto de linhas de parâmetro com valor de tabela se comporta como um driver de OLE DB regular para SQL Server objeto.  
  
```  
const GUID CLSID_ROWSET_TVP =   
{0xc7ef28d5, 0x7bee, 0x443f, {0x86, 0xda, 0xe3, 0x98, 0x4f, 0xcd, 0x4d, 0xf9}};  
  
CoType RowsetTVP  
{  
[mandatory] interface IAccessor;  
[mandatory] interface IColumnsInfo;  
[mandatory] interface IConvertType;  
[mandatory] interface IRowset;  
[mandatory] interface IRowsetInfo;  
[optional]  interface IColumnsRowset;  
[optional]  interface IRowsetChange;  
[optional]  interface ISupportErrorInfo;  
};  
```  
  
## <a name="dbtypetable"></a>DBTYPE_TABLE  
 Um tipo novo, DBTYPE_TABLE, representa um tipo de tabela. Esse tipo especifica parâmetros com valor de tabela em várias interfaces OLE DB em que um DBTYPE é obrigatório.  
  
```  
#define DBTYPE_TABLE (143)  
```  
  
 DBTYPE_TABLE tem o mesmo formato de DBTYPE_IUNKNOWN. Trata-se de um ponteiro para um objeto no buffer de dados. Para obter a especificação completa nas associações, o consumidor preenche o buffer DBOBJECT, com *iid* definido como uma das interfaces de objeto de conjunto de linhas (IID_IRowset). Se nenhum DBOBJECT for especificado nas associações, IID_IRowset será assumido.  
  
 Não há suporte para conversões bidirecionalmente em DBTYPE_TABLE em qualquer outro tipo. IConvertType::CanConvert retornará S_FALSE em uma conversão não compatível para qualquer solicitação que não seja a conversão de DBTYPE_TABLE em DBTYPE_TABLE. Isso supõe DBCONVERTFLAGS_PARAMETER no objeto Command.  
  
## <a name="methods"></a>Métodos  
 Para obter informações sobre os métodos de OLE DB que dão suporte a parâmetros com valor de tabela, consulte [OLE DB &#40;métodos&#41;de suporte de tipo de parâmetro com valor de tabela](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md).  
  
## <a name="properties"></a>Propriedades  
 Para obter informações sobre OLE DB propriedades que dão suporte a parâmetros com valor de tabela, consulte [OLE DB propriedades&#41;de &#40;suporte ao tipo de parâmetro com valor de tabela](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
