---
title: Exibir ou modificar as propriedades de uma condição de gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view policy conditions
- Policy-Based Management, modify policy conditions
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 340423e23037ae401b1e5749fbed38b1822cfb41
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62677016"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-condition"></a>Exibir ou modificar as propriedades de uma condição de gerenciamento baseado em políticas
  Este tópico descreve como exibir ou modificar as propriedades de uma condição de gerenciamento baseado em políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir ou modificar propriedades de uma condição, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-modify-a-conditions-properties"></a>Para exibir ou modificar as propriedades de uma condição  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém a condição que você deseja exibir ou modificar.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique no sinal de adição para expandir a pasta **Condições** .  
  
5.  Clique com o botão direito do mouse na condição que você deseja exibir ou editar e selecione **Propriedades**. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Abrir Condição -** _nome_da_condição_, confira [Caixa de diálogo Criar Condição ou Abrir Condição, página Geral](../../integration-services/general-page-of-integration-services-designers-options.md), [Caixa de diálogo Abrir Condição, página Políticas Dependentes](open-condition-dialog-box-dependent-policies-page.md), [Caixa de diálogo Criar Condição ou Abrir Condição, página Descrição](create-new-condition-or-open-condition-dialog-box-description-page.md) e [Caixa de diálogo Edição Avançada &#40;Condição&#41;](advanced-edit-condition-dialog-box.md).  
  
6.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-a-conditions-properties"></a>Para exibir as propriedades de uma condição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       description,  
       facet,  
       expression,  
       is_name_condition,  
       obj_name  
    FROM syspolicy_conditions;  
    GO  
  
    ```  
  
 Para obter mais informações, veja [syspolicy_conditions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syspolicy-conditions-transact-sql).  
  
  
