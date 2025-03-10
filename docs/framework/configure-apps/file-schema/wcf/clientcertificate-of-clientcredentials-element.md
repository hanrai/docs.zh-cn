---
title: <clientCertificate>of <clientCredentials>元素
ms.date: 03/30/2017
ms.assetid: 3b3fa000-3434-4142-a178-11903bdd2c5d
ms.openlocfilehash: 3450df921da8c72a555c2faf424c51e0063cb235
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69926117"
---
# <a name="clientcertificate-of-clientcredentials-element"></a>\<clientCredentials > 元素\<的 clientCertificate >
定义用于针对服务进行客户端身份验证的 X.509 证书。  
  
 \<system.ServiceModel>  
\<行为 >  
\<endpointBehaviors>  
\<行为 >  
\<clientCredentials>  
\<clientCertificate>  
  
## <a name="syntax"></a>语法  
  
```xml  
<clientCertificate findValue="String"
                   storeLocation="LocalMachine/CurrentUser"
                   storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                   X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`findValue`|一个字符串，包含要在 X.509 证书存储中搜索的值。 此属性中包含的类型必须满足 `X509FindType` 属性值的要求。 默认值为一个空字符串。|  
|`storeLocation`|指定客户端用于向服务验证自身身份的 X.509 证书的位置。 包括以下有效值：<br /><br /> -LocalMachine: 分配给本地计算机的证书存储区。<br />-CurrentUser: 分配给当前用户的证书存储区。<br /><br /> 默认值为 LocalMachine。 此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.StoreLocation>。|  
|`storeName`|指定要搜索的 X.509 证书存储的名称。 包括以下有效值：<br /><br /> 通讯簿其他用户的证书存储区。<br />AuthRoot第三方证书颁发机构 (Ca) 的证书存储区。<br />CertificateAuthority中间证书颁发机构 (Ca) 的证书存储区。<br />禁用吊销的证书的证书存储区。<br />记住个人证书的证书存储区。<br />Root受信任的根证书颁发机构 (Ca) 的证书存储区。<br />TrustedPeople直接受信任的人和资源的证书存储区。<br />TrustedPublisher直接受信任的发布者的证书存储区。<br /><br /> 默认值为 My。 此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.StoreName>。|  
|X509FindType|定义要执行的 X.509 搜索的类型。 `findValue` 属性中包含的类型必须满足此属性的要求。 包括以下有效值：<br /><br /> -FindByThumbPrint<br />-   FindBySubjectName<br />-FindBySubjectDistinguishedName<br />- FindByIssuerName<br />- FindByIssuerDistinguishedName<br />-FindBySerialNumber<br />-   FindByTimeValid<br />-   FindByTimeNotYetValid<br />- FindByTemplateName<br />-   FindByApplicationPolicy<br />-   FindByCertificatePolicy<br />- FindByExtension<br />- FindByKeyUsage<br />-   FindBySubjectKeyIdentifier<br /><br /> 默认值为 FindBySubjectDistinguishedName。 此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.X509FindType>。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|指定用于向服务验证客户端身份的凭据。|  
  
## <a name="remarks"></a>备注  
 此配置元素指定用于对具有此元素的客户端进行身份验证的证书。 有关详细信息，请参阅[如何：指定客户端凭据](../../../wcf/how-to-specify-client-credential-values.md)值。  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ClientCertificate%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A>
- <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>
- [安全行为](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [如何：指定客户端凭据值](../../../wcf/how-to-specify-client-credential-values.md)
- [保护客户端](../../../wcf/securing-clients.md)
- [使用证书](../../../wcf/feature-details/working-with-certificates.md)
- [保护服务和客户端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
