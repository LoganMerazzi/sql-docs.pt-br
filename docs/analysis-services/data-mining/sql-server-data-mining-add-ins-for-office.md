---
title: SQL Server Data Mining Add-Ins para o Office | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 89986d3c8de4a1cbefbccf285a92a2dc19c6c7aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151401"
---
# <a name="sql-server-data-mining-add-ins-for-office"></a>Suplementos de Mineração de Dados do SQL Server para Office

  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Suplementos de Mineração de Dados do para Office é um conjunto de ferramentas leve para análise preditiva que permite a você usar dados no Excel para criar modelos analíticos para previsão, recomendação ou exploração.  
  
> [!IMPORTANT]
> O data mining add-in para o Office não tem suporte no Office 2016 ou posterior.
  
 Os assistentes e as ferramentas de gerenciamento de dados nos suplementos fornecem instruções passo a passo para essas tarefas de mineração de dados comuns:  
  
-   **Organizar e limpar seus dados antes da modelagem.** Use dados armazenados no Excel ou em qualquer fonte de dados do Excel. Você pode criar e salvar conexões para reutilizar fontes de dados, repetir experimentos ou treinar modelos novamente.  
  
-   **Gere perfis, amostras e prepare.** Muitos mineradores de dados experientes indicam que 70 a 90% de um projeto de mineração de dados é gasto na preparação dos dados. Os suplementos podem tornar essa tarefa mais rápida, fornecendo visualizações no Excel e nos assistentes que ajudarão você com essas tarefas comuns:  
  
    -   Crie o perfil dos dados e entenda suas características e distribuição.  
  
    -   Crie conjuntos de treinamento e teste através da amostragem aleatória ou da sobreamostragem.  
  
    -   Encontre exceções, e remova-as ou substitua-as.  
  
    -   Rotule os dados novamente para melhorar a qualidade da análise.  
  
-   **Analise padrões por meio de aprendizado supervisionado ou não supervisionado.** Clique nos assistentes amigáveis para realizar algumas das tarefas de mineração de dados mais conhecidas, incluindo a análise de clustering, a análise de cesta de compras e previsão.  
  
     Entre os algoritmos de aprendizado de máquina conhecidos incluídos nos suplementos, estão o Naïve Bayes, a regressão logística, o clustering, a série temporal e as redes neurais.  
  
     Se você não tiver experiência em mineração de dados, obtenha ajuda para criar consultas de previsão no assistente de **Consulta** .  
  
     Usuários avançados podem criar consultas DMX personalizadas com o **Editor de Consulta Avançada**do tipo "arrastar e soltar", ou automatizar previsões usando o VBA do Excel.  
  
-   **Documente e gerencie.** Depois que você criou um conjunto de dados e criar alguns modelos, documente seu trabalho e suas ideias gerando um resumo estatístico dos parâmetros de modelo e de dados.  
  
-   **Explorar e visualizar.** Mineração de dados não é uma atividade que pode ser totalmente automatizada - você precisa explorar e compreender seus resultados para tomar uma ação significativa. Os suplementos ajudam você na exploração, fornecendo visualizadores interativos no Excel, modelos do Visio que permitem personalizar os diagramas e a capacidade de exportar gráficos e tabelas para o Excel para filtragem ou modificação adicionais.  
  
-   **Implante e integre.** Quando você criou um modelo útil, coloque-o em produção, usando as ferramentas de gerenciamento para exportar o modelo do seu servidor experimental para outra instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Você também pode deixar o modelo no servidor onde o criou, mas atualize os dados de treinamento e execute previsões usando o Integration Services ou scripts DMX.  
  
     Os usuários avançados apreciarão a funcionalidade de **rastreamento** , que permite exibir as instruções XMLA e DMX enviadas para o servidor.  
  
## <a name="getting-started"></a>Introdução  
 Para obter mais informações, veja [O que está incluído nos Suplementos de Data Mining para o Office](http://go.microsoft.com/fwlink/p/?LinkId=616849)  
  
## <a name="support-and-requirements"></a>Suporte e requisitos  
 Os Suplementos de Mineração de Dados do SQL Server para Office são downloads gratuitos. Você deve ter uma das versões do Office a seguir já instaladas para usar essas ferramentas:  
  
-   Office 2010, versões de 32 bits ou 64 bits  
  
-   Office 2013, versões de 32 bits ou 64 bits  
  
> [!WARNING]  
>  Baixe a versão dos suplementos que corresponda à sua versão do Excel.  
  
 Os Suplementos de Mineração de Dados requerem uma conexão com uma das seguintes edições do SQL Server Analysis Services:  
  
-   Enterprise  
  
-   Business Intelligence  
  
-   Standard  
  
 Dependendo da edição do SQL Server Analysis Services ao você se conectará, alguns algoritmos avançados possivelmente não estarão disponíveis. Para obter informações, consulte [Recursos com suporte nas edições do SQL Server 2016](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).  
  
 Para obter ajuda adicional com a instalação, consulte esta página no Centro de Download: [http://www.microsoft.com/download/details.aspx?id=29061](http://www.microsoft.com/download/details.aspx?id=29061)  
  
  
