---
title: Restrições do modelo de programação de integração de CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
author: rothja
ms.author: jroth
ms.openlocfilehash: ecdc3192e0b6de26d7b829883d26cc7bbaa7e04a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216396"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restrições do modelo de programação da Integração CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando você estiver criando um procedimento armazenado gerenciado ou outro objeto de banco de dados gerenciado, há determinadas verificações de código realizadas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que precisam ser consideradas. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] realiza verificações no assembly de código gerenciado quando ele é registrado pela primeira vez no banco de dados, usando o **CREATE ASSEMBLY** instrução e também em tempo de execução. O código gerenciado também é verificado em tempo de execução porque, em um assembly, talvez haja caminhos de código que jamais possam ser alcançados em tempo de execução.  Isso proporciona flexibilidade para registrar, especialmente, assemblies de terceiros, logo um assembly não seria bloqueado quando houvesse um código 'não seguro' projetado para execução em um ambiente do cliente, mas que jamais seria executado no CLR hospedado. Os requisitos que o código gerenciado deve atender dependem se o assembly é registrado como **seguro**, **EXTERNAL_ACCESS**, ou **UNSAFE**, **SAFE** sendo mais rigorosos e estão listados abaixo.  
  
 Além das restrições colocadas nos assemblies de código gerenciado, também há permissões de segurança de código que são concedidas. O CLR (Common Language Runtime) oferece suporte a um modelo de segurança chamado segurança de acesso do código (CAS) destinado ao código gerenciado. Nesse modelo, são concedidas permissões a assemblies com base na identidade do código. **SEGURO**, **EXTERNAL_ACCESS**, e **UNSAFE** assemblies têm permissões CAS diferentes. Para obter mais informações, consulte [segurança de acesso do código de integração de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Verificações de CREATE ASSEMBLY  
 Quando o **CREATE ASSEMBLY** instrução é executada, as seguintes verificações são executadas para cada nível de segurança.  Se qualquer verificação falhar, **CREATE ASSEMBLY** falhará com uma mensagem de erro.  
  
### <a name="global-any-security-level"></a>Global (qualquer nível de segurança)  
 Todos os assemblies referenciados devem atender a um ou mais dos seguintes critérios:  
  
-   O assembly já está registrado no banco de dados.  
  
-   O assembly é um daqueles para os quais há suporte. Para obter mais informações, consulte [suporte para bibliotecas do .NET Framework](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
-   Você está usando **criar ASSEMBLY da** _\<local >,_ e todos os assemblies referenciados e suas dependências estão disponíveis no *\<local >* .  
  
-   Você está usando **criar ASSEMBLY da** _\<bytes... >,_ e todas as referências são especificadas por meio do espaço de bytes separados.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Todos os **EXTERNAL_ACCESS** assemblies devem atender aos seguintes critérios:  
  
-   Não são usados campos estáticos para armazenar informações. São permitidos campos estáticos somente leitura.  
  
-   O teste PEVerify passou. A ferramenta PEVerify (peverify.exe), que verifica se o código MSIL e os metadados associados atendem aos requisitos de segurança do tipo, é fornecida com o SDK do .NET Framework.  
  
-   A sincronização, por exemplo, com o **SynchronizationAttribute** de classe, não é usado.  
  
-   Não são usados métodos Finalizer.  
  
 Os seguintes atributos personalizados não são permitidos na **EXTERNAL_ACCESS** assemblies:  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   Todos os **EXTERNAL_ACCESS** assembly condições são verificadas.  
  
## <a name="runtime-checks"></a>Verificações de tempo de execução  
 Em tempo de execução, o assembly do código é verificado em relação às seguintes condições. Se alguma dessas condições for encontrada, o código gerenciado não terá permissão de execução, e uma exceção será lançada.  
  
### <a name="unsafe"></a>UNSAFE  
 Carregar um assembly seja explicitamente chamando o **System.Reflection.Assembly.Load()** método de uma matriz de bytes ou implicitamente através do uso de **Reflection. Emit** namespace-não é permitida.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Todos os **UNSAFE** condições são verificadas.  
  
 São desaprovados todos os tipos e métodos anotados com os seguintes valores HPA (atributo de proteção de host) na lista de assemblies para a qual há suporte.  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Synchronization  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   Interface de Usuário  
  
 Para obter mais informações sobre HPAs e uma lista de tipos desaprovados e membros no assembly com suporte, consulte [atributos de proteção de Host e programação de integração de CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Todos os **EXTERNAL_ACCESS** condições são verificadas.  
  
## <a name="see-also"></a>Consulte também  
 [Bibliotecas com suporte do .NET Framework](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [Segurança de acesso do código de integração de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Atributos de proteção de host e programação da integração CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Criando um assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
