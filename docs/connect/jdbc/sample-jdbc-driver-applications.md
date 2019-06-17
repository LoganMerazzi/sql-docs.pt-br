---
title: Exemplo de aplicativos do JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 385a5d46129aac81125e29b182cb5a9fdde13897
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797847"
---
# <a name="sample-jdbc-driver-applications"></a>Aplicativos de exemplo do JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Os aplicativos de exemplo do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstram vários recursos do driver JDBC. Além disso, eles demonstram práticas de programação recomendadas que você pode seguir ao usar o driver JDBC com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Todos os aplicativos de exemplo estão contidos em arquivos de código * .java que podem ser compilados e executados em seu computador local e eles estão localizados em várias subpastas no seguinte local:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples  
```

Os tópicos nesta seção descrevem como configurar e executar os aplicativos de exemplo e incluem uma discussão do que os aplicativos de exemplo demonstram.  
  
## <a name="in-this-section"></a>Nesta seção  
  
| Tópico                                                                                                        | Descrição                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Conectando e recuperando dados](../../connect/jdbc/connecting-and-retrieving-data.md)                       | Estes aplicativos de exemplo demonstram como conectar-se a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles também demonstram diferentes maneiras de recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. |
| [Trabalhando com tipos de dados &#40;JDBC&#41;](../../connect/jdbc/working-with-data-types-jdbc.md)                 | Estes aplicativos de exemplo demonstram como usar os métodos de tipo de dados do driver JDBC para trabalhar usando dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                           |
| [Trabalhando com conjuntos de resultados](../../connect/jdbc/working-with-result-sets.md)                                   | Estes aplicativos de exemplo demonstram como usar conjuntos de resultados para processar dados contidos em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                         |
| [Manipular dados grandes](../../connect/jdbc/working-with-large-data.md)                                     | Estes aplicativos de exemplo demonstram como usar buffer adaptável para recuperar dados de valor grande de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem a sobrecarga de cursores de servidor.                                                      |
| [Descoberta e classificação de dados SQL](../../connect/jdbc/data-discovery-classification-sample.md) | Este aplicativo de exemplo demonstra como para recuperar as informações de classificação e descoberta de dados contidos em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados de um objeto de conjunto de resultados usando o Driver JDBC.                                      |
  
## <a name="see-also"></a>Consulte Também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
