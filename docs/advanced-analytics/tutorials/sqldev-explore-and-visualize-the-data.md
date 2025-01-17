---
title: Lição 1 explorar e Visualizar dados usando o R e o T-SQL
description: Tutorial mostrando como explorar e Visualizar dados de SQL Server usando as funções do R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2c204e06edd830d8036b6d0119ce1aff1a9c6833
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715375"
---
# <a name="lesson-1-explore-and-visualize-the-data"></a>Lição 1: Explorar e visualizar os dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo faz parte de um tutorial para desenvolvedores de SQL sobre como usar o R no SQL Server.

Nesta etapa, você examinará os dados de exemplo e, em seguida, gerará algumas plotagens usando [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) de [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e a função [sua](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist) genérica no R base. Essas funções do R já estão incluídas [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]no.

Um objetivo importante desta lição é mostrar como chamar funções do [!INCLUDE[tsql](../../includes/tsql-md.md)] R em procedimentos armazenados e salvar os resultados em formatos de arquivo de aplicativo:

+ Crie um procedimento armazenado usando **RxHistogram** para gerar um gráfico de R como dados varbinary. Use o **bcp** para exportar o fluxo binário para um arquivo de imagem.
+ Crie um procedimento armazenado usando **sua** para gerar uma plotagem, salvando resultados como saída jpg e PDF.

> [!NOTE]
> Como a visualização é uma ferramenta eficiente para entender a forma e a distribuição de dados, o R fornece uma variedade de funções e pacotes para gerar histogramas, gráficos de dispersão, plotagens de caixa e outros grafos de exploração de dados. Normalmente, o R cria imagens usando um dispositivo R para saída gráfica, que você pode capturar e armazenar como um tipo de dados **varbinary** para renderização no aplicativo. Você também pode salvar as imagens em qualquer um dos formatos de arquivo de suporte (. JPG,. PDF, etc.).

## <a name="review-the-data"></a>Examinar os dados

Em geral, o desenvolvimento de uma solução de ciência de dados inclui intensiva exploração e visualização de dados. Primeiro, Reserve um minuto para examinar os dados de exemplo, caso ainda não tenha feito isso.

No conjunto de entrada público original, os identificadores de táxi e os registros de viagem foram fornecidos em arquivos separados. No entanto, para tornar os dados de exemplo mais fáceis de usar, os dois DataSets originais foram Unidos nas colunas _Medallion_, _licença de\_hack_e DateTime de _retirada\__ .  Também foram obtidas amostras dos registros para que fosse obtido apenas 1% do número original de registros. O conjunto de dados resultante com redução da resolução tem 1.703.957 linhas e 23 colunas.

**Identificadores de táxi**
  
-   A coluna _Medallion_ representa o número de ID exclusivo do táxi.
  
-   A _coluna\_licença de ataque_ contém o número de licença do driver de táxi (anônimo).
  
**Registros de corrida e tarifa**
  
-   Cada registro de corrida inclui os locais de embarque e desembarque de passageiros, a hora e a distância da corrida.
  
-   Cada registro de tarifa inclui informações de pagamento, como a forma de pagamento, o valor total do pagamento e o valor da gorjeta.
  
-   As três últimas colunas podem ser usadas para várias tarefas de aprendizado de máquina. A _coluna\_valor da gorjeta_ contém valores numéricos contínuos e pode ser usada como a coluna de **rótulo** para análise de regressão. A coluna _tipped_ tem apenas valores sim/não e é usada para classificação binária. A coluna de _classe\_Tip_ tem vários **Rótulos de classe** e, portanto, pode ser usada como o rótulo para tarefas de classificação de várias classes.
  
    Este passo a passo demonstra apenas a tarefa de classificação binária; sinta-se à vontade para tentar criar modelos para as outras duas tarefas de aprendizado de máquina, regressão e classificação de várias classes.
  
-   Os valores usados para as colunas de rótulo são todos baseados na _coluna\_valor da gorjeta_ , usando estas regras de negócio:
  
    |Nome de coluna derivada|Regra|
    |-|-|
     |tipped|Se tip_amount > 0, tipped = 1; caso contrário, tipped = 0|
    |tip_class|Classe 0: tip_amount = $0<br /><br />Classe 1: tip_amount > US$ 0 e tip_amount <= US$ 5<br /><br />Classe 2: tip_amount > US$ 5 e tip_amount <= US$ 10<br /><br />Classe 3: tip_amount > US$ 10 e tip_amount <= US$ 20<br /><br />Classe 4: tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>Criar um procedimento armazenado usando rxHistogram para plotar os dados

Para criar a plotagem, use [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram), uma das funções avançadas do R fornecidas em [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). Esta etapa Plota um histograma com base em dados de uma [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. Você pode encapsular essa função em um procedimento armazenado, **PlotRxHistogram**.

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de objetos, clique com o botão direito do mouse no banco de dados **NYCTaxi_Sample** e selecione **nova consulta**.

2. Cole o script a seguir para criar um procedimento armazenado que plota o histograma. Este exemplo é chamado **RPlotRxHistogram*.

    ```sql
    CREATE PROCEDURE [dbo].[RxPlotHistogram]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM nyctaxi_sample'  
      EXECUTE sp_execute_external_script @language = N'R',  
                                         @script = N'  
       image_file = tempfile();  
       jpeg(filename = image_file);  
       #Plot histogram  
       rxHistogram(~tipped, data=InputDataSet, col=''lightgreen'',   
       title = ''Tip Histogram'', xlab =''Tipped or not'', ylab =''Counts'');  
       dev.off();  
       OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
       ',  
       @input_data_1 = @query  
       WITH RESULT SETS ((plot varbinary(max)));  
    END
    GO
    ```

Os principais pontos a serem compreendidos nesse script incluem o seguinte: 
  
+ A variável `@query` define o texto da consulta (`'SELECT tipped FROM nyctaxi_sample'`), que é passado para o script do R como o argumento da variável de entrada de script, `@input_data_1`. Para scripts R que são executados como processos externos, você deve ter um mapeamento de um-para-um entre entradas para o script e entradas para o procedimento armazenado do sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) que inicia a sessão do R no SQL Server.
  
+ No script R, uma variável (`image_file`) é definida para armazenar a imagem. 

+ A função **rxHistogram** da biblioteca RevoScaleR é chamada para gerar o gráfico.
  
+ O dispositivo R está definido como **off** porque você está executando esse comando como um script externo em SQL Server. Normalmente, no R, quando você emite um comando de plotagem de alto nível, R abre uma janela de gráficos, chamada de *dispositivo*. Você pode desativar o dispositivo se estiver gravando em um arquivo ou manipulando a saída de alguma outra maneira.
  
+ O objeto gráfico do R é serializado para um data.frame do R para saída.

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>Executar o procedimento armazenado e usar o bcp para exportar dados binários para um arquivo de imagem

O procedimento armazenado retorna a imagem como um fluxo de dados varbinary, que obviamente não pode ser exibido de forma direta. No entanto, você pode usar o utilitário **bcp** para obter os dados varbinary e salvá-los como um arquivo de imagem em um computador cliente.
  
1. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], execute a seguinte instrução:
  
    ```sql
    EXEC [dbo].[RxPlotHistogram]
    ```
  
    **Resultados**
    
    *plotagem* *0xFFD8FFE000104A4649...*
  
2. Abra um prompt de comando do PowerShell e execute o comando a seguir, fornecendo o nome de instância apropriado, o nome do banco de dados, o nome de usuário e as credenciais como argumentos. Para aqueles que usam identidades do Windows, você pode substituir **-U** e **-P** por **-T**.
  
    ```powershell
    bcp "exec RxPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
    ```

    > [!NOTE]
    > As opções de comando para bcp diferenciam maiúsculas de minúsculas.
  
3. Se a conexão for bem-sucedida, será solicitado que você insira mais informações sobre o formato de arquivo gráfico. 

   Pressione ENTER em cada prompt para aceitar os padrões, exceto para essas alterações:
    
   + Em **comprimento do prefixo de plotagem do campo**, digite 0
  
   + Digite **Y** se você desejar salvar os parâmetros de saída para reutilização posterior.
  
    ```powershell
    Enter the file storage type of field plot [varbinary(max)]: 
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **Resultados**
    
    ```powershell
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > Se você salvar as informações de formato em um arquivo (bcp.fmt), o utilitário **bcp** vai gerar uma definição de formato que pode ser aplicada a comandos semelhantes no futuro, sem a solicitação de escolher opções de formato de arquivo gráfico. Para usar o arquivo de formato, adicione `-f bcp.fmt` ao final da linha de comando, após o argumento de senha.
  
4.  O arquivo de saída será criado no mesmo diretório em que você executou o comando do PowerShell. Para exibir a plotagem, basta abrir o arquivo plot.jpg.
  
    ![viagens de táxi com e sem gorjetas](media/rsql-devtut-tippedornot.jpg "viagens de táxi com e sem gorjetas")  
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>Criar um procedimento armazenado usando sua e vários formatos de saída

Normalmente, os cientistas de dados geram várias visualizações de dados para obter informações sobre os dados de diferentes perspectivas. Neste exemplo, você criará um procedimento armazenado chamado **RPlotHist** para gravar histogramas, dispersões e outros gráficos do R em. JPG e. Formato PDF.

Esse procedimento armazenado usa a função **sua** para criar o histograma, exportando os dados binários para formatos populares, como. JPG,. PDF e. PNG. 

1. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de objetos, clique com o botão direito do mouse no banco de dados **NYCTaxi_Sample** e selecione **nova consulta**.

2. Cole o script a seguir para criar um procedimento armazenado que plota o histograma. Este exemplo é chamado de **RPlotHist** .
  
    ```sql
    CREATE PROCEDURE [dbo].[RPlotHist]  
    AS  
    BEGIN  
      SET NOCOUNT ON;  
      DECLARE @query nvarchar(max) =  
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'  
      EXECUTE sp_execute_external_script @language = N'R',  
      @script = N'  
       # Set output directory for files and check for existing files with same names   
        mainDir <- ''C:\\temp\\plots''  
        dir.create(mainDir, recursive = TRUE, showWarnings = FALSE)  
        setwd(mainDir);  
        print("Creating output plot files:", quote=FALSE)
        
        # Open a jpeg file and output histogram of tipped variable in that file.  
        dest_filename = tempfile(pattern = ''rHistogram_Tipped_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.jpg'',sep="")  
        print(dest_filename, quote=FALSE);  
        jpeg(filename=dest_filename);  
        hist(InputDataSet$tipped, col = ''lightgreen'', xlab=''Tipped'',   
            ylab = ''Counts'', main = ''Histogram, Tipped'');  
         dev.off();  

        # Open a pdf file and output histograms of tip amount and fare amount.   
        # Outputs two plots in one row  
        dest_filename = tempfile(pattern = ''rHistograms_Tip_and_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=7);  
        par(mfrow=c(1,2));  
        hist(InputDataSet$tip_amount, col = ''lightgreen'',   
            xlab=''Tip amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram, Tip amount'', xlim = c(0,40), 100);  
        hist(InputDataSet$fare_amount, col = ''lightgreen'',   
            xlab=''Fare amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram,   
            Fare amount'',   
            xlim = c(0,100), 100);  
       dev.off();  
  
        # Open a pdf file and output an xyplot of tip amount vs. fare amount using lattice;  
        # Only 10,000 sampled observations are plotted here, otherwise file is large.  
        dest_filename = tempfile(pattern = ''rXYPlots_Tip_vs_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=4);  
        plot(tip_amount ~ fare_amount,   
            data = InputDataSet[sample(nrow(InputDataSet), 10000), ],   
            ylim = c(0,50),   
            xlim = c(0,150),   
            cex=.5,   
            pch=19,   
            col=''darkgreen'',    
            main = ''Tip amount by Fare amount'',   
            xlab=''Fare Amount ($)'',   
            ylab = ''Tip Amount ($)'');   
        dev.off();',  
     @input_data_1 = @query  
     END
    ```
  
+ A saída da consulta SELECT no procedimento armazenado é armazenada no quadro de dados padrão do R, `InputDataSet`. Várias funções de plotagem do R podem ser chamadas para gerar os arquivos gráficos reais. A maior parte do script do R inserido representa opções para essas funções gráficas, como `plot` ou `hist`.
  
+ Todos os arquivos são salvos na pasta local C:\temp\Plots. A pasta de destino é definida pelos argumentos fornecidos ao script do R como parte do procedimento armazenado.  Você pode alterar a pasta de destino alterando o valor da variável `mainDir`.

+ Para gerar os arquivos em uma pasta diferente, altere o valor da variável `mainDir` no script do R inserido no procedimento armazenado. Você também pode modificar o script para gerar formatos diferentes, mais arquivos e assim por diante.

### <a name="execute-the-stored-procedure"></a>Executar o procedimento armazenado

Execute a instrução a seguir para exportar dados de plotagem binários para formatos de arquivo JPEG e PDF.

```sql
EXEC RPlotHist
```

**Resultados**
    
```sql
STDOUT message(s) from external script:
[1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 

C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]

C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
```

Os números nos nomes de arquivo são gerados aleatoriamente para garantir que você não receba um erro ao tentar gravar em um arquivo existente.

### <a name="view-output"></a>Exibir saída 

Para exibir o gráfico, abra a pasta de destino e examine os arquivos que foram criados pelo código R no procedimento armazenado.

1. Vá para a pasta indicada na mensagem STDOUT (no exemplo, isso é C:\temp\plots\)

2. Abrir `rHistogram_Tipped.jpg` para mostrar o número de corridas que receberam uma gorjeta versus as corridas que não receberam gorjeta. (Esse histograma é muito parecido com aquele que você gerou na etapa anterior.)

3. Abrir `rHistograms_Tip_and_Fare_Amount.pdf` para exibir a distribuição de valores de gorjeta, plotados em relação aos valores de Tarifa.
    
  ![histograma mostrando tip_amount e fare_amount](media/rsql-devtut-tipamtfareamt.PNG "histograma mostrando tip_amount e fare_amount")

4. Abrir `rXYPlots_Tip_vs_Fare_Amount.pdf` para exibir um dispersão com o valor da tarifa no eixo x e o valor da gorjeta no eixo y.

   ![valor da gorjeta plotado sobre o valor da tarifa](media/rsql-devtut-tipamtbyfareamt.PNG "valor da gorjeta plotado sobre o valor da tarifa")

## <a name="next-lesson"></a>Próxima lição

[Lição 2: Criar recursos de dados usando o T-SQL](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>Lição anterior

[Configurar dados de demonstração do NYC táxi](demo-data-nyctaxi-in-sql.md)
