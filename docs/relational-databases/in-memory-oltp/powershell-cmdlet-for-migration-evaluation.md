---
title: Cmdlet do PowerShell para avaliação de migração | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 769948242c747abdfb1fd6e32606df6a5800a9bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054438"
---
# <a name="powershell-cmdlet-for-migration-evaluation"></a>Cmdlet do PowerShell para Avaliação da Migração
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O cmdlet Save-SqlMigrationReport é uma ferramenta que avalia a adequação da migração de vários objetos em um banco de dados do SQL Server. Atualmente, ele é limitado pela avaliação da adequação da migração para o OLTP na Memória. O cmdlet pode ser executado em um ambiente do Windows PowerShell com privilégios elevados e no sqlps.  
  
## <a name="syntax"></a>Sintaxe  
  
```powershell  
Save-SqlMigrationReport [ -MigrationType OLTP ] [ -Server server -Database database [ -Object object_name ] ]  |  [ -InputObject smo_object ] -FolderPath path  
```  
  
#### <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros.  
  
|Parâmetros|Descrição|  
|----------------|-----------------|  
|MigrationType|O tipo de cenário de migração que o cmdlet tem como destino. Atualmente, o único valor é o OLTP padrão. Opcional.|  
|Servidor|O nome da instância do SQL Server de destino. Obrigatório no ambiente do Windows Powershell, se o parâmetro - InputObject não for fornecido. Opcional no SQLPS.|  
|banco de dados|O nome do banco de dados do SQL Server de destino. Obrigatório no ambiente do Windows Powershell, se o parâmetro - InputObject não for fornecido. Opcional no SQLPS.|  
|Object|O nome do objeto de banco de dados de destino. Pode ser uma tabela ou um procedimento armazenado.|  
|InputObject|O objeto SMO que o cmdlet deve ter como destino. Obrigatório no ambiente do Windows Powershell, se -Server e -Database não forem fornecidos. Opcional no SQLPS.|  
|FolderPath|A pasta em que o cmdlet deve colocar os relatórios gerados. Obrigatórios.|  
  
## <a name="results"></a>Resultados  
 Na pasta especificada no parâmetro – FolderPath, haverá dois nomes de pasta: Tabelas e procedimentos armazenados. Se o objeto de destino for uma tabela, o relatório estará na pasta Tables. Caso contrário, ele estará na pasta Stored Procedures.  
  
  
