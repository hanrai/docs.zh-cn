---
title: <custom>
ms.date: 03/30/2017
ms.assetid: a6f65a00-bd1a-4d4a-955a-fe009ec02ab8
ms.openlocfilehash: b5cc522604fa7aca8ca6eae787520265b36fef6f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925958"
---
# <a name="custom"></a>\<custom>
指定自定义对等解析程序服务的设置。  
  
\<system.serviceModel>  
\<bindings>  
\<netPeerBinding>  
\<绑定 >  
\<resolver>  
\<custom>  
  
## <a name="syntax"></a>语法  
  
```xml  
<custom address="Uri"
        resolverType="String">
  <headers/>
  <identity/>
</custom>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`address`|一个 URI，指定承载自定义对等解析程序服务的对等节点的终结点地址。|  
|`resolverType`|一个字符串值，指定自定义对等解析程序服务的类型。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<identity>](identity.md)|指定配置了此元素的自定义对等解析程序的标识。 此元素的类型为 <xref:System.ServiceModel.Configuration.IdentityElement>。|  
|[\<headers>](headers-element.md)|一个地址标头集合，可用于由自定义对等解析程序处理的 SOAP 消息。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<resolver>](resolver.md)|一个对等解析程序，可用于将对等网格 ID 解析为一组对等节点地址，这些地址表示参与网格的若干节点。|  
  
## <a name="remarks"></a>备注  
 此元素可定义自定义对等解析程序服务的基本设置，其中包括执行服务的对等解析程序的终结点地址和所有特定绑定设置。 有关创建自定义冲突解决程序的详细信息, 请参阅[将自定义冲突解决程序添加到 PeerChannel 应用程序](https://docs.microsoft.com/previous-versions/ms730105(v=vs.90))。  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>
- <xref:System.ServiceModel.PeerResolvers.PeerCustomResolverSettings>
- <xref:System.ServiceModel.Configuration.PeerResolverElement.Custom%2A>
- <xref:System.ServiceModel.Configuration.PeerCustomResolverElement>
- [对等解析程序](../../../wcf/feature-details/peer-resolvers.md)
- [向 PeerChannel 应用程序添加自定义冲突解决程序](https://docs.microsoft.com/previous-versions/ms730105(v=vs.90))
