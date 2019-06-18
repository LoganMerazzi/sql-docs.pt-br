---
title: Bibliotecas de Conexão para bancos de dados do Microsoft SQL | Microsoft Docs
description: Fornece links de download para módulos que permitem a conexão ao Microsoft SQL Server e banco de dados SQL Azure, de uma variedade de linguagens de programação do cliente.
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 7f759dbe9022cff557461d900a35b3ccc91d2c4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62862406"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Módulos de Conexão para bancos de dados SQL do Microsoft

Este artigo fornece links de download para os módulos de conexão ou *drivers* que seus programas cliente podem usar para interagir com [Microsoft SQL Server](../relational-databases/database-features.md)e com seu gêmeo na nuvem [Azure Banco de dados SQL](https://docs.microsoft.com/azure/sql-database/). Drivers estão disponíveis para uma variedade de linguagens de programação, em execução em sistemas operacionais a seguir:

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>Incompatibilidade de OOP para relacional

*Relacional*: os programas de cliente que são escritos em uma linguagem de (OOP) programação orientada a objeto geralmente usam drivers do SQL que retornam dados consultados em um formato que seja mais relacional que orientada a objeto. Em C# usando o ADO.NET é um exemplo. A incompatibilidade de formato relacional de OOP, às vezes, torna o código OOP mais difícil de escrever e entender.

*ORM*: outros drivers ou estruturas de retornam dados consultados no formato OOP, evitando a incompatibilidade. Esses drivers trabalhar, esperando que as classes foram definidas de acordo com as colunas de dados de determinadas tabelas SQL. O driver, em seguida, executa o *mapeamento relacional de objeto* (ORM) para retornar dados consultados como uma instância de uma classe. Entity Framework (EF da Microsoft) para c# e Hibernar para Java, são dois exemplos.

O presente artigo dedica seções separadas para esses dois tipos de drivers de conexão.

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>Drivers para acesso relacional


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| Linguagem | Baixar o driver do SQL |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br /><br />[.NET Core para Linux-Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET core para MacOS](https://www.microsoft.com/net/core#macos)<br />[.NET core para Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Driver do Node. js, instruções de instalação](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, instruções de instalação](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[Baixar o ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Driver Ruby, instruções de instalação](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Página de download do Ruby](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>Drivers para acesso ORM


A tabela a seguir lista exemplos de estruturas de objeto ORM (mapeamento relacional) que aplicativos cliente usam para se conectar a bancos de dados SQL do Microsoft.


| Linguagem | Download do driver ORM |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6. x ou posterior)](https://docs.microsoft.com/ef/) |
| Java | [Hibernar ORM](https://hibernate.org/orm)|
| PHP | [Com eloquência o ORM, incluído na instalação do Laravel](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Páginas de compilação um aplicativo da Web
[https://aka.ms/sqldev](https://aka.ms/sqldev) leva você para um conjunto de *Build um aplicativo* páginas da Web. As páginas da Web fornecem informações sobre várias combinações de idioma, o sistema operacional e o driver de conexão SQL de programação. Entre as informações fornecidas pelo Build um aplicativo páginas da Web são os seguintes itens:

- Detalhes sobre como começar desde o início, para cada combinação de idioma, o sistema operacional + o driver.
    - Instruções para instalar os drivers mais recentes de conexão SQL.
- Exemplos de código para cada um dos seguintes itens:
    - Exemplos de código de objeto relacional.
    - Exemplos de código ORM.
    - Demonstrações do índice ColumnStore para um desempenho muito mais rápido.

#### <a name="first-page-of-build-an-app-webpages"></a>Primeira página das páginas de compilação um aplicativo da Web
![Construir um aplicativo páginas da Web, primeira captura de tela da página][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Menu para Java - Ubuntu de páginas de compilação um aplicativo da Web
![Construir um aplicativo páginas da Web, menu Ubuntu de Java][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>Links relacionados
- [Exemplos de código de se conectar ao banco de dados SQL Azure na nuvem, com Java e outras linguagens](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java).

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
