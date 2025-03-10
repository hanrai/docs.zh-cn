---
title: <gcAllowVeryLargeObjects> 元素
ms.date: 03/30/2017
helpviewer_keywords:
- gcAllowVeryLargeObjects element
- <gcAllowVeryLargeObjects> element
ms.assetid: 5c7ea24a-39ac-4e5f-83b7-b9f9a1b556ab
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 643e28217d41e825f0b3a3f4a4f062c30835cae8
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040663"
---
# <a name="gcallowverylargeobjects-element"></a>\<gcAllowVeryLargeObjects > 元素
在 64 位平台上，启用总大小大于 2 千兆字节 (GB) 的数组。  
  
 \<配置 > 元素  
\<运行时 > 元素  
\<gcAllowVeryLargeObjects > 元素  
  
## <a name="syntax"></a>语法  
  
```xml  
<gcAllowVeryLargeObjects    
   enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定是否在64位平台上启用了总大小中大于 2 GB 的数组。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|总大小中大于 2 GB 的数组未启用。 这是默认设置。|  
|`true`|在64位平台上, 总大小中已启用大于 2 GB 的数组。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
  
## <a name="remarks"></a>备注  
 在应用程序配置文件中使用此元素可启用大小大于 2 GB 的数组, 但不会更改对象大小或数组大小的其他限制:  
  
- 数组中元素的最大数目为<xref:System.UInt32.MaxValue?displayProperty=nameWithType>。  
  
- 任何单个维度中的最大索引为 2147483591 (0x7FFFFFC7) (对于字节数组) 和单字节结构数组, 2146435071 (0X7FEFFFFF) 用于其他类型。  
  
- 字符串和其他非数组对象的最大大小不变。  
  
> [!CAUTION]
> 在启用此功能之前, 请确保应用程序不包含不安全代码, 该代码假定所有数组大小均小于 2 GB。 例如, 使用数组作为缓冲区的不安全代码可能容易受到缓冲区溢出的攻击, 因为假设数组不会超过 2 GB。  
  
## <a name="example"></a>示例  
 下面的示例演示如何为应用程序启用此功能。  
  
```xml  
<configuration>  
  <runtime>  
    <gcAllowVeryLargeObjects enabled="true" />  
  </runtime>  
</configuration>  
```  
  
## <a name="supported-in"></a>受以下版本支持：

.NET Framework 4.5 及更高版本

## <a name="see-also"></a>请参阅

- [运行时设置架构](index.md)
- [配置文件架构](../index.md)
