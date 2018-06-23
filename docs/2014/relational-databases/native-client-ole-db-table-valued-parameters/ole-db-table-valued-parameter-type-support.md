---
title: Suporte ao tipo de parâmetro com valor de tabela de banco de dados OLE | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
ms.assetid: 147036a0-260e-4f81-8b3b-89209e023a32
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4b6416715cc6226766773d3f1d630dc2e42e1e37
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115191"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>Suporte ao tipo de parâmetro com valor de tabela OLE DB
  Este tópico descreve suporte ao tipo OLE DB para parâmetros com valor de tabela.  
  
## <a name="table-valued-parameter-rowset-object"></a>Objeto de conjunto de linhas de parâmetro com valor de tabela  
 É possível criar um objeto de conjunto de linhas especializado para parâmetros com valor de tabela. Você pode criar o objeto de conjunto de linhas de parâmetro com valor de tabela usando ITableDefinitionWithConstraints::CreateTableWithConstraints ou IOpenRowset:: OPENROWSET. Para fazer isso, defina o *eKind* membro o *pTableID* parâmetro como DBKIND_GUID_NAME e forneça o CLSID_ROWSET_INMEMORY como o *guid* membro. O nome do tipo de servidor para o parâmetro com valor de tabela deve ser especificado no *pwszName* membro *pTableID* ao usar IOpenRowset:: OPENROWSET. O objeto de conjunto de linhas para parâmetros com valor de tabela se comporta como um objeto do provedor OLE DB do SQL Server Native Client normal.  
  
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
  
 Não há suporte para conversões para e de DBTYPE_TABLE para qualquer outro tipo. IConvertType::CanConvert retornará S_FALSE em conversão sem suporte para qualquer solicitação que não seja a conversão de DBTYPE_TABLE para. Isso supõe DBCONVERTFLAGS_PARAMETER no objeto de comando.  
  
## <a name="methods"></a>Métodos  
 Para obter informações sobre métodos OLE DB que oferecem suporte a parâmetros com valor de tabela, consulte [suporte de tipo de parâmetro OLE DB Table-Valued &#40;métodos&#41;](ole-db-table-valued-parameter-type-support-methods.md).  
  
## <a name="properties"></a>Propriedades  
 Para obter informações sobre propriedades de OLE DB que oferecem suporte a parâmetros com valor de tabela, consulte [suporte de tipo de parâmetro OLE DB Table-Valued &#40;propriedades&#41;](ole-db-table-valued-parameter-type-support-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  