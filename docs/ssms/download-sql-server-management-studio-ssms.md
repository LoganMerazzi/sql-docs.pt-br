---
title: Baixar o SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
ms.technology: ssms
ms.topic: conceptual
keywords:
- instalar ssms, baixar ssms, ssms mais recentes
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- instalação do SQL management studio
- baixar o sql management studio
- ms sql management studio
- instalar o sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dnethi
ms.author: dinethi
manager: craigg
ms.openlocfilehash: 9bc678f69df60ec07e1cca6eddbb337aab8ed8ff
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042023"
---
# <a name="download-sql-server-management-studio-ssms"></a>Baixar o SQL Server Management Studio (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

O SSMS (SQL Server Management Studio) é um ambiente integrado para gerenciar qualquer infraestrutura de SQL, do SQL Server para o Banco de Dados SQL do Azure. O SSMS fornece ferramentas para configurar, monitorar e administrar instâncias do SQL Server e bancos de dados. Use o SSMS para implantar, monitorar e atualizar os componentes da camada de dados usados pelos seus aplicativos, além de construir consultas e scripts.

Use o SSMS para consultar, criar e gerenciar seus bancos de dados e data warehouses, independentemente de onde estiverem – no computador local ou na nuvem.

O SSMS é gratuito!

[O SSMS 18.0 RC1 (Release Candidate 1) já está disponível](#ssms-180-rc1) e é a última geração do *SQL Server Management Studio* que dá suporte ao [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="ssms-1791-is-the-current-general-availability-ga-version-of-ssms"></a>O SSMS 17.9.1 é a atual versão de GA (disponibilidade geral) do SSMS

[![daixar](../ssdt/media/download.png) Baixar o SQL Server Management Studio 17.9.1](https://go.microsoft.com/fwlink/?linkid=2043154)

[![daixar](../ssdt/media/download.png) Baixar o pacote de atualização do SQL Server Management Studio 17.9.1 (atualiza o 17.x para o 17.9.1)](https://go.microsoft.com/fwlink/?linkid=2043430)

**Informações sobre versão**

- Número da versão: 17.9.1<br>
- Número de build: 14.0.17289.0<br>
- Data de lançamento: 21 de novembro de 2018

### <a name="available-languages-ssms-1791"></a>Idiomas disponíveis (SSMS 17.9.1)

> [!NOTE]
> Versões do SSMS 17.x localizadas em idiomas diferentes do inglês exigem o [pacote de atualização de segurança KB 2862966](https://support.microsoft.com/kb/2862966) se instaladas em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)

Para obter mais detalhes sobre o SSMS 17.9.1, confira o [Log de alterações do SSMS 17.9.1](release-notes-ssms.md#1791-latest-ga-release).

## <a name="ssms-installation-tips-and-issues-ssms-1791"></a>Problemas e dicas de instalação do SSMS (SSMS 17.9.1)

### <a name="minimize-installation-reboots"></a>Minimizar as reinicializações de instalação

* Execute as seguintes ações para reduzir as chances de que a instalação do SSMS exija uma reinicialização no final da instalação:
  * Verifique se você está executando uma versão atualizada do pacote redistribuível do Visual C++ 2013. A versão 12.0.40649.5 (ou superior) é necessária. Apenas a versão x64 é necessária.
  * Verifique se a versão do .NET Framework no computador é a 4.6.1 (ou superior).
  * Feche todas as instâncias do Visual Studio que estão abertas no computador.
  * Verifique se todas as atualizações mais recentes do sistema operacional estão instaladas no computador.
  * As ações indicadas geralmente são necessárias uma única vez. Há alguns casos em que uma reinicialização é necessária durante as atualizações adicionais para a mesma versão principal do SSMS. Para obter atualizações secundárias, todos os pré-requisitos do SSMS já estão instalados no computador.

## <a name="ssms-180-rc1"></a>SSMS 18.0 (RC1)

**O SSMS 18.0 RC1 (Release Candidate 1) já está disponível e é a última geração do *SQL Server Management Studio* que dá suporte ao [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]!**

**[![dowaixar](../ssdt/media/download.png) Baixar o SQL Server Management Studio (18.0 RC1)](https://go.microsoft.com/fwlink/?linkid=2085742)**

O *RC1* é a mais recente versão prévia pública do SSMS 18.0. Se você tiver uma versão prévia anterior do SSMS 18.0 instalada, desinstale-a antes de instalar o SSMS 18.0 RC1.

**Informações sobre versão**

- Número da versão: 18.0 (RC1)<br>
- Número de build: 15.0.18098.0<br>
- Data de lançamento: 28 de março de 2019

Se você tem sugestões ou comentários ou deseja relatar problemas, a melhor maneira de entrar em contato com a equipe do SSMS é usando o [UserVoice](https://aka.ms/sqlfeedback).

A instalação do SSMS 18.x não atualiza nem substitui versões do SSMS 17.x ou anteriores. O SSMS 18.x é instalado lado a lado com versões anteriores para que ambas versões estejam disponíveis para uso.

Se um computador contiver instalações lado a lado do SSMS, verifique se você iniciou a versão correta para suas necessidades específicas. A versão mais recente é rotulada **Microsoft SQL Server Management Studio 18**:
 
## <a name="available-languages-ssms-180-rc1"></a>Idiomas disponíveis (SSMS 18.0 RC1)

Esta versão do SSMS pode ser instalada nos seguintes idiomas:

SQL Server Management Studio 18.0 (RC1):<br>
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x40a)

Pacote de atualização do SQL Server Management Studio 18.0 (atualiza para o 18.0):<br>
Nenhuma opção de atualização está disponível neste momento. Se você tiver uma versão prévia anterior do SSMS 18.0 instalada, desinstale-a antes de instalar o SSMS 18.0 RC1.

> [!NOTE]
> O módulo do SQL Server PowerShell é uma instalação separada por meio da Galeria do PowerShell. Para obter mais informações, consulte [Baixar o Módulo SQL Server PowerShell](download-sql-server-ps-module.md).

## <a name="new-in-this-release-ssms-180-rc1"></a>Novo nesta versão (SSMS 18.0 RC1)

O SSMS 18.0 (RC1) é a versão mais recente do SQL Server Management Studio. A geração 18.x do SSMS dá suporte a quase todas as áreas de recursos do SQL Server 2008 por meio da versão prévia do SQL Server 2019.

Para obter detalhes sobre as novidades desta versão, confira [notas sobre a versão do SSMS](release-notes-ssms.md).

## <a name="supported-sql-offerings-ssms-180-rc1"></a>Ofertas de SQL compatíveis (SSMS 18.0 RC1)

* Esta versão do SSMS funciona com todas as [versões com suporte do SQL Server 2008 – [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e SQL Data Warehouse do Azure.
* Além disso, o SSMS 18.x pode ser instalado lado a lado com o SSMS 17.x, o SSMS 16.x ou o SSMS do SQL Server 2014 e anteriores.
* SSIS (SQL Server Integration Services) – a versão SSMS 17.x ou posterior não permite a conexão com o serviço herdado do SQL Server Integration Services. Para conectar-se a uma versão anterior do Integration Services herdado, use a versão do SSMS alinhada com a versão do SQL Server. Por exemplo, use o SSMS 16.x para conectar ao serviço herdado do SQL Server Integration Services 2016. O SSMS 17.x e o SSMS 16.x podem ser instalados lado a lado no mesmo computador. Desde o lançamento do SQL Server 2012, o banco de dados de catálogo do SSIS, o SSISDB, é a maneira recomendada para armazenar, gerenciar, executar e monitorar os pacotes do Integration Services. Para obter detalhes, veja o [Catálogo do SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-180-rc1"></a>Sistemas operacionais compatíveis (SSMS 18.0 RC1)

Esta versão do SSMS é compatível com as seguintes plataformas de 64 bits quando usada com o service pack mais recente disponível:

- Windows 10 (64-bit) <sup>*</sup>
- Windows Server 2016 <sup>*</sup>
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

<sup>*</sup> Exige a versão 1607 (10.0.14939) ou posterior

> [!NOTE]
> O SSMS é executado somente no Windows. Se você precisar de uma ferramenta que seja executada em plataformas diferentes do Windows, confira o Azure Data Studio. O Azure Data Studio é uma nova ferramenta multiplataforma executada no macOS, no Linux e no Windows. Para obter detalhes, veja [Azure Data Studio](../azure-data-studio/what-is.md).
  
## <a name="release-notes-ssms-180-rc1"></a>Notas sobre a versão (SSMS 18.0 RC1)

N/A

## <a name="previous-releases"></a>Versões anteriores

[Versões anteriores do SQL Server Management Studio](../ssms/release-notes-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>Comentários

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Fórum das ferramentas de cliente do SQL](https://social.msdn.microsoft.com/Forums/home?forum=sqltools)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="see-also"></a>Consulte Também

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentação do SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Pacotes de serviço e atualizações adicionais](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

Se você tem sugestões ou comentários ou deseja relatar problemas, a melhor maneira de entrar em contato com a equipe do SSMS é usando o [UserVoice](https://aka.ms/sqlfeedback).
