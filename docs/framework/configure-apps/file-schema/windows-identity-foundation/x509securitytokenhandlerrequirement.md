---
title: <x509SecurityTokenHandlerRequirement>
ms.date: 03/30/2017
ms.assetid: aca22c2c-5ae7-42af-9bbd-15c2524692ce
author: BrucePerlerMS
ms.openlocfilehash: 2851820460a34d62175929b48ad57914df557059
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69945185"
---
# <a name="x509securitytokenhandlerrequirement"></a>\<x509SecurityTokenHandlerRequirement>
提供<xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>类或派生类的可选配置。  
  
 \<system.identityModel>  
\<identityConfiguration>  
\<securityTokenHandlers>  
\<add>  
\<x509SecurityTokenHandlerRequirement>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <add type="System.IdentityModel.Tokens.X509SecurityTokenHandler, System.IdentityModel">  
        <x509SecurityTokenHandlerRequirement>  
          mapToWindows=xs:boolean  
          certificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
          certificateValidator="Namespace.Class, Assembly"  
          revocationMode="NoCheck||Offline||Online"  
          trustedStoreLocation="CurrentUser||LocalMachine"  
        </x509SecurityTokenHandlerRequirement>  
      </add>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|certificateValidationMode|一个<xref:System.ServiceModel.Security.X509CertificateValidationMode>值, 该值指定要用于 x.509 证书的验证模式。 默认值为 "PeerOrChainTrust"。|  
|mapToWindows|指定令牌处理程序是否应使用传入 UPN 声明将验证令牌映射到 Windows 帐户。 默认值为 "false"。|  
|revocationMode|一个<xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>值, 该值指定要用于 x.509 证书的吊销模式。 默认值为 "Online"。|  
|trustedStoreLocation|一个<xref:System.Security.Cryptography.X509Certificates.StoreLocation>值, 该值指定 x.509 证书存储区。 默认值为 "LocalMachine"。|  
|certificateValidator|派生自的自定义类型<xref:System.IdentityModel.Selectors.X509CertificateValidator>。 如果该`certificateValidationMode`属性为 "Custom", 则此类型的实例将用于颁发者证书验证。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<add>](add.md)|将指定的安全令牌处理程序添加到令牌处理程序集合。|  
  
## <a name="example"></a>示例  
  
```xml  
<add type="System.IdentityModel.Tokens.X509SecurityTokenHandler, System.IdentityModel">  
    <x509SecurityTokenHandlerRequirement mapToWindows="true"   
                                         certificateValidationMode="PeerOrChainTrust"   
                                         revocationMode="Online"   
                                         trustedStoreLocation="LocalMachine" />  
</add>  
```
