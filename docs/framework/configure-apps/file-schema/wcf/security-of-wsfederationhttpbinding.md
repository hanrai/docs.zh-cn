---
title: <security> 的 <wsFederationHttpBinding>
ms.date: 03/30/2017
ms.assetid: a8e5e854-b8dc-4921-843d-34b6a4a6a8ba
ms.openlocfilehash: 875ce7d548d59f32465da817e9e956217f346f60
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69936536"
---
# <a name="security-of-wsfederationhttpbinding"></a>\<wsFederationHttpBinding 的\<安全 > >
定义[ \<wsFederationHttpBinding >](wsfederationhttpbinding.md)的安全设置。  
  
 \<system.ServiceModel>  
\<bindings>  
\<wsFederatedBinding>  
\<绑定 >  
\<安全 >  
  
## <a name="syntax"></a>语法  
  
```xml  
<wsFederationBinding>
  <binding>
    <security mode="None/Message/TransportWithMessageCredential">
      <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
               issuedTokenType="string"
               issuedKeyType="SymmetricKey/PublicKey"
               negotiateServiceCredential="Boolean">
        <claimTypeRequirements>
          <add claimType="URI"
               isOptional="Boolean" />
        </claimTypeRequirements>
        <issuer address="Uri" >
          <headers>
            <add name="String"
                 namespace="String" />
          </headers>
          <identity>
            <certificate encodedValue="String" />
            <certificateReference findValue="String"
                                  isChainIncluded="Boolean"
                                  storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                                  storeLocation="LocalMachine/CurrentUser"
                                  X509FindType="System.Security.Cryptography.X509certificates.X509findtype" />
            <dns value="String" />
            <rsa value="String" />
            <servicePrincipalName value="String" />
            <usePrincipalName value="String" />
          </identity>
        </issuer>
        <issuerMetadata address="String">
          <headers>
            <add name="String"
                 namespace="String" />
          </headers>
          <identity>
            <certificate encodedValue="String" />
            <certificateReference findValue="String"
                                  isChainIncluded="Boolean"
                                  storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                                  storeLocation="LocalMachine/CurrentUser"
                                  X509FindType="System.Security.Cryptography.X509certificates.X509findtype" />
            <dns value="String" />
            <rsa value="String" />
            <servicePrincipalName value="String" />
            <usePrincipalName value="String" />
          </identity>
        </issuerMetadata>
        <tokenRequestParameters>
          <xmlElement>
          </xmlElement>
        </tokenRequestParameters>
      </message>
    </security>
  </binding>
</wsFederationBinding>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|模式|可选。 指定所应用的安全类型。 默认值为 `Message`。 此属性的类型为 <xref:System.ServiceModel.WSFederationHttpSecurityMode>。|  
  
## <a name="mode-attribute"></a>Mode 属性  
  
|值|描述|  
|-----------|-----------------|  
|无|SOAP 消息在传输过程中并不安全。|  
|消息|通过使用 SOAP 消息安全，可以提供完整性、保密性、服务器身份验证和客户端身份验证。 默认情况下，将对正文进行加密和签名。 此服务需要使用证书进行配置。 客户端根据由安全令牌服务颁发给客户端的令牌进行身份验证|  
|TransportWithMessageCredential|完整性、保密性和服务器身份验证均由 HTTPS 提供。 此服务需要使用证书进行配置。 客户端身份验证采用 SOAP 消息安全方式提供，并根据由安全令牌服务颁发给客户端的令牌进行。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<message>](message-element-of-wsfederationhttpbinding.md)|定义消息级安全性设置。 此元素的类型为 <xref:System.ServiceModel.Configuration.FederatedMessageSecurityOverHttpElement>。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|定义[ \<wsDualHttpBinding >](wsdualhttpbinding.md)的所有绑定功能。|  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.WSFederationHttpSecurity>
- <xref:System.ServiceModel.WSFederationHttpBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.WSFederationHttpBindingElement.Security%2A>
- <xref:System.ServiceModel.Configuration.WSFederationHttpSecurityElement>
- [如何：创建 WSFederationHttpBinding](../../../wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)
- [保护服务和客户端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
- [选择凭据类型](../../../wcf/feature-details/selecting-a-credential-type.md)
- [绑定](../../../wcf/bindings.md)
- [配置系统提供的绑定](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [使用绑定配置服务和客户端](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
