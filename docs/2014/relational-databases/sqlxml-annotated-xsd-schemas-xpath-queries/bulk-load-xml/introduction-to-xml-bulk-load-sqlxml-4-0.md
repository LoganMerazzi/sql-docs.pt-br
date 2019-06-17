---
title: Introdução ao XML Bulk Load (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nontransacted XML Bulk Load operations
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
- transacted XML Bulk Load operations
- streaming XML data
ms.assetid: 38bd3cbd-65ef-4c23-9ef3-e70ecf6bb88a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d257b6eee1fb3adc0ba611f58a1d5eea5adf3f86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013387"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>Introdução ao XML Bulk Load (SQLXML 4.0)
  XML Bulk Load é um objeto COM autônomo que permite que você carregar dados XML semiestruturados em Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabelas.  
  
 Você pode inserir dados XML em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando um comando INSERT e a função OPENXML; no entanto, o utilitário Bulk Load garante um melhor desempenho quando você precisa inserir grandes quantidades de dados XML.  
  
 O método Execute do modelo de objeto do XML Bulk Load usa dois parâmetros:  
  
-   Um esquema XSD (XML Schema Definition) anotado ou esquema XDR (XML-Data Reduced). O utilitário XML Bulk Load interpreta esse esquema de mapeamento e as anotações especificadas no esquema ao identificar as tabelas do SQL Server nas quais os dados XML serão inseridos.  
  
-   Um documento XML ou fragmento de documento (um documento sem elementos de alto nível). É possível especificar um nome de arquivo ou um fluxo do qual o XML Bulk Load pode ler.  
  
 O XML Bulk Load interpreta o esquema de mapeamento e identifica a tabela na qual os dados XML serão inseridos.  
  
 Pressupõe-se que você esteja familiarizado com os seguintes recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Esquemas XSD e XDR anotados. Para obter mais informações sobre esquemas XSD anotados, consulte [Introdução aos esquemas XSD anotados &#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Para obter informações sobre esquemas XDR anotados, consulte [esquemas XDR anotados &#40;substituídos no SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
-   Os mecanismos de inserção em massa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], como a instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]BULK INSERT e o utilitário bcp. Para obter mais informações, consulte [BULK INSERT &#40;Transact-SQL&#41; ](/sql/t-sql/statements/bulk-insert-transact-sql) e [utilitário bcp](../../../tools/bcp-utility.md).  
  
## <a name="streaming-of-xml-data"></a>Fluindo de dados XML  
 Como o documento XML de origem pode ser grande, ele não é lido na memória para o processamento do carregamento em massa. Em vez disso, o XML Bulk Load interpreta os dados XML como um fluxo e faz a leitura deles. À medida que o utilitário lê os dados, ele identifica a(s) tabela(s) de banco de dados, gera o(s) registro(s) apropriado(s) a partir da fonte de dados XML e envia o(s) registro(s) para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para inserção.  
  
 Por exemplo, o seguinte documento XML de origem consiste  **\<cliente >** elementos e  **\<Order >** elementos filho:  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 Como o XML Bulk Load lê o  **\<cliente >** elemento, ele gera um registro para o Customertable. Quando ele lê a  **\</Customer >** marca, o XML Bulk Load insere esse registro na tabela no final [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Da mesma forma, quando ele lê a  **\<ordem >** elemento, XML Bulk Load gera um registro para o Ordertable e, em seguida, insere esse registro para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabela após a leitura a  **\< / Order >** marca de fim.  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>Operações de carregamento em massa de XML transacionadas e não transacionadas  
 O XML Bulk Load pode operar no modo transacionado ou não transacionado. O desempenho é geralmente melhor se você estiver carregando em massa em um modo não transacionado: ou seja, a propriedade de transação é definida como FALSE) e qualquer uma das seguintes condições for verdadeira:  
  
-   As tabelas nas quais os dados são carregados em massa são vazias e não têm índices.  
  
-   As tabelas têm dados e índices exclusivos.  
  
 A abordagem não transacionada não garante uma reversão se algo de errado acontecer no processo de carregamento em massa (embora reversões parciais possam ser feitas). O carregamento em massa não transacionado é apropriado quando o banco de dados está vazio. Portanto, se algo der errado, você poderá limpar o banco de dados e iniciar o XML Bulk Load novamente.  
  
> [!NOTE]  
>  No modo não transacionado, o XML Bulk Load usa uma transação interna padrão e a confirma. Quando a propriedade de transação é definida como TRUE, o XML Bulk Load não chama a confirmação nesta transação.  
  
 Se a propriedade de transação é definida como TRUE, o XML Bulk Load cria arquivos temporários, uma para cada tabela que é identificada no esquema de mapeamento. O XML Bulk Load primeiro armazena os registros do documento XML de origem nesses arquivos temporários. Em seguida, uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT recupera esses registros dos arquivos e os armazena nas tabelas correspondentes. Você pode especificar o local para esses arquivos temporários, usando a propriedade TempFilePath. Você deve assegurar que a conta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usada com o XML Bulk Load tenha acesso a esse caminho. Se a propriedade TempFilePath não for especificada, o caminho do arquivo padrão que é especificado na variável de ambiente TEMP é usado para criar os arquivos temporários.  
  
 Se a propriedade de transação é definida como FALSE (a configuração padrão), o XML Bulk Load usa a interface de OLE DB IRowsetFastLoad para carregamento em massa os dados.  
  
 Se a propriedade ConnectionString define a cadeia de conexão e a propriedade de transação é definida como TRUE, o XML Bulk Load opera em seu próprio contexto de transação. (Por exemplo, o XML Bulk Load inicia sua própria transação e confirma ou reverte conforme apropriado.)  
  
 Se a propriedade ConnectionCommand define a conexão com um objeto de conexão existente e a propriedade de transação é definida como TRUE, o XML Bulk Load não emite uma instrução COMMIT ou ROLLBACK no caso de sucesso ou falha, respectivamente. Caso haja um erro, o XML Bulk Load retornará a mensagem de erro apropriada. A decisão de executar uma instrução COMMIT ou ROLLBACK fica a cargo do cliente que iniciou o carregamento em massa. O objeto de conexão que é usado para o XML Bulk Load deve ser do tipo ICommand ou ser um objeto de comando ADO.  
  
 No SQLXML 4.0, um ConnectionObject não pode ser usado com a propriedade de transação definida como FALSE. Não há suporte para o modo não transacionado com um ConnectionObject porque é impossível abrir mais de uma interface IRowsetFastLoad em uma sessão passada.  
  
  
