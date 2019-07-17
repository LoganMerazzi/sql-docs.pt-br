---
title: Replicação bidirecional entre filtros em modelos de tabela do Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eee2e859abf5b7924cb072c4653ac3e83e7b7824
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163154"
---
# <a name="bi-directional-cross-filters-in-tabular-models"></a>Filtros cruzados de BI-direcional em modelos de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Novo método interno do SQL Server 2016 para habilitação de *filtros cruzados bidirecionais* em modelos de tabela, que elimina a necessidade de soluções alternativas manuais de DAX para a propagação de contextos de filtro em relações da tabela.  
  
 Dividindo o conceito pelas respectivas partes componentes: *filtragem cruzada* é a capacidade de definir um contexto de filtro em uma tabela com base nos valores de uma tabela relacionada; *bidirecional* se refere à transferência de um contexto de filtro para uma segunda tabela relacionada do outro lado de uma relação de tabela. Como o próprio nome sugere, você pode fatiar nas duas direções da relação em vez de usar apenas uma.  Internamente, a filtragem bidirecional expande o contexto do filtro para consultar um superconjunto dos dados.  
  
 ![SSAS-BIDI-1-Filteroption](../../analysis-services/tabular-models/media/ssas-bidi-1-filteroption.PNG "Filteroption SSAS-BIDI-1")  
  
 Há dois tipos de filtros cruzados: Filtragem unidirecional e bidirecional. Unidirecional é a direção do filtro tradicional de muitos para um entre tabelas de fatos e tabelas de dimensões nessa relação. Bidirecional é um filtro cruzado que permite o uso do contexto do filtro de uma única relação como o contexto do filtro de outra relação de tabela, com uma única tabela comum para as duas relações.  
  
 Considerando **DimDate** e **DimProduct** com relações de chave estrangeira para **FactOnlineSales**, um filtro cruzado bidirecional é equivalente a **FactOnlineSales-DimDate** e **FactOnlineSales-DimProduct** usados simultaneamente.  
  
 Os filtros cruzados bidirecionais podem ser uma solução fácil para o problema de design de muitos para muitos, que desafiou os desenvolvedores de tabelas e do Power Pivot no passado. Se você já usou a solução alternativa DAX para relações muitos-para-muitos na tabela ou modelos do Power Pivot, você pode tentar aplicar um filtro bidirecional para ver se ele produz os resultados esperados.  
  
 Quando criar um filtro cruzado bidirecional, lembre-se do seguinte:  
  
-   Pense bem antes de habilitar filtros bidirecionais.  
  
     Se habilitar filtros bidirecionais em todos os locais, os dados podem ser filtrados excessivamente, de maneiras inesperadas.  Além disso, você pode introduzir ambiguidades acidentalmente, criando mais de um caminho possível da consulta. Para evitar esses problemas, planeje o uso combinado dos filtros unidirecionais e bidirecionais.  
  
-   Faça testes incrementais para verificar o impacto de cada alteração do filtro no modelo. O recurso[Analisar no Excel](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md) funciona bem para testes incrementais. Como prática recomendada, continue fazendo testes periodicamente, usando outros clientes de relatório para que não haja imprevistos posteriormente.  
  
> [!NOTE]  
>  A partir da versão CTP 3.2, o SSDT inclui um padrão que determina a aplicação automática dos filtros cruzados bidirecionais. Se você habilitar filtros bidirecionais por padrão, o SSDT permitirá a filtragem bidirecional apenas se o modelo implementar claramente um único caminho da consulta, por meio de uma cadeia de relações de tabela.  
  
## <a name="set-the-default"></a>Definir o padrão  
 Filtros direcionais únicos são o padrão. Você pode mudar o padrão de todos os projetos novos criados no Designer ou no próprio modelo, se for um projeto existente.  
  
 A configuração é avaliada durante a criação, no nível do projeto. Portanto, se você alterar o padrão para bidirecional, verá os efeitos desta escolha, quando criar o projeto seguinte.  
  
1.  No SSDT, escolha **Ferramentas** > **Opções** > **Designers de tabela do Analysis Services**  >  **Novas configurações de projeto**.  
  
2.  Defina a **Direção do filtro padrão** como **Direção única** ou **Ambas as direções**.  
  
 Como alternativa, você pode mudar o padrão no modelo.  
  
1.  No Gerenciador de Soluções. escolha **Model.bim** > **Propriedades** .  
  
2.  Defina a **Direção do filtro padrão** como **Direção única** ou **Ambas as direções**.  
  
## <a name="walkthrough-an-example"></a>Apresentação de exemplo  
 A melhor maneira de avaliar o valor da filtragem cruzada bidirecional é por meio de um exemplo. Considere o seguinte conjunto de dados de [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279), que reflete a cardinalidade e os filtros cruzados criados por padrão.  
  
 ![Modelo-de-2-BIDI-SSAS](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "modelo SSAS-BIDI-2")  
  
> [!NOTE]  
>  Durante a importação de dados, as relações de tabela são criadas por padrão em configurações de muitos para um, geradas pelas relações da chave estranheira e da chave primária entre a tabela de fatos e as tabelas de dimensões relacionadas.  
  
 Observe que a direção do filtro é descrita das tabelas de dimensões para a tabela de fatos. Promoções, produtos, datas, clientes e geografia do cliente são filtros válidos que produzem com êxito a agregação de uma medida com o valor real, que pode variar com base nas dimensões usadas.  
  
 ![ssas-bidi-3-defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas-bidi-3-defaultrelationships")  
  
 Para este esquema em estrela simples, os testes no Excel confirmam que os dados são bem fatiados durante os fluxos de filtragem das tabelas de dimensões, em linhas e em colunas, para dados agregados fornecidos por uma medida **Soma das Vendas** , localizada na tabela central **FactOnlineSales** .  
  
 ![ssas-bidi-4-excelSumSales](../../analysis-services/tabular-models/media/ssas-bidi-4-excelsumsales.PNG "ssas-bidi-4-excelSumSales")  
  
 Como as medidas são extraídas da tabela de fatos e encerra o contexto do filtro na tabela de fatos, as agregações serão filtradas corretamente para este modelo. Mas, o que acontece se você quiser criar medidas em outro local, como uma contagem distinta na tabela de produtos ou de clientes ou um desconto médio na tabela de promoção e tiver um contexto de filtro existente estendido a essa medida?  
  
 Vamos experimentar adicionando uma contagem distinta de **DimProducts** à tabela dinâmica. Observe os valores repetidos da coluna **Contagem de Produtos**. Em princípio, isso parece uma relação de tabela ausente; no entanto, podemos ver que todas as relações estão totalmente definidas e ativas em nosso modelo. Nesse caso, os valores repetidos ocorrem porque não há nenhum filtro de datas nas linhas da tabela de produtos.  
  
 ![ssas-bidi-5-prodcount-nofilter](../../analysis-services/tabular-models/media/ssas-bidi-5-prodcount-nofilter.png "ssas-bidi-5-prodcount-nofilter")  
  
 Depois de adicionar um filtro cruzado bidirecional entre **FactOnlineSales** e **DimProduct**, as linhas da tabela de produtos agora são filtradas corretamente por data e por fabricante.  
  
 ![ssas-bidi-6-prodcount-withfilter](../../analysis-services/tabular-models/media/ssas-bidi-6-prodcount-withfilter.png "ssas-bidi-6-prodcount-withfilter")  
  
## <a name="learn-step-by-step"></a>Aprenda passo a passo  
 Para experimentar os filtros cruzados bidirecionais, confira esta apresentação passo a passo. Para acompanhar, você precisará de:  
  
-   Uma instância do Analysis Services para SQL Server 2016, um modelo de tabela e a versão mais recente do CTP  
  
-   [SQL Server Data Tools (SSDT) para Visual Studio 2015](http://go.microsoft.com/fwlink/p/?LinkID=627574)lançado com o CTP mais recente.  
  
-   [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279)  
  
-   Permissões de leitura para esses dados.  
  
-   O Excel (para usar com o recurso Analisar no Excel)  
  
### <a name="create-a-project"></a>Criar um projeto  
  
1.  Inicie o SQL Server Data Tools para Visual Studio 2015.  
  
2.  Clique em **Arquivo** > **Novo** > **Projeto** > **Modelos de Tabela do Analysis Services**.  
  
3.  No Designer de Modelos de Tabela, defina o banco de dados de workspace em uma instância da Visualização do Analysis Services para SQL Server 2016, no modo de servidor tabular.  
  
4.  Verifique se o nível de compatibilidade do modelo é definido como **SQL Server 2016 RTM (1200)** ou superior.  
  
     Clique em **OK** para criar o projeto.  
  
### <a name="add-data"></a>Adicionar dados  
  
1.  Clique em **Modelo** > **Importar da Fonte de Dados** > **Microsoft SQL Server**.  
  
2.  Especifique o servidor, o banco de dados e o método de autenticação.  
  
3.  Escolha o banco de dados ContosoRetailDW.  
  
4.  Clique em **Avançar**.  
  
5.  Para selecionar tabelas, clique em Ctrl e selecione as seguintes tabelas:  
  
    -   FactOnlineSales  
  
    -   DimCustomer  
  
    -   DimDate  
  
    -   DimGeography  
  
    -   DimPromotion  
  
     Você pode editar os nomes nessa ocasião para que eles fiquem mais legíveis no modelo.  
  
     ![ssas-bidi-7-ImportData](../../analysis-services/tabular-models/media/ssas-bidi-7-importdata.PNG "ssas-bidi-7-ImportData")  
  
6.  Importe os dados.  
  
 Se ocorrer erros, verifique se a conta usada para se conectar ao banco de dados tem um logon do SQL Server com permissões de leitura no data warehouse da Contoso. Em uma conexão remota, você pode também verificar a configuração da porta no firewall do SQL Server.  
  
### <a name="review-default-table-relationships"></a>Revisar as relações de tabela padrão  
 Alternar para exibição de diagrama: **Modelo** > **exibição de modelo** > **exibição de diagrama**. A cardinalidade e as relações ativas são indicadas visualmente. Todas as relações são de um-para-muitos entre duas tabelas relacionadas.  
  
 ![Modelo-de-2-BIDI-SSAS](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "modelo SSAS-BIDI-2")  
  
 Como alternativa, clique em **Tabela** > **Gerenciar Relações** para exibir as mesmas informações em um layout de tabela.  
  
 ![ssas-bidi-3-defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas-bidi-3-defaultrelationships")  
  
### <a name="create-measures"></a>Criar medidas  
 Você precisará de uma agregação para os valores de venda de soma por diferentes facetas de dados dimensionais. Na tabela **DimProduct** , você pode criar uma medida de contagem de produtos e usá-la em uma análise de merchandising que mostra uma contagem do número de produtos que fazem parte das vendas, em um determinado ano, região ou para um certo tipo de cliente.  
  
1.  Clique em **Modelo** > **Exibição de Modelo** > **Exibição de Diagrama**.  
  
2.  Clique em **FactOnlineSales**.  
  
3.  Escolha a coluna **SalesAmount** .  
  
4.  Clique em **Coluna** > **AutoSoma** > **Soma** para criar uma medida para as vendas.  
  
5.  Clique em **DimProduct**.  
  
6.  Escolha a **ProductKeycolumn**.  
  
7.  Clique em **Coluna** > **AutoSoma** > **DistinctCount** para criar uma medida para produtos únicos.  
  
### <a name="analyze-in-excel"></a>Analisar no Excel  
  
1.  Clique em **Modelo** > **Analisar no Excel** para reunir todos os dados em uma Tabela Dinâmica.  
  
2.  Selecione as duas medidas que você acabou de criar na lista de campos.  
  
3.  Selecione **Produtos** > **Fabricante**.  
  
4.  Escolha **Data** > **Ano Civil**.  
  
 Observe que as vendas são detalhadas por ano e por fabricante conforme esperado. Isso ocorre porque o padrão contexto do filtro entre **FactOnlineSales**, **DimProduct**, e **DimDate** funciona corretamente para medidas no lado 'muitos' da relação.  
  
 Ao mesmo tempo, você pode ver que a contagem de produtos não é captada no mesmo contexto do filtro das vendas. Embora as contagens de produtos sejam filtradas corretamente por fabricante (as contagens de fabricante e de produto estão na mesma tabela), o filtro de data não é propagado na contagem de produtos.  
  
### <a name="change-the-cross-filter"></a>Alterar o filtro cruzado  
  
1.  No modelo, escolha **Tabela** > **Gerenciar Relações**.  
  
2.  Edite a relação entre **FactOnlineSales** e **DimProduct**.  
  
     Altere a direção do filtro nas duas tabelas.  
  
3.  Salve as configurações.  
  
4.  Na pasta de trabalho, clique em **Atualizar** para ler o modelo novamente.  
  
 Agora você pode observar que as contagens de produtos e de vendas são filtradas pelo mesmo contexto do filtro, que inclui os fabricantes de **DimProducts** e também o ano civil de **DimDate**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Entenda quando e como um filtro cruzado bidirecional pode ser usado de forma empírica para ver como funciona para o seu cenário. Às vezes, você encontrará que os comportamentos internos não são suficientes e serão necessário recorrer a cálculos DAX para realizar o trabalho. No **Consulte também** seção, você encontrará vários links para recursos adicionais sobre este assunto.  
  
 Na prática, a filtragem cruzada permite formas de exploração de dados que são fornecidas normalmente apenas por meio de uma construção de muitos para muitos. Dito que, é importante reconhecer que bidirecionais filtragem cruzada não é uma construção de muitos-para-muitos.  A configuração de tabela de muitos para muitos continua sem suporte no Designer para os modelos de tabela desta versão.  
  
## <a name="see-also"></a>Confira também  
 [Criar e gerenciar relações no Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/464155-create-and-manage-relationships-in-power-bi-desktop)   
 [Um exemplo prático de como muitos para tratar relações simples no Power Pivot e modelos de tabela](http://social.technet.microsoft.com/wiki/contents/articles/22202.a-practical-example-of-how-to-handle-simple-many-to-many-relationships-in-power-pivotssas-tabular-models.aspx)   
 [Resolvendo relações de muitos para muitos aproveitando a filtragem cruzada de tabelas DAX](http://blog.gbrueckl.at/2012/05/resolving-many-to-many-relationships-leveraging-dax-cross-table-filtering/)   
 [A revolução muitos para muitos (blog do SQLBI)](http://www.sqlbi.com/articles/many2many/)  
  
  
