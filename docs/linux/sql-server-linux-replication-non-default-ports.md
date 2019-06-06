---
title: Configurar o compartilhamento de pasta instantâneo de replicação do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve como configurar a replicação de SQL Server de compartilhamentos de pasta de instantâneo no Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4fd7c819af4c700af17a4b85fad2a4cc75e3e820
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705138"
---
# <a name="configure-replication-with-non-default-ports"></a>Configurar a replicação com portas não padrão

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode configurar a replicação com o SQL Server em instâncias de Linux que escuta em qualquer porta configurada com a configuração de mssql-conf network.tcpport. A porta deve ser acrescentado ao nome do servidor durante a configuração se as seguintes condições forem verdadeiras:

1. Configuração de replicação envolve uma instância do SQL Server no Linux
2. Qualquer instância (Windows ou Linux) está escutando uma porta não padrão. 

O nome do servidor de uma instância pode ser encontrado executando @@servername na instância.

## <a name="examples"></a>Exemplos

'Server1' escuta na porta 1500 no Linux. Para configurar 'Server1' para distribuição, execute `sp_adddistributor` com `@distributor`. Por exemplo: 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' escuta na porta 1500 no Linux. Para configurar um publicador para o distribuidor, execute `sp_adddistpublisher` com `@publisher`. Por exemplo:

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

'Server2' escuta na porta 6549 no Linux. Para configurar 'Server2' como um assinante, execute `sp_addsubscription` com `@subscriber`. Por exemplo:

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Servidor3' escuta na porta 6549 no Windows com o nome do servidor do servidor3 e o nome da instância do MSSQL2017. Para configurar 'Servidor3' como um assinante, execute as `sp_addsubscription` com `@subscriber`. Por exemplo:

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>Próximas etapas

[Conceitos: Replicação do SQL Server no Linux](sql-server-linux-replication.md)

[Procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

