---
title: Criar membros calculados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3bfa37a34ae6c3010c36dfe7693bb6d569e6e63d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209060"
---
# <a name="create-calculated-members"></a>Criar membros calculados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  É possível criar medidas ou membro de dimensão personalizados, chamados membros calculados, combinando dados de cubo, operadores aritméticos, números e funções. Por exemplo, você pode criar um membro calculado chamado Euros que converte dólares em euros multiplicando uma medida existente em dólar pela taxa de conversão. Euros pode então ser exibido aos usuários finais em uma linha ou coluna separada.  
  
 As definições dos membros calculados são armazenadas, mas seus valores existem apenas na memória. No exemplo anterior, valores em euros são exibidas aos usuários finais, mas não são armazenados como dados de cubo.  
  
 Os membros calculados são criados em cubos. Para criar um membro calculado, no Designer de Cubo, na guia **Cálculos** , clique no ícone **Novo Membro Calculado** na barra de ferramentas. Esse comando exibirá um formulário para você especificar as seguintes opções para o membro calculado:  
  
 **Name**  
 Selecione o nome do membro calculado. Ele aparecerá como título da coluna ou linha dos valores do membro calculado quando os usuários navegarem no cubo.  
  
 **Hierarquia pai**  
 Selecione a hierarquia pai que será incluída no membro calculado. Hierarquias são categorias descritivas de uma dimensão pelas quais os dados numéricos (ou seja, medidas) de um cubo podem ser separados para análise. Em navegadores tabulares, as hierarquias fornecem os títulos de colunas e linhas exibidas aos usuários finais quando eles procuram dados em um cubo. (Em navegadores gráficos, fornecem outros tipos de rótulos descritivos, mas sua função é a mesma que nos navegadores tabulares.) Um membro calculado fornece um novo título (ou nome) na dimensão pai selecionada.  
  
 Como alternativa, é possível incluir o membro calculado nas medidas em vez de em uma dimensão. Essa opção também fornece um novo título de coluna ou linha, mas ele será anexado a medidas no navegador.  
  
 **Membro pai**  
 Clique em **Alterar** para selecionar um membro pai que será incluído no membro calculado. Essa opção estará indisponível se você selecionar uma hierarquia de um nível ou MEASURES como a dimensão pai.  
  
 Hierarquias são divididas em níveis que contêm membros. Cada membro produz um título. Ao procurar dados em um cubo, os usuários finais podem fazer uma busca detalhada a partir de um título selecionado até títulos subordinados que antes não eram exibidos. O título do membro calculado é adicionado ao nível diretamente abaixo do membro pai selecionado.  
  
 **Expressão**  
 Especifique a expressão que produz os valores do membro calculado. Ela pode ser escrita em MDX. A expressão pode conter uma das seguintes opções:  
  
-   Expressões de dados que representam componentes de cubo, como dimensões, níveis, medidas, etc.  
  
-   Operadores aritméticos  
  
-   Números  
  
-   Funções  
  
 É possível arrastar ou copiar os componentes do cubo da guia **Metadados** do painel **Ferramentas de Cálculo** para adicioná-los rapidamente à expressão.  
  
> [!IMPORTANT]  
>  Todo membro calculado que será utilizado na expressão de valor de outro membro calculado deve ser criado antes que esse membro calculado possa usá-lo.  
  
 Cadeia de formato  
 Especifica o formato dos valores das células com base no membro calculado. Essa propriedade aceita os mesmos valores como a propriedade **Display Format** para medidas. Para obter mais informações sobre formatos de exibição, consulte [Configurar Propriedades de Medida](../../analysis-services/multidimensional-models/configure-measure-properties.md).  
  
 Visível  
 Determina se o membro calculado ficará visível ou oculto quando os metadados do cubo forem recuperados. Se ficar oculto, ainda poderá ser usado em expressões, instruções e scripts MDX, mas não será exibido como objeto selecionável nas interface de usuário clientes.  
  
 Comportamento não vazio  
 Armazena os nomes de medidas usadas para resolver consultas NON EMPTY em MDX. Se essa propriedade estiver em branco, o membro calculado deverá ser avaliado repetidamente para determinar se o membro está vazio. Se ela contiver o nome de uma ou mais medidas, o membro calculado será tratado como vazio se todas as medidas especificadas estiverem vazias. Essa propriedade é uma dica de otimização para o Analysis Services retornar apenas registros não NULL. O retorno apenas de registros não NULL melhora o desempenho das consultas MDX que utilizam o operador NON EMPTY ou a função NonEmpty ou que exigem o cálculo dos valores das células. Para melhor desempenho com cálculos de célula, especifique somente um membro sempre que possível.  
  
 Expressões de Cores  
 Especifica expressões MDX que configuram dinamicamente as cores de primeiro plano e do plano de fundo das células de acordo com o valor do membro calculado. Essa propriedade será ignorada se não for suportada pelos aplicativos cliente.  
  
 Expressões de Fonte  
 Especifica expressões MDX que configuram dinamicamente a fonte, o tamanho de fonte e os atributos de fonte das células de acordo com o valor do membro calculado. Essa propriedade será ignorada se não for suportada pelos aplicativos cliente.  
  
 É possível copiar ou arrastar os componentes do cubo da guia **Metadados** do painel **Ferramentas de Cálculo** para a caixa **Expressão** do painel Expressões de Cálculo. É possível copiar ou arrastar funções da guia **Funções** do painel **Ferramentas de Cálculo** para a caixa **Expressão** do painel Expressões de Cálculo.  
  
## <a name="addressing-calculated-members"></a>Direcionando membros calculados  
 Ao criar um membro calculado na guia **Cálculos** do **Designer de Cubo**, você especifica a hierarquia pai na qual ele será armazenado. A hierarquia pai determina como um membro calculado pode ser se direcionado, de acordo com estas regras:  
  
-   Se um membro calculado for criado na dimensão de medidas, poderá ser direcionado nessa dimensão.  
  
## <a name="see-also"></a>Consulte também  
 [Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
