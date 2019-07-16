---
title: Campos de descritor para colunas constituintes do parâmetro com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3987d21f69e6dfa74a1996428dbaf337633b2abf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895523"
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>Campos descritores para colunas constituintes do parâmetro com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Os campos de descritor de parâmetro com valor de tabela descritos nesta seção são manipulados por meio [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) e [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) com o identificador para o (de descritor de parâmetro de implementação IPD).  
  
## <a name="remarks"></a>Comentários  
 SQL_DESC_AUTO_UNIQUE_VALUE é usado para parâmetros com valor de tabela, e também com outros recursos.  
  
|Nome do atributo|type|Descrição|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE indica que esta coluna é uma coluna de identidade.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar essas informações para otimizar o desempenho, mas aplicativos não são requeridos para defini-lo para colunas de identidade.|  
  
 Os seguintes atributos são adicionado a todos os tipos de parâmetros no APD (Descritor de Parâmetro de Aplicativo) e no IPD:  
  
|Nome do atributo|type|Descrição|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE indica que essa coluna é computada.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar essas informações para otimizar o desempenho, mas aplicativos não são requeridos para defini-lo para colunas computadas.<br /><br /> Este atributo é ignorado para associações que não são colunas de parâmetro com valor de tabela.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE indica que uma coluna de parâmetro com valor de tabela participa de uma chave exclusiva. Isto pode resultar em melhor desempenho de consulta. Este atributo é ignorado para associações que não são colunas de parâmetro com valor de tabela.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|Indica a ordem de classificação de uma coluna de parâmetro com valor de tabela. Isto pode resultar em melhor desempenho de consulta. Este atributo é ignorado para associações que não são colunas de parâmetro com valor de tabela. Os seguintes valores são possíveis: <br />**SQL_SS_ASCENDING_ORDER**<br />**SQL_SS_DESCENDING_ORDER**<br />**SQL_SS_ORDER_UNSPECIFIED**<br /><br /> Valores diferentes de **SQL_SS_ASCENDING_ORDER** e **SQL_SS_DESCENDING_ORDER** geram um erro com **SQLSTATE HY024** e mensagem 'valor do atributo inválido' e são considerado **SQL_SS_ORDER_UNSPECIFIED**, que é o valor padrão para este atributo.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|Indica o ordinal de uma coluna de parâmetro com valor de tabela no conjunto de colunas que definem a ordenação global para um parâmetro com valor de tabela. Isto pode resultar em melhor desempenho de consulta. Este atributo é ignorado para associações que não são colunas de parâmetro com valor de tabela. Ordinais de classificação iniciam em 1. Um valor 0, o padrão, indica que uma coluna de parâmetro com valor de tabela não tem ordenação de coluna.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|Indica se todas as linhas no parâmetro com valor de tabela terão o valor padrão para esta coluna. Para parâmetros com valor de tabela, não é possível selecionar o valor padrão em uma base linha por linha. Um valor SQL_FALSE indica que as linhas terão valores não padrão. Esse é o padrão. Um valor SQL_TRUE indica que esta coluna terá valores padrão para todas as linhas.<br /><br /> Se definido como SQL_TRUE, nenhum dos dados será enviado ao servidor.<br /><br /> Este campo também poderá ser usado com identidade ou colunas computadas se os valores de coluna não forem requeridos para processamento de servidor.|  
  
 Estes atributos só são válidos para colunas de parâmetro com valor de tabela. Eles são ignorados para outros parâmetros.  
  
 Se SQL_CA_SS_COL_HAS_DEFAULT_VALUE for definido para uma coluna de parâmetro com valor de tabela, SQL_DESC_DATA_PTR para essa coluna deverá ser um ponteiro nulo. Caso contrário, SQLExecute ou SQLExecDirect retornará SQL_ERROR. Um registro de diagnóstico será gerado com SQLSTATE = 07S01 e a mensagem "uso inválido de parâmetro padrão para o parâmetro \<p >, coluna \<c >", onde \<p > é o parâmetro ordinal e \<c > é o ordinal da coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
