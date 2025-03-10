---
title: <add> 的 <allowedAudienceUris>
ms.date: 03/30/2017
ms.assetid: 4e7b7637-e0ea-4a91-988f-6b6ef28d9fc3
ms.openlocfilehash: 64f0dd5c97ddfcd2fffd8ff4820d02af8c1ced54
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69926884"
---
# <a name="add-of-allowedaudienceuris"></a>\<添加 allowedAudienceUris > \<的 >
添加 <xref:System.IdentityModel.Tokens.SamlSecurityToken> 安全令牌的目标 URI，只有在使用该目标 URI 时，<xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> 实例才会将该令牌视为有效令牌。  
  
 \<system.ServiceModel>  
\<行为 >  
\<serviceBehaviors>  
\<行为 >  
\<serviceCredentials>  
\<issuedTokenAuthentication>  
\<allowedAudienceUris>  
\<添加 allowedAudienceUris 的\<> 元素 >  
  
## <a name="syntax"></a>语法  
  
```xml  
<allowedAudienceUris>
  <add allowedAudienceUri="String" />
</allowedAudienceUris>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|allowedAudienceUri|一个包含 <xref:System.IdentityModel.Tokens.SamlSecurityToken> 安全令牌的目标 URI 的字符串，只有在使用该目标 URI 时，<xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> 实例才会将该令牌视为有效令牌。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<allowedAudienceUris>](allowedaudienceuris.md)|表示 <xref:System.IdentityModel.Tokens.SamlSecurityToken> 安全令牌的目标 URI 集合，只有在使用这些目标 URI 时，<xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> 实例才会将该令牌视为有效令牌。|  
  
## <a name="remarks"></a>备注  
 在采用颁发 <xref:System.IdentityModel.Tokens.SamlSecurityToken> 安全令牌的安全令牌服务 (STS) 的联合应用程序中，应使用此集合。 当 STS 颁发安全令牌时，它可以通过将 <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition> 添加到安全令牌中，来指定安全令牌的目标 Web 服务的 URI。 这样，通过指定应采用以下方式执行此检查，接收方 Web 服务的 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> 将能够验证颁发的安全令牌是否针对此 Web 服务：  
  
- 将 `audienceUriMode` 的 `<issuedTokenAuthentication>` 属性设置为 <xref:System.IdentityModel.Selectors.AudienceUriMode.Always> 或 <xref:System.IdentityModel.Selectors.AudienceUriMode.BearerKeyOnly>。  
  
- 将有效 URI 添加到此集合，以指定有效 URI 集。  
  
 有关详细信息，请参阅 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>。  
  
 有关使用此配置元素的详细信息, 请[参阅如何:在联合身份验证服务](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)上配置凭据。  
  
## <a name="see-also"></a>请参阅

- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement.AllowedAudienceUris%2A>
- <xref:System.ServiceModel.Configuration.AllowedAudienceUriElementCollection>
- <xref:System.ServiceModel.Configuration.AllowedAudienceUriElement>
- <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowedAudienceUris%2A>
- [\<allowedAudienceUris>](allowedaudienceuris.md)
- [\<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md)
- [安全行为](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [保护服务和客户端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
- [如何：在联合身份验证服务上配置凭据](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
