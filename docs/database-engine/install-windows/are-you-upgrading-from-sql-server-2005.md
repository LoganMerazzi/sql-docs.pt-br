---
title: Você está atualizando do SQL Server 2005, 2008 ou 2008R2? | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ad40e66f-71fe-4ee6-9ce3-17127e7b1d7a
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 62389a315befed467497f87dd3b86c3f52171e91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051215"
---
# <a name="are-you-upgrading-from-sql-server-2005-2008-or-2008r2"></a>Você está atualizando do SQL Server 2005, 2008 ou 2008R2?

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 O fim do suporte estendido para o SQL Server é um motivo para atualizar agora para uma versão mais recente do SQL Server e do Banco de Dados SQL do Azure. A atualização permite manter a segurança e a conformidade, alcançar um desempenho inovador e otimizar a infraestrutura da plataforma de dados.  
  
 Para obter mais informações, diretrizes e ferramentas para planejar e automatizar sua migração ou atualização, confira [Fim do suporte do SQL Server 2005](https://www.microsoft.com/sql-server/sql-server-2005) e [Fim do suporte do SQL Server 2008](https://www.microsoft.com/cloud-platform/windows-sql-server-2008).  
  
## <a name="why-upgrade"></a>Por que atualizar?  
  
> [!IMPORTANT]  
>  O suporte estendido para o SQL Server 2005 terminou em 12 de abril de 2016. Se você ainda estiver executando o SQL Server 2005 após 12 de abril de 2016, deixará de receber atualizações de segurança.  

> [!IMPORTANT]  
>  O suporte estendido para o SQL Server 2008 e 2008r2 terminou em 9 de julho de 2019. Se ainda estiver executando o SQL Server 2008 ou 2008R2 depois de 9 de abril de 2019, você deixará de receber atualizações de segurança. Mais informações podem ser encontradas no blog [Anunciando novas opções para o SQL Server 2008](https://azure.microsoft.com/blog/announcing-new-options-for-sql-server-2008-and-windows-server-2008-end-of-support/). Para estender o suporte gratuitamente, você pode migrar o SQL Server para uma VM do Azure. Para saber mais, confira [Estender o suporte para SQL Server 2008 e 2008 R2 com o Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support).  
  
## <a name="choose-your-upgrade-option"></a>Escolher sua opção de atualização  
Se você estiver atualizando bancos de dados relacionais de uma versão antiga do SQL Server, aqui estarão as opções para armazenamento relacional na plataforma Microsoft.  
  
Para ver uma análise mais abrangente dessas opções, confira [PaaS versus IaaS](/azure/sql-database/sql-database-paas-vs-sql-server-iaas).  
  
|Opção de armazenamento relacional|Benefícios|Outros fatores a considerar|  
|-------------------------------|--------------|-------------------------------|  
|**SQL Server hospedado em máquinas virtuais do Azure**<br /><br /> Considere essa opção se você quiser o seguinte:<br /><br /> Benefícios da migração para um ambiente hospedado.<br /><br /> Controle sobre o ambiente operacional.<br /><br /> Conjunto de recursos familiares do SQL Server.|**Você pode [estender o suporte](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support) para o SQL Server 2008 e 2008 R2 gratuitamente por até três anos.** <br /><br /> Você pode implantar rapidamente de uma biblioteca de imagens de máquinas virtuais.<br /><br /> Obtenha o conjunto completo de recursos do SQL Server.<br /><br /> Você economiza o custo de hardware e do software para servidores. Você paga apenas pelo uso por hora.|Você precisa gerenciar o SQL Server e o software do sistema operacional.<br /><br /> <br /><br /> Para saber mais, confira [Visão geral do SQL Server em máquinas virtuais do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).<br /><br /> Para obter informações sobre a migração, consulte [Migrar um banco de dados para o SQL Server em uma VM do Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/).|  
|**Instância gerenciada do Banco de Dados SQL do Azure (PaaS)** <br /><br /> Considere esta opção se você quiser uma solução de baixo custo com menos manutenção.<br /><br /> Uma instância gerenciada é semelhante a uma instância do mecanismo de banco de dados do Microsoft SQL Server, oferecendo recursos compartilhados para bancos de dados e recursos adicionais no escopo da instância. <br /><br />A instância gerenciada dá suporte à migração de banco de dados do local com pouca ou nenhuma alteração ao banco de dados.|Obtenha o benefício de consultas entre bancos de dados dentro da mesma instância gerenciada, bem como suporte de trabalhos do SQL e CLR. <br /><br /> Disponibilidade garantida de 99,995%.<br /><br /> O custo do serviço inclui não apenas o armazenamento, mas também a alta disponibilidade, aplicações de patches e backups automáticos.|Há algumas diferenças no Transact-SQL (T-SQL) entre a instância gerenciada de Bancos de Dados SQL do Azure e do SQL Server local. Para saber mais, veja [Informações sobre o T-SQL em instância gerenciada do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-managed-instance-transact-sql-information).<br /><br /> Para saber mais sobre a instância gerenciada do Banco de Dados SQL do Azure, veja [Visão geral sobre a instância gerenciada do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-managed-instance-index) e [Funcionalidades da instância gerenciada do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-managed-instance).<br /><br /> Para saber mais sobre a migração, confira [Migração de um SQL Server para uma instância gerenciada do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-managed-instance-migrate).|  
|**Banco de dados individual ou pool elástico do Banco de Dados SQL do Azure (PaaS)** <br /><br /> Considere esta opção se você quiser uma solução de baixo custo com menos manutenção.<br /><br /> Essa opção é especialmente adequada para aplicativos desenvolvidos para a nuvem quando a produtividade do desenvolvedor e o rápido tempo para a comercialização das novas soluções forem críticos ou se houver a necessidade de fornecer acesso externo. <br /><br />Os recursos do SQL Server geralmente mais usados estão disponíveis, mas não são tantos como para uma instância gerenciada do Banco de Dados SQL do Azure. |Você pode implantar rapidamente e escalar verticalmente com facilidade.<br /><br /> Disponibilidade garantida de 99,995%.<br /><br /> Você pode pagar o uso por segundo ou por hora. <br /><br /> O custo do serviço inclui não apenas o armazenamento, mas também a alta disponibilidade, aplicações de patches e backups automáticos.|Há algumas diferenças no Transact-SQL (T-SQL) entre o Bancos de Dados SQL do Azure e o SQL Server local. Para obter mais informações, veja [Informações do Transact-SQL do Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/).<br /><br /> O Banco de Dados SQL do Azure também tem um tamanho máximo de 100 TB, em comparação com 524 PB para o SQL Server. Para obter mais informações, confira [Limites de recurso para bancos de dados individuais](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)<br /><br /> Para obter mais informações sobre o Banco de Dados SQL, confira a [visão geral do Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/) e a [documentação do Banco de Dados SQL do Azure](/azure/sql-database/sql-database-technical-overview).<br /><br /> Para saber mais sobre a migração, confira [Migração de um banco de dados do SQL Server para um banco de dados SQL do Azure](/azure/sql-database/sql-database-single-database-migrate).|  
|**SQL Server no local**<br /><br /> Considere esta opção para aplicativos de banco de dados de qualquer tipo, desde sistemas transacionais até data warehouses.|Você tem o máximo de controle sobre recursos e escalabilidade porque você gerencia tanto o hardware quanto o software.<br /><br /> Se estiver atualizando por meio de uma instância antiga do SQL Server, esse será o ambiente mais semelhante.|Você precisa fazer o maior investimento inicial e fornecer o gerenciamento mais contínuo, pois você precisa comprar, manter e gerenciar seu próprio hardware e software.<br /><br /> Para obter mais informações, consulte [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm).|  

Você também pode desejar considerar uma solução não relacional ou NoSQL para determinados aplicativos e dados.  
  
|Solução não relacional|Benefícios|  
|------------------------------|--------------|  
|**Azure Cosmos DB**<br /><br /> Considere esta opção para aplicativos Web modernos, escalonáveis e móveis que usam dados JSON e exigem uma combinação de consultas robustas e processamento de dados transacional.<br /><br /> Para obter mais informações, consulte [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).<br /><br /> Para obter informações sobre como importar dados, consulte [Importar dados para o Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/import-data/).|Os documentos são indexados e você pode usar uma sintaxe SQL familiar para consultá-los.<br /><br /> O banco de dados é livre de esquemas.<br /><br /> Você pode adicionar propriedades aos documentos sem precisar recompilar índices.<br /><br /> Você obtém suporte ao JSON e ao JavaScript dentro do mecanismo de banco de dados.<br /><br /> Você obtém suporte nativo para dados geoespaciais e integração com outros serviços do Azure, incluindo Pesquisa do Azure, HDInsight e Data Factory.<br /><br /> Obtenha armazenamento de baixa latência e alto desempenho com níveis de produtividade reservados.|  
|**Armazenamento de tabela do Azure**<br /><br /> Considere esta opção para armazenar petabytes de dados semiestruturados em uma solução econômica.<br /><br /> Para obter mais informações, consulte o [Armazenamento de Tabela](https://azure.microsoft.com/services/storage/tables/).|Você pode evoluir seus aplicativos e seu esquema de tabela sem colocar os dados offline.<br /><br /> Você pode escalar verticalmente sem fragmentar seu conjunto de dados.<br /><br /> Você obtém armazenamento com redundância geográfica que replica os dados por várias regiões.|  
  
## <a name="plan-your-upgrade"></a>Planejar sua atualização  
  
-   Leia sobre como planejar sua atualização da instância do SQL Server 2005 na seguinte série de postagens no blog da equipe do SQL Server. 
    - Planejamento de uma atualização eficiente do SQL Server 2005: [Etapa 1 de 3](https://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx), [Etapa 2 de 3](https://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx), [Etapa 3 de 3](https://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)
- Prepare-se para o [fim do suporte do SQL Server 2008](https://www.microsoft.com/sql-server/sql-server-2008).
  
-   Examine os requisitos e as considerações em [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md), incluindo os [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Leia sobre como atualizar.  
  
    -   Analise os métodos de atualização disponíveis e saiba como planejar e testar no artigo [Atualizar Mecanismo de Banco de Dados](../../database-engine/install-windows/upgrade-database-engine.md).  
  
        > [!IMPORTANT]  
        >- Não é possível fazer upgrade de uma instância do SQL Server 2005 para um servidor do SQL Server 2017 in-loco. É necessário instalar uma instância do SQL Server 2017 e, em seguida, migrar os bancos de dados do SQL Server 2005 para a nova instalação. Para saber mais, confira a seção "Nova Atualização da Instalação" no artigo [Escolher um Método de Atualização de Mecanismo de Banco de Dados](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
        >- É possível atualizar o SQL 2008 e o SQL 2008R2 do SQL em vigor para o SQL 2017. Para obter mais informações, confira [Atualizações de versão e edição com suporte](supported-version-and-edition-upgrades-2017.md). 


-    Para obter mais informações, diretrizes e ferramentas para planejar e automatizar sua migração ou atualização, confira [Fim do suporte do SQL Server 2005](https://www.microsoft.com/sql-server/sql-server-2005) e [Fim do suporte do SQL Server 2008](https://www.microsoft.com/cloud-platform/windows-sql-server-2008).  
  
## <a name="get-sql-server"></a>Obtenha o SQL Server  
 Para baixar uma cópia de avaliação do SQL Server, confira [downloads do SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).  
  
## <a name="next-steps"></a>Next Steps  
 [SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017)   
 [Fim do suporte do SQL Server 2005](https://www.microsoft.com/sql-server/sql-server-2005)   
 [Fim do suporte do SQL Server 2008](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)
  
  
