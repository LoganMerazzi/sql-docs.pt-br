---
title: ErrorValueEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db2065bd599b1aca1542318bfab0d0ce57e2a938
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63070917"
---
# <a name="errorvalueenum"></a>ErrorValueEnum
Especifica o tipo de erro de tempo de execução do ADO.  
  
 Três formas do número do erro estão listadas:  
  
-   Positivos decimal a baixa dois bytes do número total em formato decimal. Esse número é exibido na caixa de diálogo de mensagem de erro padrão Visual Basic. Por exemplo, erro de tempo de execução '3707'.  
  
-   Negativo decimal: A conversão decimal do número de erro completa.  
  
-   Hexadecimal: A representação hexadecimal do número de erro completa. O código de recurso do Windows está em quarto dígito. É o código de recurso para os números de erro ADO *um*. Por exemplo: 0x800***A***0E7B.  
  
> [!NOTE]
>  Erros de OLE DB podem ser passados para o seu aplicativo do ADO. Normalmente, elas podem ser identificadas por um código de recurso do Windows do *4*. Por exemplo, 0x800***4***.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707 -2146824581 0x800A0E7B|Não é possível alterar o **ActiveConnection** propriedade de uma **conjunto de registros** objeto que tem um **comando** objeto como sua fonte.|  
|**adErrCannotComplete**|3732 -2146824556 0x800A0E94|Servidor não pode concluir a operação.|  
|**adErrCantChangeConnection**|3748 -2146824540 0x800A0EA4|Conexão foi negada. Nova conexão que você solicitou tem características diferentes daquele que já está sendo usado.|  
|**adErrCantChangeProvider**|3220 -2146825068 0X800A0C94|O provedor fornecido é diferente daquele que já está sendo usado.|  
|**adErrCantConvertvalue**|3724 -2146824564 0x800A0E8C|Valor de dados não pode ser convertido por razões diferentes de estouro de dados ou de incompatibilidade de sinal. Por exemplo, a conversão pode ter truncado dados.|  
|**adErrCantCreate**|3725 -2146824563 0x800A0E8D|Valor de dados não pode ser definido ou recuperado porque o tipo de dados do campo era desconhecido ou o provedor precisou recursos insuficientes para executar a operação.|  
|**adErrCatalogNotSet**|3747 -2146824541 0x800A0EA3|Operação requer uma validade **ParentCatalog**.|  
|**adErrColumnNotOnThisRow**|3726 -2146824562 0x800A0E8E|Registro não contém esse campo.|  
|**adErrDataConversion**|3421 -2146824867 0x800A0D5D|Aplicativo usa um valor do tipo errado para a operação atual.|  
|**adErrDataOverflow**|3721 -2146824567 0x800A0E89|Valor de dados é muito grande para ser representado pelo tipo de dados do campo.|  
|**adErrDelResOutOfScope**|3738 -2146824550 0x800A0E9A|URL do objeto a ser excluído está fora do escopo do registro atual.|  
|**adErrDenyNotSupported**|3750 -2146824538 0x800A0EA6|Provedor não oferece suporte a restrições de compartilhamento.|  
|**adErrDenyTypeNotSupported**|3751 -2146824537 0x800A0EA7|Provedor não dá suporte ao tipo solicitado de restrição de compartilhamento.|  
|**adErrFeatureNotAvailable**|3251 -2146825037 0x800A0CB3|Objeto ou o provedor não é capaz de executar a operação solicitada.|  
|**adErrFieldsUpdateFailed**|3749 -2146824539 0x800A0EA5|Falha na atualização de campos. Para obter mais informações, examine os **Status** propriedade dos objetos de campo individual.|  
|**adErrIllegalOperation**|3219 -2146825069 0x800A0C93|Operação não é permitida neste contexto.|  
|**adErrIntegrityViolation**|3719 -2146824569 0x800A0E87|Valor dos dados está em conflito com as restrições de integridade do campo.|  
|**adErrInTransaction**|3246 -2146825042 0x800A0CAE|**Conexão** objeto não pode ser fechado explicitamente enquanto estiver em uma transação.|  
|**adErrInvalidArgument**|3001 -2146825287 0x800A0BB9|Argumentos são do tipo errado, estão fora do intervalo aceitável ou estão em conflito com uma da outra.|  
|**adErrInvalidConnection**|3709 -2146824579 0x800A0E7D|A conexão não pode ser usado para executar esta operação. Ele está fechado ou é inválido neste contexto.|  
|**adErrInvalidParamInfo**|3708 -2146824580 0x800A0E7C|**Parâmetro** objeto está definido incorretamente. Informações inconsistentes ou incompletas foi fornecidas.|  
|**adErrInvalidTransaction**|3714 -2146824574 0x800A0E82|Coordenação de transações é inválido ou não foi iniciada.|  
|**adErrInvalidURL**|3729 -2146824559 0x800A0E91|URL contém caracteres inválidos. Certifique-se de que a URL foi digitada corretamente.|  
|**adErrItemNotFound**|3265 -2146825023 0x800A0CC1|Item não pode ser encontrado na coleção que corresponde ao nome solicitado ou ordinal.|  
|**adErrNoCurrentRecord**|3021 -2146825267 0x800A0BCD|Qualquer um dos **BOF** ou **EOF** for True, ou o registro atual foi excluído. A operação solicitada requer um registro atual.|  
|**adErrNotExecuting**|3715 -2146824573 0x800A0E83|Operação não pode ser executada durante a execução não.|  
|**adErrNotReentrant**|3710 -2146824578 0x800A0E7E|Operação não pode ser executada durante o processamento de eventos.|  
|**adErrObjectClosed**|3704 -2146824584 0x800A0E78|Operação não é permitida quando o objeto está fechado.|  
|**adErrObjectInCollection**|3367 -2146824921 0x800A0D27|Objeto já está na coleção. Não é possível anexar.|  
|**adErrObjectNotSet**|3420 -2146824868 0x800A0D5C|Objeto não é válido.|  
|**adErrObjectOpen**|3705 -2146824583 0x800A0E79|Operação não é permitida quando o objeto está aberto.|  
|**adErrOpeningFile**|3002 -2146825286 0x800A0BBA|Não foi possível abrir o arquivo.|  
|**adErrOperationCancelled**|3712 -2146824576 0x800A0E80|Operação cancelada pelo usuário.|  
|**adErrOutOfSpace**|3734 -2146824554 0x800A0E96|Operação não pode ser executada. Provedor não pode obter espaço de armazenamento suficiente.|  
|**adErrPermissionDenied**|3720 -2146824568 0x800A0E88|Permissão insuficiente impede que a gravação no campo.|  
|**adErrProviderFailed**|3000 -2146825288 0x800A0BB8|Provedor de não realizar a operação solicitada.|  
|**adErrProviderNotFound**|3706 -2146824582 0x800A0E7A|Provedor não pode ser encontrado. Ele pode não ser instalado corretamente.|  
|**adErrReadFile**|3003 -2146825285 0x800A0BBB|Não foi possível ler o arquivo.|  
|**adErrResourceExists**|3731 -2146824557 0x800A0E93|Operação de cópia não pode ser executada. Objeto nomeado pela URL de destino já existe. Especificar **adCopyOverwrite** para substituir o objeto.|  
|**adErrResourceLocked**|3730 -2146824558 0x800A0E92|O objeto representado por uma URL especificada é bloqueado por um ou mais processos. Aguarde até que o processo foi concluído e tente a operação novamente.|  
|**adErrResourceOutOfScope**|3735 -2146824553 0x800A0E97|URL de origem ou destino está fora do escopo do registro atual.|  
|**adErrSchemaViolation**|3722 -2146824566 0x800A0E8A|Valor dos dados está em conflito com o tipo de dados ou as restrições do campo.|  
|**adErrSignMismatch**|3723 -2146824565 0x800A0E8B|Falha na conversão porque o valor de dados estava assinado e o tipo de dados do campo usado pelo provedor não estava assinado.|  
|**adErrStillConnecting**|3713 -2146824575 0x800A0E81|Operação não pode ser executada durante a conexão de forma assíncrona.|  
|**adErrStillExecuting**|3711 -2146824577 0x800A0E7F|Operação não pode ser executada durante a execução de forma assíncrona.|  
|**adErrTreePermissionDenied**|3728 -2146824560 0x800A0E90|Permissões são insuficientes para acessar a árvore ou uma subárvore.|  
|**adErrUnavailable**|3736 -2146824552 0x800A0E98|Operação não foi concluída e o status não está disponível. O campo pode estar indisponível ou a operação não foi tentada.|  
|**adErrUnsafeOperation**|3716 -2146824572 0x800A0E84|Configurações de segurança neste computador impedem o acesso a uma fonte de dados em outro domínio.|  
|**adErrURLDoesNotExist**|3727 -2146824561 0x800A0E8F|A URL de origem ou o pai da URL de destino não existe.|  
|**adErrURLNamedRowDoesNotExist**|3737 -2146824551 0x800A0E99|O registro nomeado por essa URL não existe.|  
|**adErrVolumeNotFound**|3733 -2146824555 0x800A0E95|Provedor não pode localizar o dispositivo de armazenamento indicado pela URL. Certifique-se de que a URL foi digitada corretamente.|  
|**adErrWriteFile**|3004 -2146825284 0x800A0BBC|Gravação no arquivo falhou.|  
|**adWrnSecurityDialog**|3717 -2146824571 0x800A0E85|Somente para uso interno. Não use.|  
|**adWrnSecurityDialogHeader**|3718 -2146824570 0x800A0E86|Somente para uso interno. Não use.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
 Apenas os seguintes subconjuntos de equivalentes de ADO/WFC são definidos.  
  
|Constante|  
|--------------|  
|AdoEnums.ErrorValue.BOUNDTOCOMMAND|  
|AdoEnums.ErrorValue.DATACONVERSION|  
|AdoEnums.ErrorValue.FEATURENOTAVAILABLE|  
|AdoEnums.ErrorValue.ILLEGALOPERATION|  
|AdoEnums.ErrorValue.INTRANSACTION|  
|AdoEnums.ErrorValue.INVALIDARGUMENT|  
|AdoEnums.ErrorValue.INVALIDCONNECTION|  
|AdoEnums.ErrorValue.INVALIDPARAMINFO|  
|AdoEnums.ErrorValue.ITEMNOTFOUND|  
|AdoEnums.ErrorValue.NOCURRENTRECORD|  
|AdoEnums.ErrorValue.NOTEXECUTING|  
|AdoEnums.ErrorValue.NOTREENTRANT|  
|AdoEnums.ErrorValue.OBJECTCLOSED|  
|AdoEnums.ErrorValue.OBJECTINCOLLECTION|  
|AdoEnums.ErrorValue.OBJECTNOTSET|  
|AdoEnums.ErrorValue.OBJECTOPEN|  
|AdoEnums.ErrorValue.OPERATIONCANCELLED|  
|AdoEnums.ErrorValue.PROVIDERNOTFOUND|  
|AdoEnums.ErrorValue.STILLCONNECTING|  
|AdoEnums.ErrorValue.STILLEXECUTING|  
|AdoEnums.ErrorValue.UNSAFEOPERATION|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Códigos de erro ADO](../../../ado/guide/appendixes/ado-error-codes.md)
