---
title: Executar testes de unidade do SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.unittesting.testconfig
ms.assetid: febcc87f-eb18-4c12-ba30-82ef0d49aaa3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ddc31964a018bec7dc0829d21e85283db5f069e1
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65101877"
---
# <a name="running-sql-server-unit-tests"></a>Executando testes de unidade do SQL Server
Para melhorar e manter a qualidade do código, crie e execute testes de unidade do SQL Server que verifiquem o comportamento de qualquer objeto de banco de dados e faça check-in desses testes para controle de versão. À medida que você ou qualquer membro da sua equipe altera o esquema de banco de dados, você executa testes de unidade do SQL Server e testes de unidade de software para verificar se as alterações não prejudicarão a funcionalidade existente. Você pode executar testes individuais ou pode executar grupos de testes, que são conhecidos como listas de testes. Para saber mais, confira [Usar listas de teste (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182461(VS.100).aspx).  
  
## <a name="ways-to-run-sql-server-unit-tests"></a>Formas de executar testes de unidade do SQL Server  
Você pode executar os testes de unidade do SQL Server de diversas maneiras, que variam de acordo com o software instalado, conforme é mostrado a seguir:  
  
-   Execute testes usando a janela **Modo de Teste** do Visual Studio 2010. Para obter mais informações, confira [Como executar testes de unidade do SQL Server](../ssdt/how-to-run-sql-server-unit-tests.md) e [Como executar testes automatizados no Microsoft Visual Studio 2010](https://msdn.microsoft.com/library/ms182470(VS.100).aspx). Para o Visual Studio 2012, veja [Como executar testes automatizados no Microsoft Visual Studio 2012](https://msdn.microsoft.com/library/ms182470.aspx).  
  
-   Execute os testes usando o comando MSTest.exe em um prompt de comando. Para obter mais informações, confira [Como Executar testes automatizados da linha de comando usando MSTest (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182487(VS.100).aspx) ou [Como Executar testes automatizados da linha de comando usando MSTest (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182487.aspx).  
  
-   Execute os testes no **Gerenciador de Soluções** executando um projeto de teste. Para obter mais informações, confira [Como executar testes automatizados no Microsoft Visual Studio 2010](https://msdn.microsoft.com/library/ms182470(VS.100).aspx) ou [Como executar testes automatizados no Microsoft Visual Studio 2012](https://msdn.microsoft.com/library/ms182470.aspx).  
  
-   Execute novamente os testes na janela **Resultados dos Testes**. Para obter mais informações, confira [Como executar um teste novamente (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182472(VS.100).aspx).  
  
-   Execute testes individuais ou listas de testes na janela (Visual Studio 2010) **Editor de Lista de Testes**. Para obter mais informações, confira [Como executar testes automatizados no Microsoft Visual Studio 2010](https://msdn.microsoft.com/library/ms182470(VS.100).aspx) ou [Como executar testes automatizados no Microsoft Visual Studio 2012](https://msdn.microsoft.com/library/ms182470.aspx).  
  
-   Execute testes quando compilar um projeto no Team Foundation Build. Para obter mais informações, confira [Como configurar e executar testes agendados depois de criar seu aplicativo (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182465(VS.100).aspx) ou [Como configurar e executar testes agendados depois de criar seu aplicativo (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182465.aspx).  
  
Você pode executar os testes de unidade do SQL Server em uma ordem específica usando um teste ordenado. Para obter mais informações, confira [Como Criar um teste ordenado (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182631(VS.100).aspx) ou [Como Criar um teste ordenado (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182631.aspx).  
  
## <a name="interpreting-tests-results"></a>Interpretando os resultados dos testes  
Depois que você executar os testes, a janela **Resultados de Teste** mostra quais testes foram aprovados ou apresentaram falha. Para saber mais, confira [Interpretar resultados do teste de unidade do SQL Server](../ssdt/interpreting-sql-server-unit-test-results.md). Para obter mais informações sobre como diagnosticar uma falha inesperada, veja [Como depurar objetos de banco de dados](../ssdt/how-to-debug-database-objects.md).  
  
## <a name="topics-in-this-section"></a>Tópicos nesta seção  
Esta seção contém os seguintes tópicos:  
  
-   [Como: depurar objetos de banco de dados](../ssdt/how-to-debug-database-objects.md)  
  
-   [Como: executar testes de unidade do SQL Server no Team Foundation Build](../ssdt/how-to-run-sql-server-unit-tests-from-team-foundation-build.md)  
  
-   [Como: Executar testes de unidade do SQL Server](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
-   [Interpretar resultados do teste de unidade do SQL Server](../ssdt/interpreting-sql-server-unit-test-results.md)  
  
## <a name="related-scenarios"></a>Cenários relacionados  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
Você pode definir testes de unidade para verificar o comportamento dos objetos de banco de dados e associar cada projeto de teste a um plano de geração de dados, uma configuração de implantação e uma cadeia de conexão diferentes.  
  
[Condições de teste personalizadas para testes de unidade do SQL Server](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
Você pode criar uma condição de teste personalizada para testar qualquer condição que não possa verificar, usando as condições de teste padrão.  
  
## <a name="see-also"></a>Consulte Também  
[Verificar o código do banco de dados usando os testes de unidade do SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
