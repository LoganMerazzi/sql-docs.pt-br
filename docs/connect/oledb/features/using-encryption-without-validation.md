---
title: Usando criptografia sem validação | Microsoft Docs
description: Usando criptografia sem validação
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 108aef449d80fa01e88fac29e6058754626b6aed
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802890"
---
# <a name="using-encryption-without-validation"></a>Usando criptografia sem validação
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sempre criptografa pacotes de rede associados a logon. Se nenhum certificado tiver sido provisionado no servidor quando ele foi inicializado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerará um certificado autoassinado usado para criptografar pacotes de login.  

Os certificados autoassinados não garante a segurança. O handshake criptografado é baseado no Gerenciador de NTLM (NT LAN). É altamente recomendável que você forneça um certificado verificável no SQL Server para uma conectividade segura. Camada de segurança de transporte (TLS) podem ser feitas segura somente com a validação do certificado.

Os aplicativos também podem solicitar a criptografia de todo o tráfego de rede usando palavras-chave de cadeia de conexão ou propriedades de conexão. As palavras-chave são "Encrypt" para o OLE DB ao usar uma cadeia de caracteres do provedor com **IDbInitialize::Initialize** ou "Use Encryption for Data" para o ADO e o OLE DB ao usar uma cadeia de caracteres de inicialização com **IDataInitialize**. Isso também pode ser configurado com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager usando o **Forçar criptografia de protocolo** opção e, configurando o cliente para solicitar conexões criptografadas. Por padrão, a criptografia de todo o tráfego de rede para uma conexão requer que um certificado seja aprovisionado no servidor. Definindo o seu cliente para confiar no certificado no servidor, você pode se tornar vulnerável a ataques man-in-the-middle. Se você implantar um certificado verificável no servidor, certifique-se de que você altere as configurações do cliente sobre o certificado de confiança para FALSE.

Para obter informações sobre palavras-chave da cadeia de conexão, confira [Usando palavras-chave da cadeia de conexão com o OLE DB Driver for SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md ).  
  
 Para permitir o uso da criptografia quando um certificado não for provisionado no servidor, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager poderá ser usado para definir as opções **Forçar Criptografia de Protocolo** e **Confiar em Certificado do Servidor**. Neste caso, a criptografia usará um certificado do servidor autoassinado sem validação, se nenhum certificado verificável tiver sido provisionado no servidor.  
  
 Os aplicativos também podem usar a palavra-chave "TrustServerCertificate" ou seu atributo de conexão associado para garantir a criptografia. As configurações do aplicativo nunca reduzem o nível de segurança definido pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Gerenciador de Configurações de Cliente, mas podem fortalecê-la. Por exemplo, se a opção **Forçar Criptografia de Protocolo** não for definida para o cliente, um aplicativo poderá solicitar a criptografia por conta própria. Para garantir a criptografia até mesmo quando um certificado do servidor não foi provisionado, um aplicativo pode solicitar a criptografia e "TrustServerCertificate". Porém, se "TrustServerCertificate" não for habilitado na configuração do cliente, um certificado do servidor provisionado ainda será necessário. A tabela a seguir descreve todos os casos:  
  
|Configuração do cliente Forçar Criptografia de Protocolo|Configuração do cliente Confiar em Certificado do Servidor|Atributo de conexão/cadeia de conexão Criptografar/Usar criptografia de dados|Atributo de conexão/cadeia de conexão Confiar em Certificado do Servidor|Resultado|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|Não|N/A|Não (padrão)|Ignored|Não ocorre criptografia.|  
|Não|N/A|Sim|Não (padrão)|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Não|N/A|Sim|Sim|A criptografia sempre ocorre, mas pode usar um certificado do servidor autoassinado.|  
|Sim|Não|Ignored|Ignored|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Sim|Sim|Não (padrão)|Ignored|A criptografia sempre ocorre, mas pode usar um certificado do servidor autoassinado.|  
|Sim|Sim|Sim|Não (padrão)|A criptografia só ocorrerá se houver um certificado de servidor verificável; caso contrário, a tentativa de conexão falhará.|  
|Sim|Sim|Sim|Sim|A criptografia sempre ocorre, mas pode usar um certificado de servidor autoassinado.|  
||||||

> [!CAUTION]
> A tabela anterior apenas fornece um guia sobre o comportamento do sistema em configurações diferentes. Para a conectividade segura, certifique-se de que o cliente e o servidor exigem criptografia. Também verifique se o servidor tem um certificado verificável e que o **TrustServerCertificate** configuração no cliente é definida como FALSE.

## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 
 O OLE DB Driver for SQL Server dá suporte à criptografia sem validação por meio da adição da propriedade de inicialização de fonte de dados SSPROP_INIT_TRUST_SERVER_CERTIFICATE, que é implementada no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT. Além disso, uma nova palavra-chave de cadeia de conexão, "TrustServerCertificate", foi adicionada. Ela aceita os valores sim ou não; não é o padrão. Ao usar componentes de serviço, aceita os valores true ou false; false é o padrão.  
  
 Para obter mais informações sobre os aprimoramentos feitos no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, consulte [propriedades de inicialização e autorização](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
