---
title: O que é o ODBC? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc9c7a3d9f75e1863d90b16986234e0036229d01
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714088"
---
# <a name="what-is-odbc"></a>O que é o ODBC?
Existem muitos erros de concepção sobre ODBC no mundo da informática. Para o usuário final, ele é um ícone no painel de controle do Microsoft® Windows®. Para o programador de aplicativo, é uma biblioteca que contém as rotinas de acesso de dados. Para muitos outros, é a resposta para todos os problemas de acesso de banco de dados nunca tenha imaginado.  
  
 Primeiramente, o ODBC é uma especificação para um banco de dados de API. Essa API é independente de qualquer um DBMS ou sistema operacional. Embora esse manual usa C, a API de ODBC é independente de linguagem. A API de ODBC é baseada nas especificações do Open Group e ISO/IEC CLI. ODBC 3. *x* totalmente implementa ambas essas especificações - versões anteriores do ODBC eram baseadas em versões anteriores dessas especificações, mas não os implementou totalmente - e adiciona recursos comumente necessários por desenvolvedores de baseada em telas aplicativos de banco de dados, como cursores roláveis.  
  
 As funções na API do ODBC são implementadas pelos desenvolvedores de drivers específicos de DBMS. Aplicativos chamam as funções desses drivers para acessar dados de maneira independente do DBMS. Um Gerenciador de Driver gerencia a comunicação entre aplicativos e drivers.  
  
 Embora a Microsoft fornece um Gerenciador de driver para computadores que executam o Microsoft Windows® 95 e posterior, escreveu vários drivers ODBC e chama funções ODBC de alguns de seus aplicativos, qualquer pessoa pode escrever drivers e aplicativos de ODBC. Na verdade, a grande maioria dos aplicativos ODBC e drivers disponíveis hoje são escritos por empresas diferentes da Microsoft. Além disso, aplicativos e drivers ODBC existem a Macintosh® em uma variedade de plataformas UNIX.  
  
 Para ajudar os desenvolvedores de aplicativos e drivers, a Microsoft oferece um ODBC Software Development Kit (SDK) para computadores que executam o Windows 95 e posterior que fornece o Gerenciador de driver, DLL do instalador, as ferramentas de teste e aplicativos de exemplo. A Microsoft tem se com o Visigenic Software portar esses SDKs para Macintosh e uma variedade de plataformas UNIX.  
  
 É importante entender que o ODBC é projetada para expor recursos de banco de dados, não suplemento-los. Assim, os criadores de aplicativo não devem esperar que usando o ODBC será, de repente, transformar um banco de dados simple em um mecanismo de banco de dados relacional com recursos completos. Nem gravadores de driver devem implementar a funcionalidade não encontrada no banco de dados subjacente. Uma exceção a isso é que os desenvolvedores que escrevem os drivers que acessam diretamente os dados de arquivo (como os dados em um arquivo Xbase) são necessárias para escrever um mecanismo de banco de dados que dá suporte a pelo menos mínimo de funcionalidade SQL. Outra exceção é que o componente ODBC do SDK do Windows, anteriormente incluídas no Microsoft Data Access Components (MDAC) do SDK, fornece uma biblioteca de cursor que simula cursores roláveis para drivers que implementam um certo nível de funcionalidade.  
  
 Aplicativos que usam ODBC são responsáveis por qualquer funcionalidade entre bancos de dados. Por exemplo, o ODBC não é um mecanismo de junção heterogêneo, nem é um processador de transação distribuída. No entanto, porque ele é independente de DBMS, ele pode ser usado para compilar tais ferramentas de banco de dados.
