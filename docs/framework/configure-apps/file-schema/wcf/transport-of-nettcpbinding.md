---
title: <transport> 的 <netTcpBinding>
ms.date: 03/30/2017
ms.assetid: 49462e0a-66e1-463f-b3e1-c83a441673c6
ms.openlocfilehash: 265b68e058919d1d5c5f1dbcfb1419b57be9aeab
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69915552"
---
# <a name="transport-of-nettcpbinding"></a>\<netTcpBinding> 的 \<transport>
定义使用[ \<netTcpBinding >](nettcpbinding.md)配置的终结点的消息级安全性要求的类型。  
  
 \<system.ServiceModel>  
\<bindings>  
\<netTcpBinding>  
\<绑定 >  
\<安全 >  
\<transport>  
  
## <a name="syntax"></a>语法  
  
```xml  
<netTcpBinding>
  <binding>
    <security mode="None|Transport|Message|TransportWithMessageCredential">
      <transport clientCredentialType="None|Windows|Certificate"
                 protectionLevel="None|Sign|EncryptAndSign"
                 sslProtocols="Tls|Tls11|Tls12">
        <extendedProtectionPolicy policyEnforcement="Never|WhenSupported|Always"
                                  protectionScenario="TransportSelected|TrustedProxy">
          <customServiceNames>
          </customServiceNames>
        </extendedProtectionPolicy>
      </transport>
    </security>
  </binding>
</netTcpBinding>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|clientCredentialType|可选。 指定要在使用传输安全性执行客户端身份验证时使用的凭据类型。<br /><br /> -默认值为`Windows`。<br />-此属性的类型<xref:System.ServiceModel.TcpClientCredentialType>为。|  
|protectionLevel|可选。 定义 TCP 传输级别的安全性。 对消息进行签名可以降低该消息在传输过程中被第三方篡改的风险。 加密可以在传输过程中提供数据级保密。<br /><br /> 默认值为 `EncryptAndSign`。|  
|sslProtocols|指定支持哪些 SslProtocols 的 SslProtocols 枚举标志值。 默认值为 Tls&#124;Tls11&#124;Tls12。|  
|policyEnforcement|此枚举指定应何时强制实施 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy>。<br /><br /> 1.Never – 绝不强制实施此策略（禁用扩展保护）。<br />2.WhenSupported – 仅在客户端支持扩展保护时才强制实施此策略。<br />3.Always – 总是强制实施此策略。 不支持扩展保护的客户端将无法进行身份验证。|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 属性  
  
|值|描述|  
|-----------|-----------------|  
|无|客户端为匿名客户端。 这需要服务证书。|  
|Windows|指定使用 SP 协商（Kerberos 协商）进行客户端 Windows 身份验证。|  
|证书|使用证书进行对客户端进行身份验证。 这使用 SSL 协商并需要服务证书。|  
  
## <a name="protectionlevel-attribute"></a>protectionLevel 属性  
  
|值|描述|  
|-----------|-----------------|  
|无|无保护。|  
|Sign|对消息进行签名。|  
|EncryptAndSign|-对消息进行加密和签名。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<security>](security-of-nettcpbinding.md)|指定[ \<netTcpBinding >](nettcpbinding.md)的安全功能。|  
  
## <a name="remarks"></a>备注  
 使用传输安全性以获得 SOAP 消息的完整性和保密性以及相互身份验证。 如果在绑定上选择此安全模式，则使用安全传输配置信道栈，并且使用传输安全性（如 Windows (Negotiate) 或 SSLL）保护 SOAP 消息安全通过 TCP 传递。  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.TcpTransportSecurity>
- <xref:System.ServiceModel.Configuration.NetTcpSecurityElement.Transport%2A>
- <xref:System.ServiceModel.NetTcpSecurity.Transport%2A>
- <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>
- [保护服务和客户端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
- [绑定](../../../wcf/bindings.md)
- [配置系统提供的绑定](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [使用绑定配置服务和客户端](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
