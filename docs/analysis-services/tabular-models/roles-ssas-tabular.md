---
title: Funções de modelo de tabela do Analysis Services | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d6c42615115ae486d14112a1a1dbd7f05d6328eb
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263300"
---
# <a name="roles"></a>Funções
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Funções, em modelos tabulares, definem permissões de membro para um modelo. Membros da função podem executar ações no modelo conforme definido pela permissão de função. As funções definidas com permissões de leitura também podem fornecer segurança adicional no nível de linha usando filtros no nível de linha. 
  
 Para o SQL Server Analysis Services, funções contêm membros de usuário por nome de usuário do Windows ou grupo do Windows e permissões (leitura, processo, administrador). Para o Azure Analysis Services, os usuários devem estar no seu Active Directory do Azure e nomes de usuário e grupos especificados devem ser pelo endereço de email organizacionais ou UPN. 

> [!IMPORTANT]  
>  Quando usar o SSDT para criar funções e adicionar usuários organizacionais a um modelo tabular de projeto que será implantado no Azure Analysis Services, use [espaço de trabalho integrado](workspace-database-ssas-tabular.md).

> [!IMPORTANT]  
>  Para que os usuários a se conectar a um modelo implantado por meio de um aplicativo cliente de relatório, você deve criar pelo menos uma função pelo menos a permissão para que esses usuários são membros de leitura.  
  
 Informações neste tópico se destina a autores de modelos tabulares que definem funções usando a caixa de diálogo Gerenciador de funções no SSDT. As funções definidas durante a criação do modelo aplicam-se ao banco de dados de workspace do modelo. Depois de um banco de dados de modelo foi implantado, os administradores de banco de dados de modelo podem gerenciar (Adicionar, editar e excluir) membros da função usando o SSMS. Para saber mais sobre como gerenciar os membros das funções em um banco de dados implantado, consulte [funções de modelo Tabular](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
##  <a name="bkmk_underst"></a> Understanding roles  
 As funções são usadas no Analysis Services para gerenciar o acesso de dados de modelo. Existem dois tipos de funções:  
  
-   A função de servidor, uma função fixa que fornece acesso de administrador para uma instância de servidor do Analysis Services.  
  
-   As funções de banco de dados, funções definidas por autores e administradores do modelo para controlar o acesso a banco de dados modelo e dados para usuários não administradores.  
  
 As funções, definidas para um modelo de tabela, são funções de banco de dados. Ou seja, as funções contêm membros que consistem em usuários ou grupos que têm permissões específicas que definem a ação que esses membros podem executar em banco de dados modelo. Uma função de banco de dados é criada como um objeto separado no banco de dados e aplica-se apenas ao banco de dados no qual a função foi criada. Usuários e grupos são incluídos na função pelo autor do modelo, que, por padrão, tem permissões de administrador no servidor de banco de dados de espaço de trabalho; para um modelo implantado, por um administrador.  
  
 As funções em modelos tabulares podem ser definidas posteriormente com filtros de linha. Os filtros de linha usam expressões DAX para definir as linhas em uma tabela, e as linhas relacionadas nas muitas direções, que um usuário pode consultar. Os filtros de linha que usam expressões DAX somente podem ser definidos para as permissões de Leitura e Leitura e Processo. Para obter mais informações, consulte [filtros de linha](#bkmk_rowfliters) mais adiante neste tópico.  
  
 Por padrão, quando você cria um novo projeto de modelo de tabela, o projeto de modelo não tem nenhuma função. As funções podem ser definidas usando a caixa de diálogo Gerenciador de funções no SSDT. Quando as funções são definidas durante a criação do modelo, elas são se aplicadas ao banco de dados de workspace do modelo. Quando o modelo é implantado, as mesmas funções são aplicadas ao modelo implantado. Depois que um modelo tiver sido implantado, os membros da função de servidor ([administrador do Analysis Services) e os administradores de banco de dados podem gerenciar as funções associadas ao modelo e os membros associados a cada função usando o SSMS.  
  
##  <a name="bkmk_permissions"></a> Permissões  
 Cada função tem uma única permissão de banco de dados definida (exceto para a permissão de Ler e Processar combinada). Por padrão, uma nova função terá a permissão Nenhum. Ou seja, quando os membros são adicionados à função com a permissão Nenhum, eles não podem modificar o banco de dados, executar uma operação de processo, consultar dados ou ver o banco de dados a menos que uma permissão diferente seja concedida.  
  
 Um grupo ou usuário pode ser um membro de qualquer número de funções, cada função com uma permissão diferente. Quando um usuário for um membro de várias funções, as permissões definidas para cada função serão cumulativas. Por exemplo, se um usuário for membro de uma função com permissão de leitura e também um membro de uma função com permissão Nenhum, ele terá permissão de leitura.  
  
 Cada função pode ter uma das seguintes permissões definidas:  
  
|Permissões|Descrição|Filtros de linha usando DAX|  
|-----------------|-----------------|----------------------------|  
|None|Os membros não podem fazer modificações ao esquema de banco de dados modelo e não podem consultar dados.|Filtros de linha não são aplicáveis. Os dados não são visíveis a usuários nesta função|  
|leitura|Os membros têm permissão de consultar dados (com base em filtros de linha), mas não podem ver o banco de dados modelo no SSMS, não podem fazer nenhuma alteração ao esquema de banco de dados modelo e o usuário não pode processar o modelo.|Os filtros de linha podem ser aplicados. Somente os dados especificados na fórmula DAX de filtro de linha são visíveis a usuários.|  
|Leitura e processo|Os membros têm permissão de consultar dados (com base em filtros em nível de linha) e executar operações de processo por meio de um script ou pacote que contém um comando de processo, mas não pode fazer nenhuma alteração ao banco de dados. Não é possível exibir o banco de dados modelo no SSMS.|Os filtros de linha podem ser aplicados. Somente os dados especificados na fórmula DAX de filtro de linha possam ser consultados.|  
|Processar|Os membros podem executar operações de processo por meio de um script ou pacote que contém um comando de processo. Não pode modificar o esquema de banco de dados modelo. Não é possível consultar dados. Não é possível consultar o banco de dados de modelo no SSMS.|Filtros de linha não são aplicáveis. Nenhum dado pode ser consultado nesta função|  
|Administrador|Os membros podem fazer modificações ao esquema modelo e podem consultar todos os dados no designer de modelo, do cliente de relatório e do SSMS.|Filtros de linha não são aplicáveis. Todos os dados podem ser consultados nesta função.|  
  
##  <a name="bkmk_rowfliters"></a> Row filters  
 Os filtros de linha definem quais linhas em uma tabela podem ser consultados por membros de uma função específica. Os filtros de linha são definidos para cada tabela em um modelo usando fórmulas DAX.  
  
 Os filtros de linha podem ser definidos somente para funções com permissões de Leitura e Leitura e Processo. Por padrão, se um filtro de linha não for definido para uma tabela específica, os membros de uma função que têm permissão de Leitura ou Leitura e Processo poderão consultar todas as linhas na tabela a menos que a filtragem cruzada seja aplicada de outra tabela.  
  
 Quando um filtro de linha é definido para uma tabela específica, uma fórmula DAX, que deve ser avaliada como um valor TRUE/FALSE, define as linhas que poderão ser consultadas por membros daquela função específica. As linhas não incluídas na fórmula DAX não poderão ser consultadas. Por exemplo, para membros da função vendas, a tabela Customers com a linha seguinte expressão de filtros, *= Customers [Country] = "USA"* , os membros da função vendas, só poderão consultar clientes nos EUA.  
  
 Os filtros de linha aplicam-se às linhas especificadas e também a linhas relacionadas. Quando uma tabela tiver várias relações, os filtros aplicam segurança para a relação que está ativa. Os filtros de linha serão intersectados com outros filtros de linha definidos para tabelas relacionadas, por exemplo:  
  
|Table|Expressão DAX|  
|-----------|--------------------|  
|Região|=Region[Country]="USA"|  
|ProductCategory|= ProductCategory [Name] = "Bicicletas"|  
|Transações|=Transactions[Year]=2008|  
  
 O efeito líquido destas permissões na tabela de Transações é que os membros terão permissão de consultar as linhas de dados quando o cliente estiver nos EUA, e a categoria de produto for bicicletas e o ano for 2008. Os usuários não poderiam consultar nenhuma transação fora dos EUA ou nenhuma transação que não fosse bicicletas nem em 2008, a menos que fossem membros de outra função que concede estas permissões.  
  
 Você pode usar o filtro *=FALSE()* para negar acesso a todas as linhas para uma tabela inteira.  
  
### <a name="dynamic-security"></a>Segurança dinâmica  
 A segurança dinâmica é um modo de definir a segurança de nível de linha com base no nome de usuário do usuário conectado no momento ou a propriedade CustomData retornada de uma cadeia de conexão. A fim de implementar uma segurança dinâmica, você deve incluir em seu modelo uma tabela com valores de logon (nome de usuário do Windows) para usuários, assim como um campo que pode ser usado para definir uma permissão específica; por exemplo, uma tabela dimEmployees com uma ID de logon (domínio\nome de usuário) e também um valor de departamento para cada funcionário.  
  
 Para implementar uma segurança dinâmica, você pode usar as funções a seguir como parte de uma fórmula DAX para retornar o nome de usuário do usuário conectado atualmente ou a propriedade CustomData em uma cadeia de conexão:  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Função USERNAME (DAX)](/dax/username-function-dax)|Retorna o domínio\ nome de usuário do usuário conectado atualmente.|  
|[Função CUSTOMDATA (DAX)](/dax/customdata-function-dax)|Retorna a propriedade CustomData em uma cadeia de conexão.|  
  
 Você pode usar a função LOOKUPVALUE para retornar valores para uma coluna na qual o nome de usuário do Windows seja igual ao nome de usuário retornado pela função USERNAME ou uma cadeia de caracteres retornada pela função CustomData. As consultas podem ser então restritas onde os valores retornados por LOOKUPVALUE correspondem a valores na mesma tabela ou na tabela relacionada.  
  
 Por exemplo, usando esta fórmula:  
  
 `='dimDepartmentGroup'[DepartmentGroupId]=LOOKUPVALUE('dimEmployees'[DepartmentGroupId], 'dimEmployees'[LoginId], USERNAME(), 'dimEmployees'[LoginId], 'dimDepartmentGroup'[DepartmentGroupId])`  
  
 A função LOOKUPVALUE retorna valores para a coluna dimEmployees[DepartmentId] onde dimEmployees[LoginId] é igual ao LoginID do usuário conectado no momento, retornado por USERNAME, e os valores para dimEmployees[DepartmentId] são iguais aos valores para dimDepartmentGroup[DepartmentId]. Os valores em DepartmentId retornados por LOOKUPVALUE são usados para restringir as linhas consultadas na tabela dimDepartment, e as tabelas relacionadas por DepartmentId. Somente são retornadas as linhas onde DepartmentId também esteja nos valores para o DepartmentId retornados pela função LOOKUPVALUE.  
  
 **dimEmployees**  
  
|LastName|FirstName|LoginID|DepartmentName|DepartmentId|  
|--------------|---------------|-------------|--------------------|------------------|  
|Brown|Kevin|Adventure-works\kevin0|Marketing|7|  
|Bradley|David|Adventure-works\david0|Marketing|7|  
|Dobney|JoLynn|Adventure-works\JoLynn0|Production|4|  
|Baretto DeMattos|Paula|Adventure-works\Paula0|Human Resources|2|  
  
 **dimDepartment**  
  
|DepartmentId|DepartmentName|  
|------------------|--------------------|  
|1|Corporate|  
|2|Executive General and Administration|  
|3|Inventory Management|  
|4|Manufacturing|  
|5|Quality Assurance|  
|6|Research and Development|  
|7|Sales and Marketing|  
  
##  <a name="bkmk_testroles"></a> Testing roles  
 Ao criar um projeto de modelo, você pode usar o recurso Analisar no Excel para testar a eficácia das funções que você definiu. No menu **Modelo** no designer de modelo, quando você clica em **Analisar no Excel**, antes de o Excel abrir, a caixa de diálogo **Escolher Credenciais e Perspectiva** é aberta. Nesta caixa de diálogo, você pode especificar o nome de usuário atual, um nome de usuário diferente, uma função e uma perspectiva que você usará para se conectar ao modelo de workspace como uma fonte de dados. Para obter mais informações, consulte [Analisar no Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_rt"></a> Related tasks  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Criar e gerenciar funções](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)|As tarefas neste tópico descrevem como criar e gerenciar funções usando a caixa de diálogo **Gerenciador de Funções** .|  
  
## <a name="see-also"></a>Consulte também  
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Analisar no Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [Função USERNAME (DAX)](/dax/username-function-dax)   
 [Função LOOKUPVALUE (DAX)](/dax/lookupvalue-function-dax)   
 [Função CUSTOMDATA (DAX)](/dax/customdata-function-dax)  
  
  
