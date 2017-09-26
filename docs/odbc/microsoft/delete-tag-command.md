---
title: "Comando de marca de exclusão | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c10f0daac2f672b40b3bda050401e9873afe6aa8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="delete-tag-command"></a>EXCLUIR o comando marca
Remove uma marca ou marcas de um arquivo de índice composto (. cdx).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>Argumentos  
 *TagName1*OF *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]]...  
 Especifica uma marca para remover um arquivo de índice composto. Você pode excluir várias marcas com uma marca de excluir, incluindo uma lista de nomes de marcas separados por vírgulas. Se dois ou mais marcas com o mesmo nome existirem nos arquivos de índice aberto, você pode remover uma marca de um arquivo de índice específico, incluindo de *CDXFileName*.  
  
 Todos os [OF *CDXFileName*]  
 Remove todas as marcas de um arquivo de índice composto. Se a tabela atual tem um arquivo de índice composto estrutural, todas as marcas são removidas do arquivo de índice, o arquivo de índice é excluído do disco e o sinalizador no cabeçalho da tabela que indica a presença de um arquivo de índice composto estrutural associado é removido. Use com de *CDXFileName* para remover todas as marcas de um arquivo de índice composto aberto que não seja o arquivo de índice composto estrutural.  
  
## <a name="remarks"></a>Comentários  
 Arquivos de índice composto, criados com o índice, contêm marcas correspondentes a entradas de índice. Excluir marca é usada para remover uma marca ou marcas de arquivos de índice composto aberto. Você pode excluir somente marcas de arquivos de índice composto abertos na área de trabalho atual. Se você remover todas as marcas de um arquivo de índice composto, o arquivo é excluído do disco.  
  
 Do Visual FoxPro procura primeiro uma marca no arquivo de índice composto estrutural (se estiver aberto). Se a marca não está no arquivo de índice composto estrutural, Visual FoxPro, em seguida, procura a marca em outros arquivos de índice composto aberto.  
  
## <a name="see-also"></a>Consulte também  
 [Comando INDEX](../../odbc/microsoft/index-command.md)