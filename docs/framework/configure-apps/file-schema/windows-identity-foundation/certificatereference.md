---
title: <certificateReference>
ms.date: 03/30/2017
ms.assetid: 2ac8bc14-e9f1-48fb-b662-f5991558fbe4
author: BrucePerlerMS
ms.openlocfilehash: da8ea128466457409334cd0b4ee3246a923f969a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69941935"
---
# <a name="certificatereference"></a>\<certificateReference>
指定用于在证书存储中查找和验证 x.509 证书的设置。  
  
 \<system.identityModel.services>  
\<federationConfiguration>  
\<serviceCertificate>  
\<certificateReference>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.identityModel.services>  
  <federationConfiguration>  
    <serviceCertificate>  
      <certificateReference   
        storeName="AddressBook||AuthRoot||CertificateAuthority||Disallowed||My||Root||TrustedPeople||TrustedPublisher"  
        storeLocation="CurrentUser||LocalMachine"  
        x509FindType="FindByThumbprint||FindBySubjectName||FindBySubjectDistinguishedName||FindByIssuerName||FindByIssuerDistinguishedName||FindBySerialNumber||FindByTimeValid||FindByTimeNotYetValid||FindByTimeExpired||FindByTemplateName||FindByApplicationPolicy||FindByCertificatePolicy||FindByExtension||FindByKeyUsage||FindBySubjectKeyIdentifier"  
        findValue=xs:String  
        isChainIncluded=xs:Boolean >  
      </certificateReference>  
    </serviceCertificate>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|storeName|X.509 证书存储的名称。 默认值为 "My"。 可选。|  
|storeLocation|一个<xref:System.Security.Cryptography.X509Certificates.StoreLocation>值, 该值指定 x.509 证书存储区的位置。 默认值为 "LocalMachine"。 可选。|  
|x509FindType|一个<xref:System.Security.Cryptography.X509Certificates.X509FindType>值, 该值指定要执行的搜索的类型。 默认值为 "FindBySubjectDistinguishedName"。 可选。|  
|findValue|要在 X.509 证书存储区中搜索的值。 可选。|  
|isChainIncluded|指定是否应通过使用证书链来执行验证。 默认值为 "true";验证是通过使用证书链来执行的。 可选。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<serviceCertificate>](servicecertificate.md)|配置用于加密和解密令牌的证书。|  
  
## <a name="remarks"></a>备注  
 `<certificateReference>`元素指定用于在证书存储区中查找和验证 x.509 证书的设置。 指定为`<serviceCertificate>`元素的子元素时, 它将指定用于加密和解密令牌的 x.509 证书的位置和验证设置。 元素由<xref:System.ServiceModel.Configuration.CertificateReferenceElement>类表示。 `<certificateReference>`
