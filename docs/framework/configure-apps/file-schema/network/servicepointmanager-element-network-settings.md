---
title: <servicePointManager> 元素（网络设置）
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#servicePointManager
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/servicePointManager
helpviewer_keywords:
- servicePointManager element
- <servicePointManager> element
ms.assetid: 6e5def51-3646-4ef6-a7bd-c69151321bec
ms.openlocfilehash: a6a40d97bf16a3125452311e7762617e657ca384
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659147"
---
# <a name="servicepointmanager-element-network-settings"></a>\<servicePointManager > 元素 (网络设置)
配置与网络资源的连接。  
  
 \<configuration>  
\<system.net>  
\<设置 >  
\<servicePointManager>  
  
## <a name="syntax"></a>语法  
  
```xml  
<servicePointManager  
  checkCertificateName="true|false"  
  checkCertificateRevocationList="true|false"  
  encryptionPolicy="AllowNoEncryption|NoEncryption|RequireEncryption"  
  expect100Continue="true|false"  
  useNagleAlgorithm="true|false"  
  enableDnsRoundRobin="true|false"  
  dnsRefreshTimeout="time"  
/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|**特性**|**说明**|  
|-------------------|---------------------|  
|`checkCertificateName`|指定在使用证书之前, 系统是否应验证证书上的名称是否与服务器主机名匹配。 默认值为 `true`。|  
|`checkCertificateRevocationList`|指定在使用证书之前系统是否应检查证书是否已吊销。 默认值为 `false`。|  
|`dnsRefreshTimeout`|指定域名服务 (DNS) 解析与 DNS 轮循机制选项一起缓存的时间长度 (以毫秒为单位)。 默认值是 120,000 毫秒（2 分钟）。|  
|`enableDnsRoundRobin`|指定具有多个 Internet 协议 (IP) 地址的主机名的 DNS 解析是返回所有地址, 还是只返回第一个地址。 默认值为 `false`。|  
|`encryptionPolicy`|指定应用到<xref:System.Net.ServicePointManager>实例上的 SSL/TLS 会话的加密策略。 可能的值等效于<xref:System.Net.Security.EncryptionPolicy>枚举的值。 加密策略设置<xref:System.Security.Authentication.CipherAlgorithmType.Null>为`NoEncryption`时, 需要使用。 默认值为 `RequireEncryption`。|  
|`expect100Continue`|指定 POST 方法是否应该接收`100-continue`来自服务器的响应。 默认值为 `true`。|  
|`useNagleAlgorithm`|指定由服务点管理器控制的连接是否使用 Nagle 算法。 默认值为 `true`。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|[设置](settings-element-network-settings.md)|配置 <xref:System.Net> 命名空间的基本网络选项。|  
  
## <a name="remarks"></a>备注  
  
## <a name="configuration-files"></a>配置文件  
 此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Net.ServicePointManager>
- <xref:System.Net.Security.EncryptionPolicy>
- [网络设置架构](index.md)
