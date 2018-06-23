---
title: 'Lição 3: Criar uma credencial do SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 201863a1df64cdc85ef41a55170948dbf4eba419
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120348"
---
# <a name="lesson-3-create-a-sql-server-credential"></a>Lição 3: Criar uma credencial do SQL Server
  Nesta lição, você criará uma credencial para armazenar as informações de segurança usadas para acessar a conta de armazenamento do Windows Azure.  
  
 Uma credencial do SQL Server é um objeto usado para armazenar as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server. A credencial armazena o caminho de URI do contêiner de armazenamento e os valores de chave de assinatura de acesso compartilhado. Para cada contêiner de armazenamento usado por um arquivo de dados ou de log, você deve criar uma Credencial do SQL Server cujo nome corresponda ao caminho do contêiner.  
  
 Para obter informações gerais sobre credenciais, consulte [credenciais &#40;mecanismo de banco de dados&#41;](security/authentication-access/credentials-database-engine.md).  
  
> [!IMPORTANT]  
>  Os requisitos para a criação de uma credencial do SQL Server descrita abaixo são específicos para o [arquivos de dados do SQL Server no Windows Azure](databases/sql-server-data-files-in-microsoft-azure.md) recurso. Para obter informações sobre como criar credenciais para processos de backup no armazenamento do Azure, consulte [lição 2: criar uma credencial do SQL Server](../tutorials/lesson-2-create-a-sql-server-credential.md).  
  
 Para criar uma Credencial do SQL Server, execute estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  No Pesquisador de Objetos, conecte-se à instância do Mecanismo de Banco de Dados instalado.  
  
3.  Na barra de ferramentas Padrão, clique em Nova Consulta.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta, e modifique conforme necessário. A instrução a seguir criará uma Credencial do SQL Server para armazenar o Certificado de Acesso Compartilhado do contêiner de armazenamento.  
  
    ```tsql  
  
    USE master  
    CREATE CREDENTIAL credentialname – this name should match the container path and it must start with https.   
       WITH IDENTITY='SHARED ACCESS SIGNATURE', -- this is a mandatory string and do not change it.   
       SECRET = 'sharedaccesssignature' –- this is the shared access signature key that you obtained in Lesson 2.   
    GO  
  
    ```  
  
     Para obter informações detalhadas, consulte [CREATE CREDENTIAL &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-credential-transact-sql) nos Manuais Online do SQL Server.  
  
5.  Para ver todas as credenciais disponíveis, você pode executar a instrução a seguir na janela de consulta:  
  
    ```tsql  
    SELECT * from sys.credentials  
    ```  
  
     Para obter mais informações sobre Credentials, consulte [Credentials &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) nos Manuais Online do SQL Server.  
  
 **Próxima lição:**  
  
 [Lição 4: Criar um banco de dados no Armazenamento do Microsoft Azure](lesson-3-database-backup-to-url.md)  
  
  