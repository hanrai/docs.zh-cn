---
title: <service>
ms.date: 03/30/2017
ms.assetid: 13123dd6-c4a9-4a04-a984-df184b851788
ms.openlocfilehash: 69f3c70514fc2bcab1b4ef6a45036de98d1af7b7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69936524"
---
# <a name="service"></a>\<service>
`service` 元素包含 Windows Communication Foundation (WCF) 服务的设置。 它还包含公开此服务的终结点。  
  
 \<system.ServiceModel>  
\<services>  
\<service>  
  
## <a name="syntax"></a>语法  
  
```xml  
<service behaviorConfiguration="String"
         name="String">
</service>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|behaviorConfiguration|一个字符串，其中包含要用于实例化服务的行为的行为名。 定义服务时，该行为名必须在作用域内。 默认值为一个空字符串。|  
|NAME|必需的字符串属性，此属性指定要进行实例化的服务的类型。 此设置必须等同于一个有效类型。 格式应为 `Namespace.Class.`|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<endpoint>](endpoint-element.md)|公开此服务的 `endpoint` 元素的集合。|  
|[\<host>](host.md)|指定此服务实例的主机。 此元素的类型为 <xref:System.ServiceModel.Configuration.HostElement>。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<services>](services.md)|所有 WCF 配置元素的根元素。|  
  
## <a name="remarks"></a>备注  
 服务是在配置文件的 `services` 节中定义的。 程序集可以包含任意多个服务。 每个服务都有自己的 `service` 配置节。 本节及其内容定义特定服务的服务协定、行为和终结点。  
  
 `behaviorConfiguration` 元素也是可选的。 它标识服务使用的行为。 在此属性中指定的行为必须链接到同一配置文件中的作用域内的行为。  
  
 每个服务都将公开一个或多个终结点，每个终结点具有自己的地址和绑定。 配置文件中使用的所有绑定都必须在该文件的范围内定义。 绑定通过 `name` 和 `bindingConfiguration` 属性的组合链接到终结点。 `name` 特性说明在哪个节中定义绑定。 `bindingConfiguration` 特性定义使用绑定节中的哪个配置。 绑定节可以定义若干个配置。  
  
## <a name="example"></a>示例  
 这是服务配置的一个示例。  
  
```xml  
<service behaviorConfiguration="testChannelBehavior"
         name="HelloWorld">
  <endpoint address="/HelloWorld2/"
            name="test"
            bindingNamespace="http://www.cohowinery.com/"
            binding="basicHttpBinding"
            contract="IHelloWorld" />
</service>
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Configuration.ServiceElement>
- [配置服务](../../../wcf/configuring-services.md)
