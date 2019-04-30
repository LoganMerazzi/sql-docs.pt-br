---
title: DataTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc18212852954accfddd9f3082b5c8f8a5485b58
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140281"
---
# <a name="datatypeenum"></a>DataTypeEnum
Especifica o tipo de dados de um [campo](../../../ado/reference/ado-api/field-object.md), [parâmetro](../../../ado/reference/ado-api/parameter-object.md), ou [propriedade](../../../ado/reference/ado-api/property-object-ado.md). O indicador de tipo OLE DB correspondente é mostrado entre parênteses na coluna Descrição da tabela a seguir.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|Um valor de sinalizador, sempre combinado com outro constante de tipo de dados, que indica uma matriz do tipo de dados. Não é aplicável para ADOX.|  
|**adBigInt**|20|Indica um inteiro com sinal de oito bytes (DBTYPE_I8).|  
|**adBinary**|128|Indica um valor de binário (DBTYPE_BYTES).|  
|**adBoolean**|11|Indica um **Boolean** valor (DBTYPE_BOOL).|  
|**adBSTR**|8|Indica uma cadeia de caracteres terminada em nulo (DBTYPE_BSTR) de (Unicode).|  
|**adChapter**|136|Indica um valor de capítulo de quatro bytes que identifica as linhas de um conjunto de linhas filho (DBTYPE_HCHAPTER).|  
|**adChar**|129|Indica um valor de cadeia de caracteres (DBTYPE_STR).|  
|**adCurrency**|6|Indica um valor de moeda (DBTYPE_CY). A moeda é um número de ponto fixo com quatro dígitos à direita da vírgula decimal. Ele é armazenado em um inteiro com sinal de oito bytes dimensionado por 10.000.|  
|**adDate**|7|Indica um valor de data (DBTYPE_DATE). Uma data é armazenada como um duplo, a parte inteira do qual é o número de dias desde 30 de dezembro de 1899 e a parte fracionária é a fração de um dia.|  
|**adDBDate**|133|Indica um valor de data (AAAAMMDD) (DBTYPE_DBDATE).|  
|**adDBTime**|134|Indica um valor de hora (hhmmss) (DBTYPE_DBTIME).|  
|**adDBTimeStamp**|135|Indica um carimbo de data/hora (yyyymmddhhmmss mais uma fração em bilionésimos) (DBTYPE_DBTIMESTAMP).|  
|**adDecimal**|14|Indica um valor numérico exato com uma precisão e escala fixas (DBTYPE_DECIMAL).|  
|**adDouble**|5|Indica um valor de ponto flutuante de precisão dupla (DBTYPE_R8).|  
|**adEmpty**|0|Não especifica nenhum valor (DBTYPE_EMPTY).|  
|**adError**|10|Indica um código de erro de 32 bits (DBTYPE_ERROR).|  
|**adFileTime**|64|Indica um valor de 64 bits que representa o número de intervalos de 100 nanossegundos desde 1 de janeiro de 1601 (DBTYPE_FILETIME).|  
|**adGUID**|72|Indica um identificador global exclusivo (GUID) (DBTYPE_GUID).|  
|**adIDispatch**|9|Indica um ponteiro para um **IDispatch** interface em um objeto COM (DBTYPE_IDISPATCH).<br /><br /> **Observação** esse tipo de dados não tem suporte atualmente pelo ADO. Uso pode causar resultados imprevisíveis.|  
|**adInteger**|3|Indica um inteiro com sinal de quatro bytes (DBTYPE_I4).|  
|**adIUnknown**|13|Indica um ponteiro para um **IUnknown** interface em um objeto COM (DBTYPE_IUNKNOWN).<br /><br /> **Observação** esse tipo de dados não tem suporte atualmente pelo ADO. Uso pode causar resultados imprevisíveis.|  
|**adLongVarBinary**|205|Indica um valor binário longo.|  
|**adLongVarChar**|201|Indica um valor de cadeia de caracteres longa.|  
|**adLongVarWChar**|203|Indica um valor de cadeia de caracteres Unicode longa terminada em nulo.|  
|**adNumeric**|131|Indica um valor numérico exato com uma precisão e escala fixas (DBTYPE_NUMERIC).|  
|**adPropVariant**|138|Indica uma automação PROPVARIANT (DBTYPE_PROP_VARIANT).|  
|**adSingle**|4|Indica um valor de ponto flutuante de precisão simples (DBTYPE_R4).|  
|**adSmallInt**|2|Indica um inteiro com sinal de dois bytes (DBTYPE_I2).|  
|**adTinyInt**|16|Indica um inteiro com sinal de um byte (DBTYPE_I1).|  
|**adUnsignedBigInt**|21|Indica um inteiro sem sinal de oito bytes (DBTYPE_UI8).|  
|**adUnsignedInt**|19|Indica um inteiro sem sinal de quatro bytes (DBTYPE_UI4).|  
|**adUnsignedSmallInt**|18|Indica um inteiro sem sinal de dois bytes (DBTYPE_UI2).|  
|**adUnsignedTinyInt**|17|Indica um inteiro sem sinal de um byte (DBTYPE_UI1).|  
|**adUserDefined**|132|Indica uma variável definida pelo usuário (DBTYPE_UDT).|  
|**adVarBinary**|204|Indica um valor binário.|  
|**adVarChar**|200|Indica um valor de cadeia de caracteres.|  
|**adVariant**|12|Indica um objeto de automação **Variant** (DBTYPE_VARIANT).<br /><br /> **Observação** esse tipo de dados não tem suporte atualmente pelo ADO. Uso pode causar resultados imprevisíveis.|  
|**adVarNumeric**|139|Indica um valor numérico.|  
|**adVarWChar**|202|Indica uma cadeia de caracteres Unicode terminada em nulo.|  
|**adWChar**|130|Indica uma cadeia de caracteres do Unicode de terminada em nulo (DBTYPE_WSTR).|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.DataType.ARRAY|  
|AdoEnums.DataType.BIGINT|  
|AdoEnums.DataType.BINARY|  
|AdoEnums.DataType.BOOLEAN|  
|AdoEnums.DataType.BSTR|  
|AdoEnums.DataType.CHAPTER|  
|AdoEnums.DataType.CHAR|  
|AdoEnums.DataType.CURRENCY|  
|AdoEnums.DataType.DATE|  
|AdoEnums.DataType.DBDATE|  
|AdoEnums.DataType.DBTIME|  
|AdoEnums.DataType.DBTIMESTAMP|  
|AdoEnums.DataType.DECIMAL|  
|AdoEnums.DataType.DOUBLE|  
|AdoEnums.DataType.EMPTY|  
|AdoEnums.DataType.ERROR|  
|AdoEnums.DataType.FILETIME|  
|AdoEnums.DataType.GUID|  
|AdoEnums.DataType.IDISPATCH|  
|AdoEnums.DataType.INTEGER|  
|AdoEnums.DataType.IUNKNOWN|  
|AdoEnums.DataType.LONGVARBINARY|  
|AdoEnums.DataType.LONGVARCHAR|  
|AdoEnums.DataType.LONGVARWCHAR|  
|AdoEnums.DataType.NUMERIC|  
|AdoEnums.DataType.PROPVARIANT|  
|AdoEnums.DataType.SINGLE|  
|AdoEnums.DataType.SMALLINT|  
|AdoEnums.DataType.TINYINT|  
|AdoEnums.DataType.UNSIGNEDBIGINT|  
|AdoEnums.DataType.UNSIGNEDINT|  
|AdoEnums.DataType.UNSIGNEDSMALLINT|  
|AdoEnums.DataType.UNSIGNEDTINYINT|  
|AdoEnums.DataType.USERDEFINED|  
|AdoEnums.DataType.VARBINARY|  
|AdoEnums.DataType.VARCHAR|  
|AdoEnums.DataType.VARIANT|  
|AdoEnums.DataType.VARNUMERIC|  
|AdoEnums.DataType.VARWCHAR|  
|AdoEnums.DataType.WCHAR|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|  
|[Método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|[Propriedade Type (ADO)](../../../ado/reference/ado-api/type-property-ado.md)|
