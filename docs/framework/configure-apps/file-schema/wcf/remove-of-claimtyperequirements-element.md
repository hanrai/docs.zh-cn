---
title: <remove>of <claimTypeRequirements>元素
ms.date: 03/30/2017
ms.assetid: 8ef05bc4-1950-4ee4-95c5-1c6a394eff7e
ms.openlocfilehash: 7238c253bfbc3224c8bbd31265e197dd35e56514
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69934228"
---
# <a name="remove-of-claimtyperequirements-element"></a>\<删除 claimTypeRequirements > \<元素的 >
指定要从联合凭据中移除的声明的类型。  
  
 \<system.ServiceModel>  
\<bindings>  
\<wsFederatedBinding>  
\<绑定 >  
\<安全 >  
\<message>  
\<claimTypeRequirements>  
  
## <a name="syntax"></a>语法  
  
```xml  
<claimTypeRequirements>
  <remove claimType="URI" />
</claimTypeRequirements>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|claimType|一个 URI，定义要移除的声明的类型。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<claimTypeRequirements>](claimtyperequirements-for-message.md)|指定所需声明类型的集合。 每个元素的类型都为 <xref:System.ServiceModel.Configuration.ClaimTypeElement>。<br /><br /> 在联合方案中，服务规定有关传入凭据的要求。 例如，传入凭据必须具有某组声明类型。 此集合中的每个元素都指定希望出现在联合凭据中的必选和可选的声明类型。|  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement>
- <xref:System.ServiceModel.Configuration.FederatedMessageSecurityOverHttpElement.ClaimTypeRequirements%2A>
- <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>
- <xref:System.ServiceModel.Configuration.ClaimTypeElement>
