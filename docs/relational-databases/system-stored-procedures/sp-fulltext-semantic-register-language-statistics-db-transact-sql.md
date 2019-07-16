---
title: sp_fulltext_semantic_register_language_statistics_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_register_language_statistics_db
- sp_fulltext_semantic_register_language_statistics_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_register_language_statistics_db
ms.assetid: bef1b104-5a44-4327-9ae4-45eae3000f7e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 59cf70574a73827887542221f556e65e46090395
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124211"
---
# <a name="spfulltextsemanticregisterlanguagestatisticsdb-transact-sql"></a>sp_fulltext_semantic_register_language_statistics_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra um banco de dados de Estatísticas Semânticas de Idioma previamente preenchido na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 É possível iniciar a extração semântica apenas depois de anexar este banco de dados de estatísticas de idioma e de registrá-lo com este procedimento armazenado. É necessário executar essa tarefa apenas uma vez para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db  
    [ @dbname = ] 'database_name';  
GO  
```  
  
##  <a name="Arguments"></a> Argumentos  
 [ @dbname = ] '*database_name*'  
 É o nome do banco de dados de Estatísticas de Idioma Semântico a ser registrado para a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O banco de dados já deve estar anexado. *Database_Name* está **sysname**, e não pode ser NULL.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-set"></a>Conjunto de resultados  
 nenhuma.  
  
## <a name="general-remarks"></a>Comentários gerais  
 O banco de dados de Estatísticas de Idioma Semântico contém estatísticas relacionadas a idioma que são necessárias para processamento semântico de conteúdo textual.  
  
 **sp_fulltext_semantic_register_language_statistics_db** executa as seguintes etapas:  
  
1.  Verifica se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é uma versão que dá suporte ao processamento semântico.  
  
2.  Verifica se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] já não tem um banco de dados de Estatísticas de Idioma Semântico definido.  
  
3.  Verifica se o banco de dados é um banco de dados de Estatísticas de Idioma Semântico válido.  
  
4.  Define as permissões no banco de dados de Estatísticas de Idioma Semântico para restringir o acesso ao banco de dados pelos usuários.  
  
5.  Insere os metadados que definem o nome do banco de dados de Estatísticas de Idioma Semântico para a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
6.  Insere os metadados que definem os mapeamentos entre o banco de dados de Estatísticas de Idioma Semântico instalado e as tabelas do Modelo do Idioma.  
  
7.  Verifica se o banco de dados está pronto para uso.  
  
 Para obter mais informações, veja [Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre o banco de dados de estatísticas semânticas de idioma instalado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte a exibição do catálogo [sys. fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer as permissões CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como registrar o banco de dados de estatísticas semânticas de idioma, chamando **sp_fulltext_semantic_register_language_statistics_db**.  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = 'semanticsDb';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instalar e configurar a pesquisa semântica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
