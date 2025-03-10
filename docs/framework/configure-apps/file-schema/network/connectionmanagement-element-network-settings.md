---
title: <connectionManagement> 元素（网络设置）
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement
- http://schemas.microsoft.com/.NetConfiguration/v2.0#connectionManagement
helpviewer_keywords:
- <connectionManagement> element
- connectionManagement element
ms.assetid: bedccaab-12a2-4511-8f67-e961f249aec6
ms.openlocfilehash: faaba1b9de302ed916ad1a81c7e80b3fb5a67170
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69664157"
---
# <a name="connectionmanagement-element-network-settings"></a>\<connectionManagement > 元素 (网络设置)
指定到网络主机的最大连接数。  
  
 \<configuration>  
\<system.net>  
\<connectionManagement>  
  
## <a name="syntax"></a>语法  
  
```xml  
<connectionManagement>   
</connectionManagement>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
 无。  
  
### <a name="child-elements"></a>子元素  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|[add](add-element-for-connectionmanagement-network-settings.md)|将 IP 地址或 DNS 名称添加到连接管理列表。|  
|[clear](clear-element-for-connectionmanagement-network-settings.md)|清除连接管理列表。|  
|[remove](remove-element-for-connectionmanagement-network-settings.md)|从连接管理列表中删除 IP 地址或 DNS 名称。|  
  
### <a name="parent-elements"></a>父元素  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|[system.net](system-net-element-network-settings.md)|包含指定 .NET Framework 如何连接到网络的设置。|  
  
## <a name="remarks"></a>备注  
 `connectionManagement`元素定义与服务器或服务器组的最大连接数。  
  
## <a name="configuration-files"></a>配置文件  
 此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。  
  
## <a name="example"></a>示例  
 下面的示例将应用程序配置为使用四个到服务器`www.contoso.com`的连接, 以及两个与其他服务器的连接。  
  
```xml  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <add address = "http://www.contoso.com" maxconnection = "4" />  
      <add address = "*" maxconnection = "2" />  
    </connectionManagement>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Net.ServicePoint>
- <xref:System.Net.ServicePointManager>
- [网络设置架构](index.md)
