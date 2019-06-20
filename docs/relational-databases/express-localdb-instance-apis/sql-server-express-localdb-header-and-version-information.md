---
title: SQL Server Express LocalDB cabeçalho e informações de versão | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apilocation:
- sqluserinstance.dll
ms.assetid: 506b5161-b902-4894-b87b-9192d7b1664a
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 870acddcd825c9c112274d294fa4c97848a85236
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62669651"
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>Cabeçalho e informações de versão de LocalDB do SQL Server Express
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Não há nenhum arquivo de cabeçalho separado para a API da instância de LocalDB do SQL Server Express; as assinaturas e os códigos de erro da função LocalDB são definidos no arquivo de cabeçalho do SQL Server Native Client (sqlncli.h). Para usar a API de instância LocalDB, você deverá incluir o arquivo de cabeçalho sqlncli.h em seu projeto.  
  
## <a name="localdb-versioning"></a>Controle de versão de LocalDB  
 A instalação de LocalDB usa um único conjunto de binários por versão principal do SQL Server. Estas versões LocalDB são mantidas e corrigidas de maneira independente. Isto significa que o usuário tem que especificar qual versão de linha de base do LocalDB (quer dizer, a versão principal do SQL Server) ele ou ela estará usando. A versão é especificada no formato de versão padrão definido pelo .NET Framework **Version** classe:  
  
 *major.minor[.build[.revision]]*  
  
 Os primeiros dois números na cadeia de caracteres de versão (*principais* e *secundárias*) são obrigatórios. Os dois últimos números na cadeia de caracteres de versão (*construir* e *revisão*) são opcionais e usarão zero como padrão se o usuário os omitir. Isso significa que, se o usuário especificar só "12.2" como o número de versão LocalDB, ele será tratado como se o usuário especificasse "12.2.0.0".  
  
 A versão para a instalação do LocalDB é definida na chave do Registro MSSQLServer\CurrentVersion na chave do Registro da instância do SQL Server, por exemplo:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL13E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 Diversas versões do LocalDB na mesma estação de trabalho têm suporte lado a lado. No entanto, o código do usuário sempre usa a versão mais recente disponível **SQLUserInstance** DLL no computador local para se conectar a instâncias de LocalDB.  
  
## <a name="locating-the-sqluserinstance-dll"></a>Localizando a DLL SQLUserInstance  
 Para localizar o **SQLUserInstance** DLL, o provedor de cliente usa a seguinte chave do registro:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 Nesta chave, há uma lista de chaves, uma para cada versão do LocalDB instalada no computador. Cada uma destas chaves é nomeada com o número de versão de LocalDB no formato  *\<major-version >* . *\<versão secundária >* (por exemplo, a chave para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] chamado 13.0). Em cada chave de versão há um par de nome-valor `InstanceAPIPath` que define o caminho completo para o arquivo SQLUserInstance.dll instalado com essa versão. O exemplo a seguir mostra as entradas do registro para um computador que tem versões de LocalDB 11.0 e 13.0 instalado:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 O provedor de cliente deve localizar a versão mais recente entre todas as versões instaladas e carregar os **SQLUserInstance** arquivo DLL do associado `InstanceAPIPath` valor.  
  
### <a name="wow64-mode-on-64-bit-windows"></a>Modo de WOW64 no Windows de 64 bits  
 As instalações de 64 bits do LocalDB terão um conjunto adicional de chave do Registro para permitir que aplicativos de 32 bits executados em modo WOW64 (Windows-32-on-Windows-64) usem LocalDB. Especificamente, no Windows de 64 bits, o LocalDB MSI criará as chave do Registro a seguir:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\13.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\130\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 programas de 64 bits lendo a `Installed Versions` chave verão valores apontando para versões de 64 bits do **SQLUserInstance** DLL, enquanto programas de 32 bits (em execução no Windows de 64 bits no modo WOW64) serão automaticamente redirecionados para uma `Installed Versions` chave localizada sob o `Wow6432Node` hive. Esta chave contém valores apontando para versões de 32 bits do **SQLUserInstance** DLL.  
  
## <a name="using-localdbdefineproxyfunctions"></a>Usando LOCALDB_DEFINE_PROXY_FUNCTIONS  
 A API da instância de LocalDB define uma constante chamada LOCALDB_DEFINE_PROXY_FUNCTIONS que automatiza a descoberta e carregamento do **SqlUserInstance** DLL.  
  
 A seção de código habilitada por esta constante fornece uma implementação de proxies para cada API do LocalDB. As implementações de proxy usam uma função comum para associar a pontos de entrada no mais recente instalada **SqlUserInstance** DLL e, em seguida, encaminhar as solicitações.  
  
 As funções de proxy só serão habilitadas se a constante LOCALDB_DEFINE_PROXY_FUNCTIONS estiver definida no código de usuário antes de incluir o arquivo sqlncli.h. A constante deve ser definida em somente um módulo de origem (arquivo .cpp) porque define nomes de função externos para todos os pontos de entrada da API. Fornece uma implementação de proxies para cada API de LocalDB.  
  
 O exemplo de código a seguir mostra como usar a macro do código de C++ nativo:  
  
```  
// Define the LOCALDB_DEFINE_PROXY_FUNCTIONS constant to enable the LocalDB proxy functions   
// The #define has to take place BEFORE the API header file (sqlncli.h) is included  
#define LOCALDB_DEFINE_PROXY_FUNCTIONS  
#include <sqlncli.h>  
...  
HRESULT hr = S_OK;  
  
// Create LocalDB instance by calling the create API proxy function included by macro  
if (FAILED(hr = LocalDBCreateInstance( L"12.0", L"name", 0)))  
{  
...  
}  
...  
  
```  
  
  
