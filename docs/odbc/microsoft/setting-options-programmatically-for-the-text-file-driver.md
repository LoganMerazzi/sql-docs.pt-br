---
title: "Opções de configuração por meio de programação para o Driver de arquivo de texto | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d5037ca7d41470a2e9f7ce342ab49b08a6af0d74
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Opções de configuração por meio de programação para o Driver de arquivo de texto
|Opção|Description|Método|  
|------------|-----------------|------------|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como folha de pagamento ou pessoal.|Para definir essa opção dinamicamente, use o **DSN** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definir o formato|Exibe o **definir formato de texto** caixa de diálogo e permite que você especifique o esquema para tabelas individuais no diretório de origem de dados.|Essa opção não pode ser definida dinamicamente por uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Description|Uma descrição opcional dos dados na fonte de dados; Por exemplo, "data de contratação, histórico de salário e análise atual de todos os funcionários."|Para definir essa opção dinamicamente, use o **descrição** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Diretório|Seleciona o diretório de destino.|Para definir essa opção dinamicamente, use o **DEFAULTDIR** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Lista de extensões|Lista as extensões de nome de arquivo dos arquivos de texto na fonte de dados. Quando o driver de texto é usado, um arquivo sem extensão é criado quando a instrução CREATE TABLE é executada com um nome que não tem extensão. Outros drivers de criar um arquivo com uma extensão padrão quando nenhuma extensão é fornecido. Para criar um arquivo com uma extensão. txt, a extensão deve ser incluída no nome. Para exibir arquivos sem extensões de **definir formato de texto** caixa de diálogo, "*." deve ser adicionado à lista de extensões.|Para definir essa opção dinamicamente, use o **extensões** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Somente Leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use o **READONLY** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Linhas de varredura|O número de linhas a serem examinadas para determinar o tipo de dados de cada coluna. O tipo de dados é determinado o número máximo de tipos de dados encontrados. Se forem encontrados dados que não coincide com o tipo de dados avaliado para a coluna, o tipo de dados será retornado como um valor nulo.<br /><br /> Para o driver de texto, você pode inserir um número de 1 a 32767 para o número de linhas a serem examinadas; No entanto, o valor padrão será sempre 25. (Um número fora do limite retornará um erro.)|Para definir essa opção dinamicamente, use o **MAXSCANROWS** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Selecione o diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório que contém os arquivos que você deseja acessar.<br /><br /> Quando a definição de um diretório de origem de dados especifica o diretório onde o mais comumente usados arquivos estão localizados. O driver ODBC usa esse diretório como o diretório padrão. Copie outros arquivos nesse diretório, se eles são usados com frequência. Como alternativa, você pode qualificar nomes de arquivo em uma instrução SELECT com o nome do diretório:`SELECT * FROM C:\MYDIR\EMP`<br /><br /> Ou, você pode especificar um novo diretório padrão usando o **SQLSetConnectOption** função com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use o **DEFAULTDIR** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|