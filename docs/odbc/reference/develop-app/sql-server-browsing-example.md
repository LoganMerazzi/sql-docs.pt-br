---
title: Exemplo de navegação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f3a7568c0849844526ef5f172bcecc0a5857268
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114325"
---
# <a name="sql-server-browsing-example"></a>Exemplo de navegação do SQL Server
A exemplo a seguir mostra como **SQLBrowseConnect** pode ser usado para procurar as conexões disponíveis com um driver para SQL Server. Primeiro, o aplicativo solicita um identificador de conexão:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 Em seguida, o aplicativo chama **SQLBrowseConnect** e especifica o driver do SQL Server, usando a descrição do driver retornada por **SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Como esta é a primeira chamada para **SQLBrowseConnect**, o Gerenciador de Driver carrega o driver do SQL Server e chama o driver **SQLBrowseConnect** função com os mesmos argumentos que ele recebeu das aplicativo.  
  
> [!NOTE]  
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, você deve especificar `Trusted_Connection=yes` em vez de informações de ID e a senha do usuário na cadeia de conexão.  
  
 O driver determina que essa é a primeira chamada para **SQLBrowseConnect** e retorna o segundo nível de atributos de conexão: servidor, nome de usuário, senha, nome do aplicativo e ID da estação de trabalho. Para o atributo de servidor, ele retorna uma lista de nomes de servidor válido. O código de retorno **SQLBrowseConnect** é SQL_NEED_DATA. Aqui está a cadeia de caracteres de resultado de procurar:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 Cada palavra-chave na cadeia de caracteres de resultado da navegação é seguido por dois-pontos e uma ou mais palavras antes do sinal de igual. Essas palavras são o nome amigável que um aplicativo pode usar para criar uma caixa de diálogo. O **APP** e **WSID** palavras-chave são prefixadas por um asterisco, o que significa que eles são opcionais. O **SERVER**, **UID**, e **PWD** palavras-chave não são prefixadas por um asterisco; valores deverão ser fornecidos para eles na cadeia de caracteres de solicitação de procurar próximo. O valor para o **SERVER** palavra-chave pode ser um dos servidores retornados por **SQLBrowseConnect** ou um nome fornecido pelo usuário.  
  
 O aplicativo chama **SQLBrowseConnect** novamente, especificando o servidor de verde e omitindo a **APP** e **WSID** palavras-chave e os nomes amigáveis de usuário depois de cada palavra-chave:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 O driver tenta se conectar ao servidor verde. Se houver erros não fatais, como um par de valor de palavra-chave ausente, **SQLBrowseConnect** retornará SQL_NEED_DATA e permanece no mesmo estado, como era antes do erro. O aplicativo pode chamar **SQLGetDiagField** ou **SQLGetDiagRec** para determinar o erro. Se a conexão for bem-sucedida, o driver retorna SQL_NEED_DATA e retorna a cadeia de caracteres de resultado de procurar:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 Como os atributos desta cadeia de caracteres são opcionais, o aplicativo pode omiti-los. No entanto, o aplicativo deve chamar **SQLBrowseConnect** novamente. Se o aplicativo optar por omitir o nome do banco de dados e o idioma, ele especifica uma cadeia de caracteres de solicitação de navegação vazia. Neste exemplo, o aplicativo escolhe o banco de dados pubs e chama **SQLBrowseConnect** uma última vez, omitindo o **idioma** palavra-chave e o asterisco antes do **banco de dados**palavra-chave:  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 Porque o **banco de dados** é o atributo de conexão final exigido pelo driver, o processo de localização estiver concluído, o aplicativo está conectado à fonte de dados, e **SQLBrowseConnect** Retorna SQL_SUCCESS. **SQLBrowseConnect** também retorna a cadeia de conexão completa como a cadeia de caracteres de resultado de procurar:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 A cadeia de caracteres de final de conexão retornada pelo driver não contém os nomes amigáveis de usuário depois de cada palavra-chave, nem que ele contém palavras-chave opcional não é especificadas pelo aplicativo. O aplicativo pode usar essa cadeia de caracteres com **SQLDriverConnect** para reconectar-se à fonte de dados no identificador da conexão atual (após a desconexão) ou se conectar à fonte de dados em um identificador de conexão diferentes. Por exemplo:  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
