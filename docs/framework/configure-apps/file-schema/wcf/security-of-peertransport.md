---
title: <security> 的 <peerTransport>
ms.date: 03/30/2017
ms.assetid: f73634ed-f896-4968-bf74-5e5ac52d3b6b
ms.openlocfilehash: bdd3b236c9bae198f8027c4ca0c0fa5b70d30342
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69936641"
---
# <a name="security-of-peertransport"></a>\<peerTransport 的\<安全 > >
包含与对等通道相关的安全设置，包括使用的身份验证类型和用于消息传输的安全性。  
  
 \<system.serviceModel>  
\<bindings>  
\<customBinding>  
\<绑定 >  
\<peerTransport>  
\<安全 >  
  
## <a name="syntax"></a>语法  
  
```xml  
<security mode="None/Transport/Message/TransportWithMessageCredential">
  <transport clientCredentialType="None/Windows/UserName/Certificate/CardSpace" />
</security
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`mode`|指定要应用的安全类型。 默认值为 Message。 此属性的类型为 <xref:System.ServiceModel.SecurityMode>。|  
  
## <a name="mode-attribute"></a>mode 属性  
  
|值|描述|  
|-----------|-----------------|  
|`None`|禁用安全性。|  
|`Transport`|使用 HTTPS 提供安全性。|  
|`Message`|SOAP 安全提供身份验证、完整性和保密性。|  
|`TransportWithMessageCredential`|HTTPS 提供身份验证和保密性。 SOAP 消息提供丰富的凭据类型。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<transport>](transport-of-peertransport.md)|定义自定义绑定的对等传输。 此元素具有一个 `clientCredentialType` 属性，可指定与服务进行交互时要使用的凭据。 此属性的类型为 <xref:System.ServiceModel.PeerTransportCredentialType>。<br /><br /> 此元素的类型为 <xref:System.ServiceModel.Configuration.PeerTransportSecurityElement>。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<peerTransport>](peertransport.md)|定义自定义绑定的对等传输。|  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Configuration.PeerSecurityElement>
- <xref:System.ServiceModel.PeerSecuritySettings>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [传输安全性](../../../wcf/feature-details/transport-security.md)
- [传输](../../../wcf/feature-details/transports.md)
- [选择传输](../../../wcf/feature-details/choosing-a-transport.md)
- [绑定](../../../wcf/bindings.md)
- [扩展绑定](../../../wcf/extending/extending-bindings.md)
- [自定义绑定](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
