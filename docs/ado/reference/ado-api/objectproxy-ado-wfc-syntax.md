---
title: ObjectProxy (ADO – sintaxe WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 485d011fa6762acd04cad54ff7fffc8d8136e063
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917952"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO – Sintaxe WFC)
Uma **ObjectProxy** objeto representa um servidor e é retornado pela **createObject** método da [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto. A classe ObjectProxy tem um método, **chamar**, que pode invocar um método no servidor e retornar um objeto resultante dessa invocação.  
  
 **pacote com.ms.wfc.data**  
  
## <a name="methods"></a>Métodos  
  
### <a name="call-method-adowfc-syntax"></a>Método de chamada (sintaxe do ADO/WFC)  
 Invoca um método no servidor representadas pela ObjectProxy. Opcionalmente, os argumentos de método podem ser passados como uma matriz de objetos.  
  
#### <a name="syntax"></a>Sintaxe  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>Retorna  
 Object  
 Um objeto resultante da invocação do método.  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjectProxy*  
 Uma **ObjectProxy** objeto que representa o servidor.  
  
 *Método*  
 Uma cadeia de caracteres que contém o nome do método a ser invocado no servidor.  
  
 *args*  
 Opcional. Uma matriz de objetos que são argumentos para o método no servidor. Tipos de dados Java são automaticamente convertidos para tipos de dados adequados para uso no servidor.
