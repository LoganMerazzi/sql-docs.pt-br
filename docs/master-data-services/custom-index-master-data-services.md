---
title: Índice personalizado (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: c57bf8b8-55a6-4b6c-9adb-91b5f4f1ee3c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 546e04385490e725adfa0bb2f256109da7a0d55d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094429"
---
# <a name="custom-index-master-data-services"></a>Índice personalizado (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Índices personalizados criam um índice não clusterizado em um atributo (índice único) ou em uma lista de atributos (índice composto), em uma entidade. Geralmente os índices melhoram o desempenho do processo de consulta. Para obter mais informações sobre índices do SQL Server, consulte [Índices](../relational-databases/indexes/indexes.md).  
  
## <a name="type-of-indexes"></a>Tipos de índice  
 Você pode criar os seguintes tipos de vários índices personalizados para cada entidade.  
  
-   Índice exclusivo  
  
-   Índices não exclusivos  
  
 Um índice exclusivo garante que a coluna indexada não contenha valores duplicados. Para índices exclusivos compostos, o índice garante que cada combinação de valores na lista de atributos selecionados seja exclusiva. Um índice exclusivo não poderá ser criado se houver valores duplicados para os atributos selecionados.  
  
## <a name="rules"></a>Regras  
 As seguintes regras se aplicam a índices personalizados, exclusivos e não exclusivos.  
  
-   Para criar um índice personalizado, selecione pelo menos um atributo.  
  
-   Se você tentar salvar um índice que tem a mesma lista de atributos e o sinalizador de exclusividade como outro índice, o índice não poderá ser salvo. Um erro é exibido.  
  
    > [!NOTE]  
    >  O MDS cria índices automaticamente para determinados atributos (como DBAs e código). Isso significa que você não pode criar outro índice que contenha um desses atributos e nenhum outro atributo.  
  
-   Os atributos podem ser incluídos em mais de um índice personalizado, desde que haja pelo menos um atributo diferente nos outros índices. Caso contrário, os índices são os mesmos.  
  
-   Se você criar um índice que contém muitos atributos, ou atributos de tamanho grande e o tamanho total dos atributos selecionados exceder o tamanho máximo da chave de índice (900 bytes), o índice não poderá ser salvo.  
  
-   Um índice personalizado pode ser criado em atributos de membro folha, exceto atributos de arquivo.  
  
-   Se você quiser excluir um atributo que está incluído em um índice personalizado, o seguinte será aplicável.  
  
    -   Se o índice for criado em apenas um atributo (índice único), o atributo e o índice serão ambos excluídos.  
  
    -   Se o índice for criado em mais de um atributo (índice composto), o atributo não poderá ser excluído até você editar o índice.  
  
-   O tipo de um atributo que é incluído em um índice personalizado não pode ser alterado.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar um índice|[Criar um índice &#40;Master Data Services&#41;](../master-data-services/create-an-index-master-data-services.md)|  
|Editar e excluir um índice|[Editar e excluir um índice &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)|  
  
  
