---
title: Salvar metadados (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b2517735-dd19-449f-8cee-08e68ca89d3a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8bfe338c128ce301e98346d17ce00b973912ffd4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667513"
---
# <a name="save-metadata--sybasetosql"></a>Salvar metadados (SybaseToSQL)
O **salvar metadados** caixa de diálogo solicita que você carregar metadados em seu projeto do SSMA antes de salvá-lo. Isso permite que você tiver um arquivo de projeto completo que você pode usar offline e enviar a outras pessoas, como a equipe de suporte técnico.  
  
Para acessar o **salvar metadados** caixa de diálogo, salve o projeto. Se todos os metadados estiverem ausentes, o SSMA exibirá os **salvar metadados** caixa de diálogo.  
  
## <a name="options"></a>Opções  
**Nome**  
O nome de cada banco de dados no projeto.  
  
**Status**  
Indica se os metadados são carregados para o projeto do SSMA, ou se os metadados estiverem ausentes.  
  
O SSMA carrega os metadados para o projeto conforme necessário. Metadados são carregados automaticamente quando você procurar os metadados e converter esquemas.  
  
**Selecionar Tudo**  
Seleciona listados todos os bancos de dados.  
  
**Liberada**  
Desmarca a caixa de seleção para todos os bancos de dados com metadados ausentes. Você não pode desmarcar a caixa de seleção se metadados tiver sido carregado.  
  
**Salvar**  
Salva o projeto, carregar os metadados para bancos de dados selecionados que têm metadados ausentes.  
  
**Cancelar**  
Cancela o salvamento operação. Metadados ausentes não é carregado no projeto.  
  
