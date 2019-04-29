---
title: Criando índices do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
- adding indexes
ms.assetid: 6239d440-2818-4b98-bb79-732dced41952
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bda39528b6bc04fbff6faa4c72d85a4eccd576c6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046448"
---
# <a name="creating-sql-server-indexes"></a>Criando índices do SQL Server
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client expõe a **iindexdefinition:: CreateIndex** função, permitindo que os consumidores definam novos índices em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client cria índices de tabela como índices ou restrições. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] concede privilégios para criação de restrições ao proprietário da tabela, ao proprietário do banco de dados e aos membros de determinadas funções administrativas. Por padrão, apenas o proprietário da tabela pode criar um índice em uma tabela. Portanto, o êxito ou a falha de **CreateIndex** depende não apenas dos direitos de acesso do usuário do aplicativo, mas também do tipo de índice criado.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pTableID*. O membro *eKind* de *pTableID* precisa ser DBKIND_NAME.  
  
 O *pIndexID* parâmetro pode ser NULL, e se for, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client cria um nome exclusivo para o índice. O consumidor pode capturar o nome do índice especificando um ponteiro válido para um DBID no parâmetro *ppIndexID*.  
  
 O consumidor pode especificar o nome do índice como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* do parâmetro *pIndexID*. O membro *eKind* de *pIndexID* precisa ser DBKIND_NAME.  
  
 O consumidor especifica a coluna ou as colunas que participam do índice por nome. Para cada estrutura DBINDEXCOLUMNDESC usada em **CreateIndex**, o membro *eKind* da *pColumnID* precisa ser DBKIND_NAME. O nome da coluna é especificado como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no *pColumnID*.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suporte ordem crescente de valores no índice. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retornará E_INVALIDARG se o consumidor especificar DBINDEX_COL_ORDER_DESC em qualquer estrutura DBINDEXCOLUMNDESC.  
  
 **CreateIndex** interpreta as propriedades de índice, conforme mostrado a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/W: leitura/gravação<br /><br /> Padrão: None<br /><br /> Descrição: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client não oferece suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_CLUSTERED|R/W: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Clustering de índice de controles.<br /><br /> VARIANT_TRUE: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client tenta criar um índice clusterizado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a no máximo um índice clusterizado em qualquer tabela.<br /><br /> VARIANT_FALSE: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client tenta criar um índice não clusterizado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.|  
|DBPROP_INDEX_FILLFACTOR|R/W: leitura/gravação<br /><br /> Padrão: 0<br /><br /> Descrição: Especifica a porcentagem de uma página de índice usada para armazenamento. Para obter mais informações, confira [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql).<br /><br /> O tipo da variante é VT_I4. O valor deve ser maior ou igual a 1 e menor ou igual a 100.|  
|DBPROP_INDEX_INITIALIZE|R/W: leitura/gravação<br /><br /> Padrão: None<br /><br /> Descrição: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client não oferece suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLCOLLATION|R/W: leitura/gravação<br /><br /> Padrão: None<br /><br /> Descrição: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client não oferece suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLS|R/W: leitura/gravação<br /><br /> Padrão: None<br /><br /> Descrição: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client não oferece suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_PRIMARYKEY|R/W: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE Description: Cria o índice como uma integridade referencial, restrição PRIMARY KEY.<br /><br /> VARIANT_TRUE: O índice é criado para dar suporte a restrição de chave primária da tabela. As colunas devem ser não nulas.<br /><br /> VARIANT_FALSE: O índice não é usado como uma restrição PRIMARY KEY para valores de linha na tabela.|  
|DBPROP_INDEX_SORTBOOKMARKS|R/W: leitura/gravação<br /><br /> Padrão: None<br /><br /> Descrição: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client não oferece suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TEMPINDEX|R/W: leitura/gravação<br /><br /> Padrão: None<br /><br /> Descrição: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client não oferece suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TYPE|R/W: leitura/gravação<br /><br /> Padrão: None<br /><br /> Descrição: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client não oferece suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_UNIQUE|R/W: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Cria o índice como uma restrição UNIQUE na coluna participante ou colunas.<br /><br /> VARIANT_TRUE: O índice é usado para restringir exclusivamente os valores de linha na tabela.<br /><br /> VARIANT_FALSE: O índice não restringe valores de linha com exclusividade.|  
  
 Na propriedade específica do provedor definida DBPROPSET_SQLSERVERINDEX, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client define a seguinte propriedade de informações de fonte de dados.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|Digite: VT_BOOL (R/W)<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Quando essa propriedade é especificada com um valor de VARIANT_TRUE com iindexdefinition:: CreateIndex, isso resulta em um índice xml primário que está sendo criado que corresponde à coluna que está sendo indexada. Se essa propriedade for VARIANT_TRUE, cIndexColumnDescs deverá ser 1, caso contrário, será um erro.|  
  
 Este exemplo cria um índice de chave primária:  
  
```  
// This CREATE TABLE statement shows the referential integrity and   
// PRIMARY KEY constraint on the OrderDetails table that will be created   
// by the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//        CONSTRAINT PK_OrderDetails  
//        PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
HRESULT CreatePrimaryKey  
    (  
    IIndexDefinition* pIIndexDefinition  
    )  
    {  
    HRESULT             hr = S_OK;  
  
    DBID                dbidTable;  
    DBID                dbidIndex;  
    const ULONG         nCols = 2;  
    ULONG               nCol;  
    const ULONG         nProps = 2;  
    ULONG               nProp;  
  
    DBINDEXCOLUMNDESC   dbidxcoldesc[nCols];  
    DBPROP              dbpropIndex[nProps];  
    DBPROPSET           dbpropset;  
  
    DBID*               pdbidIndexOut = NULL;  
  
    // Set up identifiers for the table and index.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    dbidIndex.eKind = DBKIND_NAME;  
    dbidIndex.uName.pwszName = L"PK_OrderDetails";  
  
    // Set up column identifiers.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbidxcoldesc[nCol].pColumnID = new DBID;  
        dbidxcoldesc[nCol].pColumnID->eKind = DBKIND_NAME;  
  
        dbidxcoldesc[nCol].eIndexColOrder = DBINDEX_COL_ORDER_ASC;  
        }  
    dbidxcoldesc[0].pColumnID->uName.pwszName = L"OrderID";  
    dbidxcoldesc[1].pColumnID->uName.pwszName = L"ProductID";  
  
    // Set properties for the index. The index is clustered,  
    // PRIMARY KEY.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        dbpropIndex[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        dbpropIndex[nProp].colid = DB_NULLID;  
  
        VariantInit(&(dbpropIndex[nProp].vValue));  
  
        dbpropIndex[nProp].vValue.vt = VT_BOOL;  
        }  
    dbpropIndex[0].dwPropertyID = DBPROP_INDEX_CLUSTERED;  
    dbpropIndex[0].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropIndex[1].dwPropertyID = DBPROP_INDEX_PRIMARYKEY;  
    dbpropIndex[1].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropset.rgProperties = dbpropIndex;  
    dbpropset.cProperties = nProps;  
    dbpropset.guidPropertySet = DBPROPSET_INDEX;  
  
    hr = pIIndexDefinition->CreateIndex(&dbidTable, &dbidIndex, nCols,  
        dbidxcoldesc, 1, &dbpropset, &pdbidIndexOut);  
  
    // Clean up dynamically allocated DBIDs.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        delete dbidxcoldesc[nCol].pColumnID;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
