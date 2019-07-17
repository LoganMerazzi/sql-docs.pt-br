---
title: sp_OAGetProperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetProperty_TSQL
- sp_OAGetProperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetProperty
ms.assetid: 240eeeb9-6d8b-4930-b912-1d273ca0ab38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6efc0b620dcec300b5342ea5a0f63358fcdfadc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107886"
---
# <a name="spoagetproperty-transact-sql"></a>sp_OAGetProperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Obtém um valor de propriedade de um objeto OLE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_OAGetProperty objecttoken , propertyname   
    [ , propertyvalue OUTPUT ]  
    [ , index...]   
```  
  
## <a name="arguments"></a>Argumentos  
 *objecttoken*  
 É o token de objeto de um objeto OLE que foi criado anteriormente usando **sp_OACreate**.  
  
 *propertyname*  
 É o nome de propriedade do objeto OLE a ser retornado.  
  
 *PropertyValue* **saída**  
 É o valor de propriedade retornado. Se for especificado, deverá ser uma variável local do tipo de dados apropriado.  
  
 Se a propriedade retorna um objeto OLE, *propertyvalue* deve ser uma variável local de tipo de dados **int**. Um token de objeto é armazenado na variável local, e esse token de objeto pode ser usado com outros procedimentos armazenados de automação OLE.  
  
 Se a propriedade retornar um único valor, especifique uma variável local para *propertyvalue*, que retorna a propriedade de valor na variável local; ou não especificar *propertyvalue*, que retorna o valor da propriedade para o cliente como um conjunto de resultados de coluna única e uma linha.  
  
 Quando a propriedade retorna uma matriz, se *propertyvalue* for especificado, ele é definido como NULL.  
  
 Se *propertyvalue* for especificado, mas a propriedade não retorna um valor, ocorrerá um erro. Se a propriedade retornar uma matriz com mais de duas dimensões, ocorrerá um erro.  
  
 *index*  
 É um parâmetro de índice. Se especificado, *índice* deve ser um valor de tipo de dados apropriado.  
  
 Algumas propriedades têm parâmetros. Estas propriedades são chamadas de propriedades indexadas e os parâmetros são chamados de parâmetros de índice. Uma propriedade pode ter vários parâmetros de índice.  
  
> [!NOTE]  
>  Os parâmetros deste procedimento armazenado são especificados por posição, não por nome.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha) que é o valor inteiro do HRESULT retornado pelo objeto de Automação OLE.  
  
 Para obter mais informações sobre códigos de retorno HRESULT, consulte [OLE automação códigos de retorno e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se a propriedade retornar uma matriz com uma ou duas dimensões, a matriz será retornada ao cliente como um conjunto de resultados:  
  
-   Uma matriz unidimensional é retornada ao cliente como um conjunto de resultados de uma linha, com tantas colunas quanto houver elementos na matriz. Em outras palavras, a matriz é retornada como colunas.  
  
-   Uma matriz bidimensional é retornada ao cliente como um conjunto de resultados com tantas colunas quanto houver elementos na primeira dimensão da matriz e com tantas linhas quanto houver elementos na segunda dimensão da matriz. Em outras palavras, a matriz é retornada como (colunas, linhas).  
  
 Quando o valor de retorno de uma propriedade ou valor de retorno de método é uma matriz **sp_OAGetProperty** ou **sp_OAMethod** retorna um conjunto de resultados para o cliente. (Os parâmetros de saída de método não podem ser matrizes.) Esses procedimentos examinam todos os valores de dados na matriz para determinar os tipos de dados apropriados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os tamanhos dos dados a serem usados para cada coluna no conjunto de resultados. Para uma coluna específica, esses procedimentos usam o tipo de dados e o tamanho necessários para representar todos os valores de dados nesta coluna.  
  
 Quando todos os valores de dados em uma coluna compartilharem o mesmo tipo de dados, esse tipo de dados será usado para a coluna inteira. Quando os valores de dados em uma coluna forem de tipos de dados diferentes, o tipo de dados da coluna inteira será escolhido com base no quadro a seguir.  
  
||int|float|money|datetime|varchar|NVARCHAR|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>Comentários  
 Você também pode usar **sp_OAMethod** para obter um valor da propriedade.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **sysadmin** função de servidor fixa ou permissão de execução diretamente nesse procedimento armazenado. `Ole Automation Procedures` configuração deve estar **habilitado** usar qualquer procedimento de sistema relacionado à automação OLE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-local-variable"></a>A. Usando uma variável local  
 O exemplo a seguir obtém a `HostName` propriedade (da criado anteriormente **SQLServer** objeto) e o armazena em uma variável local.  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAGetProperty @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END  
PRINT @property;  
```  
  
### <a name="b-using-a-result-set"></a>B. Usando um conjunto de resultados  
 O exemplo a seguir obtém a `HostName` propriedade (da criado anteriormente **SQLServer** objeto) e retorna-o para o cliente como um conjunto de resultados.  
  
```  
EXEC @hr = sp_OAGetProperty @object, 'HostName';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Consulte também  
 [OLE procedimentos armazenados de automação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script de exemplo de automação](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
