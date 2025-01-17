---
title: Escolher um destino (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 746aed7f49b0db51f46a32fdf040eb5b9e968dd2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768019"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Escolher um destino (Assistente de Importação e Exportação do SQL Server)
  Use o **escolher um destino** página para especificar o destino dos dados que você deseja copiar.  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções para iniciar o assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Destino**  
 Escolha o provedor de dados que corresponde ao formato de armazenamento do destino. Pode haver mais de um provedor disponível para sua fonte de dados. Por exemplo, com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o .NET Framework Data Provider para SQL Server ou o Microsoft OLE DB Provider para SQL Server.  
  
> [!NOTE]  
>  Para salvar dados em um destino ODBC, selecione o Provedor de dados do .NET Framework para ODBC.  
  
 O **fonte de dados** propriedade tem um número variável de opções que mudam de acordo com os provedores instalados no computador. As tabelas a seguir listam as opções de alguns destinos usados com frequência. Para outros provedores, consulte a documentação específica do provedor.  
  
## <a name="dynamic-options"></a>Opções dinâmicas  
 As seções a seguir mostram as opções disponíveis para várias fontes de dados. Nem todos os destinos disponíveis no menu suspenso Destino são listados aqui.  
  
### <a name="destination--sql-server-native-client-or-microsoft-ole-db-provider-for-sql-server"></a>Destino = SQL Server Native Client ou Microsoft OLE DB Provider for SQL Server  
 **Nome do servidor**  
 Digite o nome do servidor que receberá os dados ou escolha um servidor da lista.  
  
 **Usar Autenticação do Windows**  
 Especifique se o pacote deve usar a Autenticação do Microsoft Windows para fazer login no banco de dados. A Autenticação do Windows é recomendada para obter melhor segurança.  
  
 **Usar Autenticação do SQL Server**  
 Especifique se o pacote deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer login no banco de dados. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **Nome de usuário**  
 Especifique um nome de usuário para estabelecer conexão com o banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Senha**  
 Forneça uma senha para estabelecer conexão de banco de dados quando estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Backup de banco de dados**  
 Selecione na lista de bancos de dados na instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou crie um novo banco de dados clicando **New**.  
  
 **Atualizar**  
 Restaure a lista de bancos de dados disponíveis clicando em **Atualizar**.  
  
 **Nova**  
 Criar um novo banco de dados de destino usando o **criar banco de dados** caixa de diálogo.  
  
### <a name="destination--flat-file-destination"></a>Destino = Destino de Arquivos Simples  
 **Nome do arquivo**  
 Especifique o caminho e o nome de arquivo do arquivo no qual deseja armazenar os dados. Se preferir, clique em **Procurar** para localizar um arquivo.  
  
 **Procurar**  
 Localize um arquivo usando a caixa de diálogo **Abrir**.  
  
 **Localidade**  
 Especifique a ID de localidade (LCID) que define as ordens de classificação de caracteres e a formatação de data e hora.  
  
 **Unicode**  
 Indique se deve ser usado o Unicode. Se decidir usá-lo, não será possível especificar uma página de códigos.  
  
 **Página de código**  
 Especifique a página de códigos da linguagem que deseja usar.  
  
 **Formato**  
 Indique se será usada formatação delimitada, de largura fixa ou irregular à direita.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por um delimitador, especificado na **colunas** página.|  
|Largura fixa|As colunas têm uma largura fixa.|  
|Irregular à direita|Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha.|  
  
 **Qualificador de texto**  
 Digite o qualificador de texto a ser usado. Por exemplo, você pode especificar que cada coluna de texto seja destacada com aspas.  
  
 **Nomes de coluna na primeira linha de dados**  
 Indique se você deseja exibir os nomes de coluna na primeira linha de dados.  
  
### <a name="destination--microsoft-excel"></a>Destino = Microsoft Excel  
  
> [!NOTE]  
>  Selecione **o Microsoft Excel** apenas se você quiser se conectar a uma fonte de dados que usa o Excel 2003 ou versões anteriores. Para se conectar a uma fonte de dados que usa o Excel 2007, selecione **Microsoft Office 12.0 Access Database Engine OLE DB Provider**, clique em **propriedades**e, em seguida, na **todos os** guia das **Propriedades de vínculo de dados** caixa de diálogo, para **propriedades estendidas**, insira `Excel 12.0`.  
  
 **Caminho de arquivo do Excel**  
 Especifique o nome de arquivo e caminho da pasta de trabalho no qual armazenar os dados (por exemplo, C:\MyData.xls, \\\Sales\Database\Northwind.xls). Ou, clique em **procurar** para localizar uma pasta de trabalho.  
  
 **Procurar**  
 Localize uma pasta de trabalho do Excel usando o **abrir** caixa de diálogo.  
  
 **Versão do Excel**  
 Selecione a versão do Excel que será usada pela pasta de trabalho de destino.  
  
> [!NOTE]  
>  Ao exportar dados a um destino do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)], o assistente utilizará o componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Excel Destination. Para obter informações sobre algumas considerações de uso e problemas conhecidos, consulte [destino do Excel](../data-flow/excel-destination.md).  
  
### <a name="destination--microsoft-access"></a>Destino = Microsoft Access  
  
> [!NOTE]  
>  Selecione **Microsoft Access** apenas se você quiser se conectar a um banco de dados que usa o Access 2003 ou versões anteriores. Para conectar a um banco de dados que usa o Access 2007, selecione **Microsoft Office 12.0 Access Database Engine OLE DB Provider**.  
  
 **Nome do arquivo**  
 Especifique o nome de arquivo e caminho para o arquivo de banco de dados no qual armazenar os dados (por exemplo, C:\MyData.mdb, \\\Sales\Database\Northwind.mdb). Ou, clique em **procurar** para localizar um arquivo de banco de dados.  
  
 **Procurar**  
 Navegue até o arquivo de banco de dados usando o **abrir** caixa de diálogo.  
  
 **Nome de usuário**  
 Especifique um nome de usuário válido para estabelecer conexão com o banco de dados quando houver um arquivo de informações do grupo de trabalho associado ao banco de dados.  
  
 **Senha**  
 Forneça a senha do usuário para estabelecer conexão quando o arquivo de informações do grupo de trabalho estiver associado ao banco de dados. No entanto, se o banco de dados estiver protegido com uma única senha para todos os usuários, você deve fornecer esse valor na **propriedades de vínculo de dados** caixa de diálogo que é acessada a partir de **avançado** botão.  
  
 **Avançado**  
 Especifique as opções avançadas, como a senha do banco de dados ou um arquivo de informações do grupo de trabalho não padrão, usando a caixa de diálogo **Propriedades de Vínculo de Dados**. Para obter mais informações sobre as propriedades do provedor OLE DB, pesquise na seção acesso a dados das [biblioteca MSDN](https://go.microsoft.com/fwlink/?linkid=62553).  
  
  
