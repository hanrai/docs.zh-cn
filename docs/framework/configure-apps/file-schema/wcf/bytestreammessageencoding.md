---
title: <byteStreamMessageEncoding>
ms.date: 03/30/2017
ms.assetid: bbadd8dd-60a2-4007-b959-89373a8a7d60
ms.openlocfilehash: b11f472c0e33003e50be4b45bb49196c64ecb70d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69919721"
---
# <a name="bytestreammessageencoding"></a>\<byteStreamMessageEncoding>
指定消息编码作为字节流，也可以选择指定字符编码。  
  
 \<system.serviceModel>  
\<bindings>  
\<customBinding>  
\<绑定 >  
\<binaryMessageEncoding>  
  
## <a name="syntax"></a>语法  
  
```xml  
<byteStreamMessageEncoding />
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|messageVersion|指定使用此绑定发送的消息的 SOAP 版本。 此属性只能设置为 <xref:System.ServiceModel.Channels.MessageVersion.None%2A> 的消息版本值。 字节流消息编码器不支持其他任何消息版本。<br /><br /> 此属性的类型为 <xref:System.ServiceModel.Channels.MessageVersion>。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|定义可由采用此绑定配置的终结点进行处理的 SOAP 消息的复杂性约束。 此元素的类型为 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|定义自定义绑定的所有绑定功能。|  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Configuration.ByteStreamMessageEncodingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>
- <xref:System.ServiceModel.Channels.ByteStreamMessageEncodingBindingElement>
- [消息编码](message-encoding.md)
- [选择消息编码器](../../../wcf/feature-details/choosing-a-message-encoder.md)
- [绑定](../../../wcf/bindings.md)
- [扩展绑定](../../../wcf/extending/extending-bindings.md)
- [自定义绑定](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
