---
title: SQL Server R Services | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 140885b86f0f6fa1a56119246c859f143f596726
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="machine-learning-services-with-python"></a>Serviços de aprendizado de máquina com Python

Python é uma linguagem que oferece excelente flexibilidade e capacidade para uma variedade de tarefas de aprendizado de máquina. As bibliotecas de código-fonte aberto para Python incluem várias plataformas para redes neurais personalizáveis, bem como bibliotecas populares para processamento de linguagem natural. Agora, este idioma amplamente utilizado é suportado no SQL Server de 2017 CTP 2.0 e versões posteriores.

Como o Python é integrado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados, você pode manter a análise próxima aos dados e eliminar os custos e os riscos de segurança associados à movimentação de dados.  Você pode implantar soluções de aprendizado de máquina com base em Python usando ferramentas familiares e convenientes como o Visual Studio. Os aplicativos de produção podem obter previsões, modelos, ou procedimento armazenado de visuais de tempo de execução do Python 3.5 simplesmente chamando um T-SQL.

Esta versão inclui a distribuição Anaconda do Python, bem como o novo [revoscalepy](../python/what-is-revoscalepy.md) biblioteca, para melhorar o desempenho de sua soluções de aprendizado de máquina e a escala.

Você pode instalar tudo que você precisa para começar a usar o Python por meio da instalação do SQL Server 2017:

+ **Serviços de aprendizado de máquina (no banco de dados):** instalar esse recurso, junto com o mecanismo de banco de dados do SQL Server, para permitir a execução segura de scripts de R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador.
  
     Quando você seleciona esse recurso, extensões são instaladas no mecanismo de banco de dados para permitir a execução de scripts de Python e um novo serviço é criado, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para gerenciar as comunicações entre o tempo de execução do Python e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.

+ **Servidor de aprendizado de máquina (autônomo):** se você não precisar de integração do SQL Server, instale esse recurso para obter suporte de Python no Microsoft R Server. Isso permite que você operacionalizar soluções de Python usando **mrsdeploy**.
  
     Não instale esse recurso no mesmo computador que está executando serviços de aprendizado de máquina do SQL Server.


## <a name="additional-resources"></a>Recursos adicionais

[Configurar serviços no banco de dados de aprendizado de máquina do Python](setup-python-machine-learning-services.md)

[Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)