---
title: Configurando opções programaticamente para drivers do Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 658d03469e2733b0c25513a4d4a89c6ab88b9852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063510"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Configurar opções programaticamente para drivers do Paradox

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Diretório|Define o diretório de destino.|Para definir essa opção dinamicamente, use o **DEFAULTDIR** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Sequência de agrupamento|A sequência na qual os campos são classificados.<br /><br /> A sequência pode ser ASCII (o padrão), internacionais, finlandês-sueco ou dinamarquês-norueguês.|Para definir essa opção dinamicamente, use o **COLLATINGSEQUENCE** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; Por exemplo, "data de contratação, histórico de salário e análise atual de todos os funcionários."|Para definir essa opção dinamicamente, use o **descrição** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusive|Se o **exclusivo** caixa é selecionada, o banco de dados será aberto no modo exclusivo e pode ser acessado somente por um usuário por vez. O desempenho é aprimorado quando em execução em modo exclusivo.|Para definir essa opção dinamicamente, use o **exclusivos** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Estilo da rede|O estilo de acesso de rede a ser usado ao acessar dados Paradox: qualquer um dos "3.*x*" para Paradox 3. *x* ou "4. *x*"para Paradox 4. *x* ou 5. *x*. Pode ser definido como "3. *x*"ou" 4. *x*"se a versão for Paradox 4. *x* ou 5. *x*; se a versão for Paradox 3. *x*, o estilo deve ser "3. *x*".|Para definir essa opção dinamicamente, use o **PARADOXNETSTYLE** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Tempo limite da página|Especifica o período de tempo, em décimos de segundo, que uma página (se não usado) permanece no buffer antes de serem removidos. O padrão é 600 décimos de segundo (60 segundos). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo limite da página não pode ser 0 devido a um atraso inerente. O tempo limite da página não pode ser menor que o atraso inerente, mesmo se a opção de tempo limite da página é definida abaixo desse valor.|Para definir essa opção dinamicamente, use o **PAGETIMEOUT** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Somente Leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use o **READONLY** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selecionar diretório|Exibe uma caixa de diálogo onde você pode selecionar um diretório que contém os arquivos que você deseja acessar.<br /><br /> Quando a definição de um diretório de origem de dados especifica o diretório em que os comumente usados mais arquivos estão localizados. O driver ODBC usa esse diretório como o diretório padrão. Copie outros arquivos nesse diretório, se eles forem usados com frequência. Como alternativa, você pode qualificar nomes de arquivo em uma instrução SELECT com o nome do diretório:<br /><br /> SELECIONE \* DE C:\MYDIR\EMP<br /><br /> Ou, você pode especificar um novo diretório padrão usando o **SQLSetConnectOption** função com a opção SQL_CURRENT_QUALIFIER.|Para definir essa opção dinamicamente, use o **DEFAULTDIR** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Selecione o diretório de rede|O caminho completo do diretório que contém um banco de dados de bloqueio do Paradox, porque ela contém o arquivo Pdoxusrs.net (no Paradox 4. *x*) ou o arquivo Paradox.net (no Paradox 5. *x*). Se o diretório não contiver um desses arquivos, o driver do Paradox criará um. Para obter informações sobre esses arquivos, consulte a documentação do Paradox.<br /><br /> Antes de selecionar um diretório de rede, você deve inserir seu nome de usuário do Paradox na **nome de usuário** caixa de texto. Clique em **selecione o diretório de rede** para selecionar um diretório de rede.|Para definir essa opção dinamicamente, use o **PARADOXNETPATH** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nome do Usuário|O nome de usuário do Paradox. Isso é o nome exibido para outros usuários de arquivos do Paradox quando um bloqueio for encontrado.|Para definir essa opção dinamicamente, use o **PARADOXUSERNAME** palavra-chave em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
