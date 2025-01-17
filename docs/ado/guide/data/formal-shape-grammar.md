---
title: Gramática de forma formal | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91bdf0cfbfe87075d2c9484bca7edd835a950ee6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925343"
---
# <a name="formal-shape-grammar"></a>Gramática de forma formal
Esta é a gramática formal para a criação de qualquer comando de forma:  
  
-   Termos gramaticais necessários são cadeias de caracteres de texto delimitadas por colchetes angulares ("<>").  
  
-   Termos opcionais são delimitados por colchetes ("[]").  
  
-   Alternativas são indicadas por uma barra oblíqua ("&#124;").  
  
-   Repetição alternativas são indicadas por um sinal de reticências (...").  
  
-   *Alfa* indica uma cadeia de caracteres de letras em ordem alfabética.  
  
-   *Dígito* indica uma cadeia de caracteres de números.  
  
-   *Dígito do Unicode* indica uma cadeia de caracteres de dígitos de unicode.  
  
 Todos os outros termos são literais.  
  
|Termo|Definição|  
|----------|----------------|  
|\<shape-command>|SHAPE [\<table-exp> [[AS] \<alias>]][\<shape-action>]|  
|\<table-exp>|{\<texto de comando do provedor >}&#124;<br /><br /> (\<comando shape >)&#124;<br /><br /> TABELA \<entre aspas-name >&#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|ACRESCENTAR \<lista de campos de um alias >&#124;<br /><br /> COMPUTAR \<lista de campos de um alias > [BY \<lista de campos >]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<relation-exp>) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> Relacionar \<relação-cond-list >|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<nome do campo > TO \<filho ref >|  
|\<child-ref>|\<nome do campo >&#124;<br /><br /> PARÂMETRO \<ref param >|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|Soma (\<nome qualificado de campo >)&#124;<br /><br /> AVG(\<qualified-field-name>) &#124;<br /><br /> MIN(\<qualified-field-name>) &#124;<br /><br /> MAX(\<qualified-field-name>) &#124;<br /><br /> COUNT(\<qualified-alias> &#124; \<qualified-name>) &#124;<br /><br /> STDEV(\<qualified-field-name>) &#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias>]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<name>|  
|\<qualified-name>|alias[.alias...]|  
|\<name>|alfa [alfa &#124; dígitos &#124; _ &#124; # &#124; : &#124; ...]|  
|\<number>|Dígito [dígito...]|  
|\<new-exp>|NOVOS \<tipo de campo > [(\<número > [, \<número >])]|  
|\<tipo de campo >|Um tipo de dados OLE DB ou ADO.|  
|\<string>|caractere Unicode [unicode char...]|  
|\<expression>|Um Visual Basic para a expressão de aplicativos cujos operandos são outras colunas não CALC na mesma linha.|  
  
## <a name="see-also"></a>Consulte também  
 [Acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Visão geral de modelagem de dados](../../../ado/guide/data/data-shaping-overview.md)   
 [Provedores necessários para Data Shaping](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md)   
 [Funções do Visual Basic for Applications](../../../ado/guide/data/visual-basic-for-applications-functions.md)
