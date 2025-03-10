---
title: <defaultCertificate> 元素
ms.date: 03/30/2017
ms.assetid: f1ddf364-9a00-45d3-b989-ff381c154ce6
ms.openlocfilehash: 93410e815a156f91db1962f05fb1aa6baca7f955
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69919254"
---
# <a name="defaultcertificate-element"></a>\<defaultCertificate > 元素
指定在服务或 STS 未通过协商协议提供证书时要使用的 X.509 证书。  
  
 \<system.ServiceModel>  
\<行为 >  
endpointBehaviors 部分  
\<行为 >  
\<clientCredentials>  
\<serviceCertificate>  
\<defaultCertificate>  
  
## <a name="syntax"></a>语法  
  
```xml  
<defaultCertificate findValue="String"
                    storeLocation=" CurrentUser/LocalMachine"
                    storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                    x509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialiNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|findValue|字符串。 要搜索的值。|  
|x509FindType|枚举。 要搜索的证书字段之一。|  
|storeLocation|枚举。 要搜索的两个系统存储位置之一。|  
|storeName|枚举。 要搜索的系统存储之一。|  
  
## <a name="findvalue-attribute"></a>findValue 属性  
  
|值|描述|  
|-----------|-----------------|  
|String|值取决于搜索的字段（由 X509FindType 属性指定）。 例如，如果搜索指纹，则此值必须为十六进制数字字符串。|  
  
## <a name="x509findtype-attribute"></a>x509FindType 属性  
  
|值|描述|  
|-----------|-----------------|  
|枚举|值包括：FindByThumbprint、Findbysubjectname)、FindBySubjectDistinguishedName、FindByIssuerName、FindByIssuerDistinguishedName、FindBySerialNumber、FindByTimeValid、FindByTimeNotYetValid、FindBySerialNumber、FindByTimeExpired、FindByTemplateName, FindByApplicationPolicy, FindByCertificatePolicy, FindByExtension, FindByKeyUsage, FindBySubjectKeyIdentifier.|  
  
## <a name="storelocation-attribute"></a>storeLocation 属性  
  
|值|描述|  
|-----------|-----------------|  
|枚举|CurrentUser 或 LocalMachine。|  
  
## <a name="storename-attribute"></a>storeName 属性  
  
|值|描述|  
|-----------|-----------------|  
|枚举|值包括：通讯簿、AuthRoot、CertificateAuthority、不允许、My、Root、TrustedPeople 和 TrustedPublisher。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<serviceCertificate>](servicecertificate-of-clientcredentials-element.md)|指定客户端对服务进行身份验证时使用的证书。|  
  
## <a name="remarks"></a>备注  
 对于使用基于证书的消息安全的绑定，此配置元素指定的证书用于加密发送给服务的消息，并期望服务用它来对客户端的应答进行签名。 如果服务未指定任何证书，它只存储要使用的一个证书。  
  
## <a name="example"></a>示例  
 下面的示例指定证书用于 URI 以开头的终结点 `http://www.contoso.com` 和要使用其他不执行证书协商的所有终结点的证书。  
  
```xml  
<serviceCertificate>
  <defaultCertificate findValue="www.contoso.com"
                      storeLocation="LocalMachine"
                      storeName="TrustedPeople"
                      x509FindType="FindByIssuerDistinguishedName" />
  <scopedCertificates>
    <add targetUri="http://www.contoso.com"
         findValue="www.contoso.com"
         storeLocation="LocalMachine"
         storeName="Root"
         x509FindType="FindByIssuerName" />
  </scopedCertificates>
  <authentication revocationMode="Online"
                  trustedStoreLocation="LocalMachine" />
</serviceCertificate>
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Configuration.X509DefaultServiceCertificateElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.DefaultCertificate%2A>
- [使用证书](../../../wcf/feature-details/working-with-certificates.md)
- [\<authentication>](authentication-of-clientcertificate-element.md)
- [保护客户端](../../../wcf/securing-clients.md)
- [保护服务和客户端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
