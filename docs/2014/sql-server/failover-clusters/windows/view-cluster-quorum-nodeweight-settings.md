---
title: Exibir configurações de NodeWeight de quorum de cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: b845e73a-bb01-4de2-aac2-8ac12abebc95
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bab64e8a33baae2c87e8068a1e4d23799742b55c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049372"
---
# <a name="view-cluster-quorum-nodeweight-settings"></a>Exibir configurações de NodeWeight de quorum de cluster
  Este tópico descreve como exibir configurações de NodeWeight para cada nó de membro em um cluster WSFC (Windows Server Failover Clustering). As configurações de NodeWeight são usadas durante a votação de quorum para dar suporte à recuperação de desastre e a cenários com várias sub-redes para instâncias de cluster de failover do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Antes de iniciar:**  [Pré-requisitos](#Prerequisites), [Segurança](#Security)  
  
-   **Para exibir as configurações de NodeWeight de quorum usando:** [Usando o Transact-SQL](#TsqlProcedure), [Usando o PowerShell](#PowerShellProcedure), [Usando Cluster.exe](#CommandPromptProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de iniciar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Esse recurso somente tem suporte no [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] ou em versões posteriores.  
  
> [!IMPORTANT]  
>  Para usar configurações de NodeWeight, é necessário aplicar o seguinte hotfix para todos os servidores no cluster WSFC:  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036): Um hotfix está disponível para permitir que você configure um nó de cluster que não tem votos de quorum em [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e, em [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
> [!TIP]  
>  Se esse hotfix não for instalado, os exemplos neste tópico retornarão valores vazios ou NULL para NodeWeight.  
  
###  <a name="Security"></a> Segurança  
 O usuário deve ser uma conta de domínio que seja membro do grupo Administradores local em cada nó do cluster WSFC.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
##### <a name="to-view-nodeweight-settings"></a>Para exibir configurações de NodeWeight  
  
1.  Conecte-se a qualquer instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no cluster.  
  
2.  Consulte a exibição [sys].[dm_hadr_cluster_members].  
  
### <a name="example-transact-sql"></a>Exemplo (Transact-SQL)  
 O exemplo a seguir consulta um modo de exibição do sistema para retornar valores para todos os nós no cluster dessa instância.  
  
```sql  
SELECT  member_name, member_state_desc, number_of_quorum_votes  
 FROM   sys.dm_hadr_cluster_members;  
```  
  
##  <a name="PowerShellProcedure"></a> Usando o Powershell  
  
##### <a name="to-view-nodeweight-settings"></a>Para exibir configurações de NodeWeight  
  
1.  Inicie um Windows PowerShell elevado via **Executar como Administrador**.  
  
2.  Importe o módulo `FailoverClusters` para habilitar commandlets de cluster.  
  
3.  Use o objeto `Get-ClusterNode` para retornar uma coleção de objetos de nó de cluster.  
  
4.  Gere as propriedades de nó de cluster em um formato legível.  
  
### <a name="example-powershell"></a>Exemplo (Powershell)  
 O exemplo a seguir gera algumas das propriedades de nó para o cluster chamado "Cluster001".  
  
```powershell  
Import-Module FailoverClusters  
  
$cluster = "Cluster001"  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> Usando Cluster.exe  
  
> [!NOTE]  
>  O utilitário cluster.exe foi preterido na versão [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] .  Use o PowerShell com Clustering de Failover para desenvolvimento futuro.  O utilitário cluster.exe será removido na próxima versão do Windows Server. Para obter mais informações, consulte [Mapeando comandos cluster.exe para cmdlets Windows PowerShell para clusters de failover](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx).  
  
##### <a name="to-view-nodeweight-settings"></a>Para exibir configurações de NodeWeight  
  
1.  Inicie um Prompt de Comando elevado via **Executar como Administrador**.  
  
2.  Usar **cluster.exe** para retornar o status do nó e valores de NodeWeight  
  
### <a name="example-clusterexe"></a>Exemplo (Cluster.exe)  
 O exemplo a seguir gera algumas das propriedades de nó para o cluster chamado "Cluster001".  
  
```ms-dos  
cluster.exe Cluster001 node /status /properties  
```  
  
## <a name="see-also"></a>Consulte também  
 [Configuração de modos de quorum WSFC e votação &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Definir configurações de NodeWeight de quorum de cluster](configure-cluster-quorum-nodeweight-settings.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)   
 [Cmdlets de cluster de failover no Windows PowerShell listados por foco de tarefa](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
