---
title: <cryptographySettings> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#cryptographySettings
helpviewer_keywords:
- cryptographySettings element
- <cryptographySettings> element
ms.assetid: 6201b7da-bcb7-49f7-b9f5-ba1fe05573b9
ms.openlocfilehash: 462db50a42e55c0c5a9570317ceeeb0ae69215a0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927653"
---
# <a name="cryptographysettings-element"></a>\<G s > 元素
包含加密设置。  
  
 \<configuration>  
\<mscorlib>  
\<cryptographySettings>  
  
## <a name="syntax"></a>语法  
  
```xml  
      <cryptographySettings>   
</cryptographySettings>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
 无。  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<cryptoNameMapping>](cryptonamemapping-element.md)|包含类到友好名称的映射。|  
|[\<oidMap>](oidmap-element.md)|包含与类的 ASN 对象标识符 (OID) 映射。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`mscorlib`|`cryptographySettings`包含元素。|  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 **\<g s >** 元素包含加密名称映射和 OID 映射。 此示例将配置运行时, <xref:System.Security.Cryptography.HashAlgorithm.Create%2A?displayProperty=nameWithType>以便`MyHashClass`返回对象, `MyCryptoClass`类映射到对象标识符1.3.36.2.1。  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyHash="MyHashClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
               <cryptoClass   MyCrypto="MyCryptoClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="System.Security.Cryptography.HashAlgorithm"  
                       class="MyHash"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.36.3.2.1"   name="MyCryptoClass"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- [配置文件架构](../index.md)
- [加密设置架构](index.md)
- [Cryptographic Services](../../../../standard/security/cryptographic-services.md)
