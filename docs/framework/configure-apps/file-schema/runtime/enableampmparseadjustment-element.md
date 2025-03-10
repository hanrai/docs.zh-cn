---
title: <EnableAmPmParseAdjustment> 元素
ms.date: 03/30/2017
ms.assetid: fda998a5-f538-4f8b-a18c-ee7f35e16938
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 46cf37ee800c05eb7fe12e8491ad3b2130c3a04d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69920824"
---
# <a name="enableampmparseadjustment-element"></a>\<EnableAmPmParseAdjustment > 元素
确定日期和时间分析方法是否使用经过调整的规则集来分析包含 day、month、hour 和 AM/PM 指示符的日期字符串。  
  
 \<configuration>  
 \<运行时 >  
\<EnableAmPmParseAdjustment>  
  
## <a name="syntax"></a>语法  
  
```xml  
<EnableAmPmParseAdjustment enabled="0"|"1" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定日期和时间分析方法是否使用经过调整的规则集来分析只包含 day、month、hour 和 AM/PM 指示符的日期字符串。|  
  
### <a name="enabled-attribute"></a>enabled 特性  
  
|值|Description|  
|-----------|-----------------|  
|0|日期和时间分析方法不使用调整的规则来分析日期字符串, 这些字符串只包含日、月、小时和 AM/PM 指示符。|  
|1|日期和时间分析方法使用经过调整的规则, 用于分析日期字符串, 这些字符串只包含日、月、小时和 AM/PM 指示符。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关运行时初始化选项的信息。|  
  
## <a name="remarks"></a>备注  
 `<EnableAmPmParseAdjustment>`元素控制以下方法如何分析包含数字日和月后跟一个小时和 AM/PM 指示符的日期字符串 (例如 "4/10 6 AM"):  
  
- <xref:System.DateTime.Parse%2A?displayProperty=nameWithType>  
  
- <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType>  
  
- <xref:System.DateTime.TryParse%2A?displayProperty=nameWithType>  
  
- <xref:System.DateTimeOffset.TryParse%2A?displayProperty=nameWithType>  
  
- <xref:System.Convert.ToDateTime%2A?displayProperty=nameWithType>  
  
 其他模式不受影响。  
  
 `<EnableAmPmParseAdjustment>`元素对<xref:System.DateTime.TryParseExact%2A?displayProperty=nameWithType>、、和<xref:System.DateTimeOffset.ParseExact%2A?displayProperty=nameWithType>方法不起作用<xref:System.DateTimeOffset.TryParseExact%2A?displayProperty=nameWithType>。 <xref:System.DateTime.ParseExact%2A?displayProperty=nameWithType>  
  
> [!IMPORTANT]
> 在.NET Core 和.NET Native，默认情况下启用的调整后的 AM/PM 分析规则。  
  
 如果未启用解析调整规则, 则会将字符串的第一个数字解释为12小时制的小时, 而除 AM/PM 指示符之外的字符串的其余部分将被忽略。 解析方法返回的日期和时间由当前日期和从日期字符串提取的日期中的小时组成。  
  
 如果启用了解析调整规则, 则分析方法会将日期和月份解释为属于当前年份, 并将时间解释为12小时制的小时。  
  
 <xref:System.DateTime>下表说明了<xref:System.DateTime.Parse%28System.String%29?displayProperty=nameWithType>当使用方法分析字符串 " `<EnableAmPmParseAdjustment>` 4/10 6 AM" (元素的`enabled`属性设置为 "0" 或 "1") 时, 值中的差异。 它假定今天的日期为2017年1月5日, 并使用指定的区域性的 "G" 格式字符串来显示日期。  
  
|区域性名称|enabled = "0"|enabled = "1"|  
|------------------|------------------|------------------|  
|en-US|上午 1/5/2017 4:00:00|上午 4/10/2017 6:00:00|  
|en-GB|5/1/2017 6:00:00|10/4/2017 6:00:00|  
  
## <a name="see-also"></a>请参阅

- [\<运行时 > 元素](runtime-element.md)
- [\<configuration> 元素](../configuration-element.md)
