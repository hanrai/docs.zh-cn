---
title: <add> 的 <authorizationPolicies>
ms.date: 03/30/2017
ms.assetid: 613a03d8-4384-4556-bce2-8c23286c0bb0
ms.openlocfilehash: 65398c5afa9750f215c95899bb6004cae671123a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69920273"
---
# <a name="add-of-authorizationpolicies"></a>\<添加 authorizationPolicies > \<的 >
指定声明转换的授权策略。  
  
 \<system.ServiceModel>  
\<行为 >  
\<行为 >  
\<serviceAuthorization>  
\<authorizationPolicies>  
\<add>  
  
## <a name="syntax"></a>语法  
  
```xml  
<authorizationPolicies>
  <add policyType="String" />
</authorizationPolicies>
```  
  
## <a name="type"></a>类型  
 `Type`  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`policyType`|必需的字符串属性。<br /><br /> Windows Communication Foundation (WCF) 访问控制模型支持将一组授权策略作为类型进行设置。 此属性指定一个授权策略，使得可以将一组输入声明转换为另一组声明。 可以根据该授权策略来授予或拒绝访问控制。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<authorizationPolicies>](authorizationpolicies.md)|指定一个授权策略类型集合。|  
  
## <a name="remarks"></a>备注  
 每个授权类型都包含一个所需的 `policyType` 属性，此属性是一个字符串。 该属性指定一个授权策略，可以将一组输入声明转换为另一组声明。 可以根据该授权策略来授予或拒绝访问控制。 有关授权策略工作方式的详细信息, 请参阅<xref:System.IdentityModel.Policy.IAuthorizationPolicy>和[授权策略](../../../wcf/samples/authorization-policy.md)。  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Configuration.ServiceAuthorizationElement>
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A>
- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>
- <xref:System.ServiceModel.Configuration.AuthorizationPolicyTypeElement>
- <xref:System.ServiceModel.Configuration.ServiceAuthorizationElement.AuthorizationPolicies%2A>
- <xref:System.ServiceModel.Configuration.AuthorizationPolicyTypeElementCollection>
- <xref:System.IdentityModel.Policy.IAuthorizationPolicy>
- [授予对服务操作的权限](../../../wcf/samples/authorizing-access-to-service-operations.md)
- [如何：为服务创建自定义授权管理器](../../../wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md)
- [\<add>](add-of-authorizationpolicies.md)
- [授权策略](../../../wcf/samples/authorization-policy.md)
