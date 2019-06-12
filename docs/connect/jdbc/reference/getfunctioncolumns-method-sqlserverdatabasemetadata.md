---
title: Método getFunctionColumns (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e2b0e0f7-717c-48e6-bcd2-a325d938a833
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cd4958db78e2e35d29bcc47428295db50f7e5678
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66774625"
---
# <a name="getfunctioncolumns-method-sqlserverdatabasemetadata"></a>Método getFunctionColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma descrição do sistema do catálogo especificado - ou parâmetros de função do usuário e tipo de retorno.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public ResultSet getFunctionColumns(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern  
                       java.lang.String columnNamePattern)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *catalog*  
  
 Uma **String** que contém o nome do catálogo. Se for uma cadeia de caracteres vazia "", o resultado incluirá as funções sem um catálogo. Se for **null**, o nome do catálogo não será usado para pesquisa.  
  
 *schemaPattern*  
  
 Uma **String** que contém o padrão de nome do esquema. Se for uma cadeia de caracteres vazia "", o resultado incluirá as funções sem um esquema. Se for **null**, o nome do esquema não será usado para pesquisa.  
  
 *functionNamePattern*  
  
 Uma **String** que contém o nome de uma função.  
  
 *columnNamePattern*  
  
 Uma **String** que contém o nome de um parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getColumns é especificado pelo método getColumns na interface java.sql.DatabaseMetaData.  
  
 Esse método retorna apenas as funções e os parâmetros correspondentes ao nome do esquema e da função especificados, além do nome do parâmetro dentro do catálogo especificado.  
  
 Todas as linhas do conjunto de resultados incluem as seguintes colunas para uma descrição de parâmetro, uma descrição de coluna ou um tipo de retorno:  
  
|Nome|Tipo|Descrição|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|O nome do banco de dados no qual a função reside.|  
|FUNCTION_SCHEM|**String**|O esquema da função.|  
|FUNCTION_NAME|**String**|O nome da função.|  
|COLUMN_NAME|**String**|O nome de um parâmetro ou coluna.|  
|COLUMN_TYPE|**short**|**O tipo da coluna. Pode ser um dos seguintes valores:**<br /><br /> functionColumnUnknown (0): Tipo desconhecido.<br /><br /> functionColumnIn (1): Parâmetro de entrada.<br /><br /> functionColumnInOut (2): Parâmetro de entrada/saída.<br /><br /> functionColumnOut (3): Parâmetro de saída.<br /><br /> functionReturn (4): Valor de retorno da função.<br /><br /> functionColumnResult (5): Um parâmetro ou uma coluna é uma coluna no conjunto de resultados.|  
|DATA_TYPE|**smallint**|O valor de tipo de dados SQL de Java.sql.Types.|  
|TYPE_NAME|**String**|O nome do tipo de dados.|  
|PRECISION|**int**|O número total de dígitos significativos.|  
|LENGTH|**int**|O comprimento dos dados em bytes.|  
|SCALE|**short**|O número de dígitos à direita da vírgula decimal.|  
|RADIX|**short**|A base para tipos numéricos.|  
|NULLABLE|**short**|Indica se o parâmetro ou o valor retornado pode conter um valor **null**.<br /><br /> **Pode ser um dos seguintes valores:**<br /><br /> functionNoNulls (0): O valor NULL não é permitido.<br /><br /> functionNullable (1): O valor NULL é permitido.<br /><br /> functionNullableUnknown (2): Desconhecido.|  
|REMARKS|**String**|Os comentários sobre uma coluna ou um parâmetro.|  
|COLUMN_DEF|**String**|O valor padrão da coluna.<br /><br /> **Observação:** essas informações estão disponíveis com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], sendo específicas do driver JDBC.|  
|SQL_DATA_TYPE|**smallint**|Esta coluna é igual à coluna **DATA_TYPE**, com exceção dos tipos de dados **datetime** e **interval** ISO.<br /><br /> **Observação:** essas informações estão disponíveis com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], sendo específicas do driver JDBC.|  
|SQL_DATETIME_SUB|**smallint**|O subcódigo de **interval** ISO de **datetime**, se o valor de **SQL_DATA_TYPE** for **SQL_DATETIME** ou **SQL_INTERVAL**. Para tipos de dados diferente de **datetime** e ISO **intervalo**, essa coluna será NULL.<br /><br /> **Observação:** essas informações estão disponíveis com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], sendo específicas do driver JDBC.|  
|CHAR_OCTET_LENGTH|**int**|O tamanho máximo dos parâmetros ou colunas binários ou baseados em caractere. Para outros tipos de dados, ele é NULL.|  
|ORDINAL_POSITION|**int**|Para parâmetros de entrada e saída, ele representa a posição começando em 1.<br /><br /> Para colunas do conjunto de resultados, é a posição da coluna no conjunto de resultados começando em 1.<br /><br /> Para o valor de retorno, é 0.|  
|IS_NULLABLE|**String**|Determina a nulidade de um parâmetro ou de uma coluna.<br /><br /> Pode ser um dos seguintes valores:<br /><br /> **Sim**: O parâmetro ou coluna pode incluir valores nulos.<br /><br /> **NÃO**: O parâmetro ou coluna não pode incluir valores nulos.<br /><br /> Cadeia de caracteres vazia (""): Desconhecida.|  
|SS_TYPE_CATALOG_NAME|**String**|O nome do catálogo que contém o UDT (tipo definido pelo usuário).|  
|SS_TYPE_SCHEMA_NAME|**String**|O nome do esquema que contém o UDT (tipo definido pelo usuário).|  
|SS_UDT_CATALOG_NAME|**String**|O UDT (tipo definido pelo usuário) do nome totalmente qualificado.|  
|SS_UDT_SCHEMA_NAME|**String**|O nome do catálogo em que é definido um nome da coleção de esquemas XML. Se não for possível localizar o nome do catálogo, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|O nome do esquema no qual é definido um nome da coleção de esquemas XML. Se não for possível localizar o nome do esquema, essa cadeia de caracteres estará vazia.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|O nome de uma coleção de esquemas XML. Se não for possível localizar o nome, essa cadeia de caracteres estará vazia.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|O nome do catálogo que contém o UDT (tipo definido pelo usuário).|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|O nome do esquema que contém o UDT (tipo definido pelo usuário).|  
|SS_DATA_TYPE|**tinyint**|O tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usado por procedimentos armazenados estendidos.<br /><br /> **Observação:** para saber mais sobre os tipos de dados retornados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], veja "Tipos de dados (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
