---
title: Definir as opções de projeto (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f325a606-97ac-48bc-b344-b55f5e086a48
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 16bf79c185a23399d48d141b5d773e2e0d41dc3f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269993"
---
# <a name="setting-project-options-db2tosql"></a>Definir opções do projeto (DB2ToSQL)
Para cada projeto do SSMA, você pode definir opções de nível de projeto. Essas opções especificam a conversão do objeto, o carregamento do objeto, configurações de migração de dados e interface do usuário. Antes de converter objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou migrar os dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se as opções de configuração são adequadas para o projeto.  
  
O SSMA permite configurar opções padrão para todos os projetos. Essas opções são aplicadas a qualquer novo projeto criado por você. Em seguida, você pode personalizar as opções para cada projeto.  
  
## <a name="configuration-options-and-modes"></a>Modos e opções de configuração  
O SSMA tem cinco conjuntos de configurações do projeto:  
  
-   Informações do projeto  
  
-   Geral (conversão ou migração, carregando objetos)  
  
-   Synchronization  
  
-   GUI  
  
-   Mapeamento de tipo  
  
Ele também tem quatro modos para definir essas configurações:  
  
-   Padrão  
  
-   Otimistas  
  
-   Completo  
  
-   Personalizar  
  
O modo padrão é recomendado para a maioria dos usuários. O modo otimista mantém mais da sintaxe do DB2 atual e é mais fácil de ler. No entanto, a manter a sintaxe atual pode não ser precisa. Se a sintaxe do DB2 deve ser convertida ao equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe, o modo completo executa a conversão mais completa, mas o código resultante pode ser mais difícil de ler. No modo personalizado, você deve definir as opções.  
  
Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os tópicos a seguir:  
  
-   [Configurações do projeto &#40;conversão&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)  
  
-   [Configurações do projeto &#40;migração&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md)  
  
-   [Configurações do projeto&#40;sincronização&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)  
  
-   [Configurações do projeto &#40;interface gráfica do usuário&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)  
  
-   [Configurações do projeto &#40;mapeamento de tipo&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)  
  
## <a name="setting-project-options"></a>Definir opções do projeto  
No SSMA, você pode configurar as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto criado por você.  
  
**Para definir opções de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, clique em **configurações do projeto padrão**.  
  
2.  No **configurações de projeto padrão** caixa de diálogo, use um dos procedimentos a seguir:  
  
    -   Selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida ou alterada de **versão de destino de migração** lista suspensa clique **geral** na parte inferior do painel esquerdo e, em seguida, selecione conversão ou Migração.  
  
    -   Para selecionar um modo predefinido, nos **modo** caixa de lista suspensa, selecione **padrão**, **Optimistic**, ou **completo**.  
  
    -   Para especificar configurações personalizadas, selecione ou insira as novas configurações ou valores.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
Você também pode personalizar configurações para o projeto atual. Essas configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações para o projeto atual**  
  
1.  Sobre o **ferramentas** menu, clique em **configurações do projeto**.  
  
2.  No **configurações do projeto** caixa de diálogo, use um dos procedimentos a seguir:  
  
    -   Para selecionar um modo predefinido, nos **modo** caixa de lista suspensa, selecione **padrão**, **Optimistic**, ou **completo**.  
  
    -   Para especificar um modo personalizado, na **modo** caixa, selecione **personalizado**e, em seguida, selecione as configurações de projeto apropriado.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento de tipos de dados de origem e destino, consulte [DB2 de mapeamento e tipos de dados do SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
-   Caso contrário, você pode converter as definições de objeto de banco de dados do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto. Para obter mais informações, consulte [converter esquemas do DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Mapeamento de DB2 e tipos de dados do SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)  
  
