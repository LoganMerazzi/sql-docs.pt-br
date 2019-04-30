---
title: Documentação de extensões de programação e aprendizado de máquina do R e Python – Machine Learning do SQL Server
description: R e Python no SQL Server, com a modelagem de ciência de dados interna e algoritmos de aprendizado de máquina para análise de dados corporativos em escala.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/10/2019
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 20acdf2789158bf067319930a5be65770eae67f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126828"
---
# <a name="sql-server-machine-learning"></a>Machine Learning do SQL Server

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

## <a name="sql-server-machine-learning-and-programming-extensions-documentation"></a>Documentação de extensões de programação e Machine Learning do SQL Server

Saiba como usar bibliotecas externas do R e Python e linguagens em dados relacionais residentes com nossos guias de início rápido, tutoriais e artigos de instruções. As bibliotecas de R e Python no [Machine Learning do SQL Server](what-is-sql-server-machine-learning.md) incluem distribuições de base, modelos de ciência de dados, algoritmos de aprendizado de máquina e funções para conduzir a análise de alto desempenho em escala, sem precisar transferir dados pela rede.

No SQL Server 2019, a execução de código Java usa a mesma estrutura de extensibilidade como R e Python, mas não inclui bibliotecas de função de aprendizado de máquina e de ciência de dados. Para obter mais informações sobre novos recursos, veja [Novidades nos serviços do Computador SQL Server](what-s-new-in-sql-server-machine-learning-services.md).

|   |   |
|---|:--|
| ![Logotipo do R](media/index/logo_r.png) | R de software livre, estendido com [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) e algoritmos da IA da Microsoft no [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). Essas bibliotecas fornecem modelos de previsão, análise estatística, visualização e manipulação de dados em escala.<br/>A integração do R começa no [SQL Server 2016](install/sql-r-services-windows-install.md) e também está no [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logotipo do Python](media/index/logo_python.png) | Os desenvolvedores de Python podem usar as bibliotecas [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) da Microsoft para análise preditiva e aprendizado de máquina em escala. As bibliotecas compatíveis com Anaconda e Python 3.5 são a distribuição de linha de base.<br/>A integração do Python começa no [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logotipo do Java](media/index/logo_java.png) | Os desenvolvedores de Java podem usar a [extensão da linguagem Java](java/extension-java.md) para encapsular o código em procedimentos armazenados ou em um formato binário acessível por meio do Transact-SQL.<br/>A integração do Java começa no [SQL Server 2019 – versão prévia](install/sql-machine-learning-services-ver15.md). |
| &nbsp; | &nbsp; |
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"

## <a name="sql-server-machine-learning-r-and-python-documentation"></a>Documentação de Python e R do Machine Learning do SQL Server

Saiba como usar bibliotecas externas do R e Python e linguagens em dados relacionais residentes com nossos guias de início rápido, tutoriais e artigos de instruções. As bibliotecas de R e Python no [Machine Learning do SQL Server](what-is-sql-server-machine-learning.md) incluem distribuições de base, modelos de ciência de dados, algoritmos de aprendizado de máquina e funções para conduzir a análise de alto desempenho em escala, sem precisar transferir dados pela rede.

|   |   |
|---|:--|
| ![Logotipo do R](media/index/logo_r.png) | R de software livre, estendido com [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) e algoritmos da IA da Microsoft no [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package). Essas bibliotecas fornecem modelos de previsão, análise estatística, visualização e manipulação de dados em escala.<br/>A integração do R começa no [SQL Server 2016](install/sql-r-services-windows-install.md) e também está no [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| ![Logotipo do Python](media/index/logo_python.png) | Os desenvolvedores de Python podem usar as bibliotecas [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) da Microsoft para análise preditiva e aprendizado de máquina em escala. As bibliotecas compatíveis com Anaconda e Python 3.5 são a distribuição de linha de base.<br/>A integração do Python começa no [SQL Server 2017](install/sql-machine-learning-services-windows-install.md). |
| &nbsp; | &nbsp; |
::: moniker-end

## <a name="5-minute-quickstarts"></a>Guias de início rápido de cinco minutos

- [Criar um modelo preditivo em R](tutorials/rtsql-create-a-predictive-model-r.md)

- [Prever e plotar com base no modelo usando R](tutorials/rtsql-predict-and-plot-from-model.md)

## <a name="step-by-step-tutorials"></a>Tutoriais passo a passo

- [Como adicionar o aprendizado de máquina e a estrutura de extensibilidade ao SQL Server](install/sql-machine-learning-services-windows-install.md)

- [Como executar o R do T-SQL e procedimentos armazenados](tutorials/sqldev-in-database-r-for-sql-developers.md)

- [Como usar a análise integrada no Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="video-introduction"></a>Introdução de vídeo

> [!VIDEO https://www.youtube.com/embed/ACejZ9optCQ]

## <a name="reference"></a>Referência

| Pacote | Idioma | Descrição |
|:--------|:---------|:------------|
| [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | R | Processamento paralelo e distribuído para tarefas do R: transformação de dados, exploração, visualização, estatística e análise preditiva. |
| [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | R | Funções com base em algoritmos de IA da Microsoft, adaptado para R. |
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | R | Importa dados de cubos OLAP. |
| [sqlRUtils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | R | Funções de auxiliar para encapsular o R e T-SQL. |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Python | Processamento paralelo e distribuído para tarefas do Python: transformação de dados, exploração, visualização, estatística e análise preditiva. |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Python | Funções com base em algoritmos de IA da Microsoft, adaptado para Python. |
| &nbsp; | &nbsp; | &nbsp; |
