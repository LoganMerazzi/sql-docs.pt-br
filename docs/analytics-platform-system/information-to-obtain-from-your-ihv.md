---
title: Obtenha informações do IHV - Analytics Platform System | Microsoft Docs
description: Informações a serem obtidas do IHV sobre o dispositivo do Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 016a20567968e45456be79c8c67e77d7c3fbb2bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960834"
---
# <a name="information-to-obtain-from-your-ihv"></a>Informações a serem obtidas do IHV
Quando o seu fornecedor independente de hardware (IHV) seu novo dispositivo de PDW do SQL Server para você, eles também fornecerá informações sobre o hardware do dispositivo e a configuração que eles executaram em seu dispositivo. Você precisará dessas informações para administrar seu dispositivo.  
  
A lista a seguir mostra informações normalmente necessárias do IHV. Em alguns casos, informações adicionais ou é necessário. Verifique com IHV para garantir que todas as informações relevantes foi transferidas para você com a entrega de dispositivo.  
  
|||  
|-|-|  
|**Informações ou documento**|**Descrição**|  
|Lista de materiais (BOM)|Lista de materiais lista os componentes que estão incluídos no seu dispositivo. Essas informações são necessárias para confirmar que todos os componentes foram entregues.<br /><br />**Importante:** Lista de materiais deve incluir os pesos para cada um de nós de dispositivo em cada rack completo. Essa informação é importante ao planejar como tratar e mover componentes do dispositivo e para verificar se seu data center pode acomodar o dispositivo. Se o seu BOM não inclui os pesos de nó, certifique-se de obter essas informações do IHV para todos os nós.|  
|Cabeamento de diagramas|Cabeamento diagramas mostram como se conectar a rede, energia e outros cabos para cada dispositivo do rack. Esses diagramas são necessários ao instalar o dispositivo em seu data center, e sempre que você precisa remover ou substituir um componente.|  
|Requisitos de acompanhamento de dispositivo|Antes de seu dispositivo pode ser instalado em seu data center, você precisa saber se seu data center atende o fluxo de ar e requisitos de comprimento de cabo para o dispositivo, bem como o tamanho e os requisitos de energia para os componentes. Consulte também lista de materiais (BOM) acima para obter informações sobre os pesos de componente do dispositivo, que também é necessário.|  
  
