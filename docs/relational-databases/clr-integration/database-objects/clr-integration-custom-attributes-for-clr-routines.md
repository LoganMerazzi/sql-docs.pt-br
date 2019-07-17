---
title: Atributos personalizados para rotinas de CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c1105579dc5da82a66fb101e559e1fb96feac1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138626"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>Atributos personalizados da integração CLR para rotinas CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os atributos listados podem ser aplicados para rotinas de tempo de execução (CLR) de linguagem comum, tipos definidos pelo usuário e agregações definidas pelo usuário que são registradas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se o atributo não for aplicado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] assumirá o valor padrão. Os atributos listados são definidos na **SQLServer** namespace.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>O atributo SqlUserDefinedAggregate  
 O **SqlUserDefinedAggregate** atributo indica que o método deve ser registrado como uma agregação definida pelo usuário. Todas as agregações definidas pelo usuário devem ser anotadas com esse atributo.  
  
 Para obter mais informações, consulte [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>O atributo SqlFunction  
 O **SqlFunction** atributo indica que o método deve ser registrado como uma função, com o conjunto de atributos de função apropriada.  
  
 Para obter mais informações, consulte [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>O atributo SqlFacet  
 O **SqlFacet** atributo é usado para retornar informações sobre o tipo de retorno de uma expressão de tipo definido pelo usuário (UDT).  
  
 Para obter mais informações, consulte [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>O atributo SqlProcedure  
 O **SqlProcedure** atributo indica que o método deve ser registrado como um procedimento armazenado. Esse atributo só é usado pelo Visual Studio para registrar o método especificado como um procedimento armazenado automaticamente; não é usado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações, consulte [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>O atributo SqlTrigger  
 O **SqlTrigger** atributo indica que o método deve ser registrado como um gatilho.  
  
 Para obter mais informações, consulte [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022) e [SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>O SqlUserDefinedTypeAttribute  
 Você pode aplicar o SqlUserDefinedTypeAttribute a uma definição de classe no assembly. Ele faz com que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crie um tipo definido pelo usuário que é associado à definição de classe que tem esse atributo personalizado.  
  
 Para obter mais informações, consulte [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>O atributo SqlMethod  
 O **SqlMethod** atributo é usado para indicar as propriedades de determinismo e dados de acesso de um método ou uma propriedade em um UDT.  
  
 Para obter mais informações, consulte [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Consulte também  
 [Agregações CLR definidas pelo usuário](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Funções CLR definidas pelo usuário](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipos CLR definidos pelo usuário](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Procedimentos armazenados CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Gatilhos CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
