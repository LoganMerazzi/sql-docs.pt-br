---
title: Alterações de comportamento em pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- behavior changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: 573444e8-51bc-4f3d-9813-0037d2e13b8f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 0d3bf42ec031415d16ea45bc8241c85c6d937c35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813189"
---
# <a name="behavior-changes-to-full-text-search"></a>Alterações de comportamento na pesquisa de texto completo
  Este tópico descreve alterações de comportamento em pesquisa de texto completo. Essas alterações afetam a maneira como os recursos funcionam ou interagem no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] em comparação com as versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>Alterações de comportamento na pesquisa de texto completo do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Informações que virão posteriormente.  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>Alterações de comportamento na pesquisa de texto completo do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 O [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] instala uma nova versão dos separadores de palavras e lematizadores para inglês dos EUA (LCID 1033) e inglês do Reino Unido (LCID 2057). Porém, você poderá alternar para a versão anterior desses componentes se desejar reter o comportamento anterior. Para obter mais informações, consulte [Alterar o separador de palavras usado para inglês (EUA) e inglês (Reino Unido)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
### <a name="new-word-breakers-and-stemmers-installed"></a>Novos separadores de palavras e lematizadores instalados  
 O [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] atualiza todos os separadores de palavras e lematizadores usados por Pesquisas de texto completo e semântico. Para obter consistência entre o conteúdo de índices e os resultados das consultas, nós recomendamos que você repopule os índices de texto completo existentes.  
  
1.  Há novos separadores de palavras para inglês. Se você tiver que manter o comportamento anterior, consulte [Alterar o separador de palavras usado para inglês (EUA) e inglês (Reino Unido)](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
2.  Separadores de palavras de terceiros para dinamarquês, polonês e turco que foram incluídos com versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] foram substituídos por componentes do [!INCLUDE[msCoName](../includes/msconame-md.md)] . Os novos componentes estão habilitados por padrão.  
  
3.  Há novos separadores de palavras para tcheco e grego. As versões anteriores de Pesquisa de Texto Completo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não incluíam suporte para estes dois idiomas.  
  
### <a name="behavior-changes-of-new-word-breakers-and-stemmers"></a>Alterações de comportamento de novos separadores de palavras e lematizadores  
 Os novos componentes podem retornar resultados diferentes dos componentes mais antigos quando você popula e consulta índices de texto completo. As tabelas a seguir demonstram algumas das diferenças que podem ser esperadas em resultados em inglês.  
  
 Se você tiver que reter o comportamento anterior dos separadores de palavras e lematizadores, consulte os tópicos seguintes:  
  
-   [Alterar o separador de palavras usado para inglês dos EUA e inglês do Reino Unido](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
-   [Reverter à versão anterior os separadores de palavras usados pela pesquisa](../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
 Em alguns casos, os novos componentes retornam *mais* resultados:  
  
|**Termo**|**Resultados com separador de palavras anterior e lematizador**|**Resultados com novo separador de palavras e lematizador**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|cat-dog|cat<br /><br /> dog|cat<br /><br /> cat-dog<br /><br /> dog|  
|cat@dog.com|cat<br /><br /> com<br /><br /> dog|cat<br /><br /> cat@dog.com<br /><br /> com<br /><br /> dog|  
|12/11/2011<br /><br /> *(onde o termo é uma data)*|12/11/2011<br /><br /> dd20111211|11<br /><br /> 12<br /><br /> 12/11/2011<br /><br /> 2011<br /><br /> dd20111211|  
  
 Em alguns casos, os novos componentes retornam resultados *semelhantes* :  
  
|**Termo**|**Resultados com separador de palavras anterior e lematizador**|**Resultados com novo separador de palavras e lematizador**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|100$|100$<br /><br /> nn100$|100$<br /><br /> nn100usd|  
|022|022<br /><br /> nn022|022<br /><br /> nn22|  
|10:49AM<br /><br /> *(onde o termo é uma hora)*|10:49AM<br /><br /> tt1049|10:49AM<br /><br /> tt24104900|  
  
 Em alguns casos, os novos componentes retornam *menos* resultados ou resultados que podem ser inesperados pelos aplicativos:  
  
|**Termo**|**Resultados com separador de palavras anterior e lematizador**|**Resultados com novo separador de palavras e lematizador**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|jěˊÿｑℭžl<br /><br /> *(em que os termos não são caracteres válidos em inglês)*|'jěˊÿｑℭžl'|je yq zl|  
|table's|table's<br /><br /> table|table's|  
|cat-|cat<br /><br /> cat-|cat|  
|v-z *(em que v e z são palavras de ruído)*|*(nenhum resultado)*|v-z|  
|$100 000 USD|$100<br /><br /> 000<br /><br /> nn000<br /><br /> nn100$<br /><br /> usd|$100 000 USD<br /><br /> nn100000usd|  
|beautiful U.S land|beautiful<br /><br /> land<br /><br /> u.s<br /><br /> us|beautiful<br /><br /> land|  
|Mt. Kent and Mt Challenger|challenger<br /><br /> kent<br /><br /> mt<br /><br /> Mt.|mt<br /><br /> kent<br /><br /> challenger|  
  
## <a name="behavior-changes-in-full-text-search-in-sql-server-2008"></a>Alterações de comportamento na pesquisa de texto completo no SQL Server 2008  
 No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versões posteriores, o mecanismo de texto completo é integrado como um serviço de banco de dados ao banco de dados relacional como parte da infraestrutura de mecanismo de consulta e o armazenamento de servidor. A nova arquitetura de pesquisa de texto completo atinge as seguintes metas:  
  
-   Armazenamento integrado e gerenciamento-Full-text search agora está integrado diretamente com os recursos de armazenamento e gerenciamento inerentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], e o serviço MSFTESQL não existe mais.  
  
    -   Os índices de texto completo são armazenados nos grupos de arquivos de banco de dados, e não no sistema de arquivos. As operações administrativas executadas em um banco de dados, como a criação de um backup, afetam automaticamente seus índices de texto completo.  
  
    -   Agora um catálogo de texto completo é um objeto virtual que não pertence a nenhum grupo de arquivos; trata-se de um conceito lógico que faz referência a um grupo de índices de texto completo. Por esse motivo, muitos recursos de gerenciamento de catálogo ficaram obsoletos e isso gerou alterações recentes em alguns recursos. Para obter mais informações, consulte [recursos do mecanismo de banco de dados preteridos no SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md) e [Breaking Changes to Full-Text Search](breaking-changes-to-full-text-search.md).  
  
        > [!NOTE]  
        >  As instruções DDL [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] do [!INCLUDE[tsql](../includes/tsql-md.md)] que especificam catálogos de texto completo funcionam corretamente.  
  
-   O processamento de consulta integrada à nova, processador de consulta pesquisa de texto completo faz parte do mecanismo de banco de dados e é totalmente integrado com o processador de consulta do SQL Server. Isso significa que o otimizador de consulta reconhece predicados de consulta de texto completo e os executa automaticamente com o máximo de eficácia possível.  
  
-   Administração aprimorada e integrada à solução de problemas de pesquisa de texto completo fornece ferramentas para ajudá-lo a analisar estruturas de pesquisa, como o índice de texto completo, a saída de um determinado separador de palavras, configuração de palavras irrelevantes e assim por diante.  
  
-   As palavras irrelevantes e as listas de palavras irrelevantes (stoplists) substituíram as palavras de ruído o os arquivos de palavras de ruído. Uma lista de palavras irrelevantes é um objeto de banco de dados que facilita as tarefas de capacidade de gerenciamento relacionadas a palavras irrelevantes e melhora a integridade entre diferentes ambientes e instâncias de servidor. Para obter mais informações, veja [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes para pesquisa de texto completo](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   O [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e versões posteriores inclui novos separadores de palavras para muitos dos idiomas existentes no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. Somente os separadores de palavras para inglês, coreano, tailandês e chinês (todas as formas) permanecem os mesmos. Para outros idiomas, se um catálogo de texto completo foi importado durante um [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] banco de dados foi atualizado para [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] ou uma versão posterior, um ou mais idiomas usados pelos índices de texto completo no catálogo de texto completo podem agora ser associados a novos separadores de palavras que comportamento pode ser ligeiramente diferente dos separadores importados. Para obter mais informações sobre como garantir a consistência entre as consultas e o conteúdo do índice de texto completo, consulte [atualizar pesquisa de texto completo](../relational-databases/search/upgrade-full-text-search.md).  
  
-   Um novo serviço Iniciador FDHOST (MSSQLFDLauncher) foi adicionado. Para obter mais informações, consulte [Introdução à pesquisa de texto completo](../relational-databases/search/get-started-with-full-text-search.md).  
  
-   Indexação de texto completo funciona com uma [FILESTREAM](../relational-databases/blob/filestream-sql-server.md) coluna da mesma maneira que faz com um `varbinary(max)` coluna. A tabela FILESTREAM deve ter uma coluna que contenha a extensão do nome do arquivo para cada BLOB FILESTREAM. Para obter mais informações, consulte [consulta com pesquisa de texto completo](../relational-databases/search/query-with-full-text-search.md),[configurar e gerenciar filtros para pesquisa](../relational-databases/search/configure-and-manage-filters-for-search.md), e [fulltext_document_types &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
     O mecanismo de texto completo indexa o conteúdo dos BLOBs FILESTREAM. Arquivos de indexação como imagens podem não ser úteis. Quando um BLOB FILESTREAM é atualizado, ele é reindexado.  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisa de Texto Completo](../relational-databases/search/full-text-search.md)   
 [Compatibilidade com versões anteriores de pesquisa de texto completo](../../2014/database-engine/full-text-search-backward-compatibility.md)   
 [Atualizar pesquisa de texto completo](../relational-databases/search/upgrade-full-text-search.md)   
 [Iniciar a pesquisa de texto completo](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
