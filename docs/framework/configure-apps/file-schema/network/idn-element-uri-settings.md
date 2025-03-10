---
title: <idn> 元素（Uri 设置）
ms.date: 03/30/2017
ms.assetid: 16c8e869-1791-4cf5-9244-3d3c738f60ec
ms.openlocfilehash: 5fe2eafee702be96bfdca80a06af4a040d9ef0f6
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69664125"
---
# <a name="idn-element-uri-settings"></a>\<idn > 元素 (Uri 设置)
指定是否将国际化域名 (IDN) 分析应用于域名。  
  
## <a name="schema-hierarchy"></a>架构层次结构  
 [\<configuration> 元素](../configuration-element.md)  
  
 [\<Uri > 元素 (Uri 设置)](uri-element-uri-settings.md)  
  
 [\<idn>](idn-element-uri-settings.md)  
  
## <a name="syntax"></a>语法  
  
```xml  
<idn  
  enabled="All|AllExceptIntranet|None"  
/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|`enabled`|指定是否将国际化域名 (IDN) 分析应用于域名。默认值为 none。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|[oma-uri](uri-element-uri-settings.md)|包含指定 .NET Framework 如何处理使用统一资源标识符 (Uri) 表示的 web 地址的设置。|  
  
## <a name="remarks"></a>备注  
 已在<xref:System.Uri> .NET Framework 3.5 中扩展了现有的类。 3.0 SP1 和 2.0 SP1, 支持国际资源标识符 (IRI) 和国际化域名 (IDN)。 当前用户将看不到 .NET Framework 2.0 行为中的任何更改, 除非它们专门启用 IRI 和 IDN 支持。 这确保了 NET Framework 以前版本的应用程序兼容性。  
  
 若要启用对 IRI 的支持, 需要以下两项更改:  
  
1. 将以下行添加到 .NET Framework 2.0 目录下的 machine.config 文件中。  
  
    ```xml  
    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    ```  
  
2. 指定是否要将国际化域名 (IDN) 分析应用于域名, 以及是否应该应用 IRI 分析规则。 这可以在 machine.config 或应用配置文件中完成。  
  
 根据所使用的 DNS 服务器, IDN 有三个可能的值:  
  
- 已启用 idn = 全部  
  
     此值会将任何 Unicode 域名转换为其 Punycode 等效项 (IDN 名称)。  
  
- 启用 idn = AllExceptIntranet  
  
     此值会将本地 Intranet 上的所有 Unicode 域名转换为使用 Punycode 等效项 (IDN 名称)。 在这种情况下, 为了处理本地 Intranet 上的国际名称, 用于 Intranet 的 DNS 服务器应该支持 Unicode 名称解析。  
  
- 启用 idn = 无  
  
     此值不会将任何 Unicode 域名转换为使用 Punycode。 这是与 .NET Framework 2.0 行为一致的默认值。  
  
 启用 IDN 可以将域名中所有 Unicode 标签转换成标签的 Punycode 等同项。 Punycode 名称只包含 ASCII 字符，并且始终以 xn-- 前缀开头。 这样是为了支持 Internet 上的 DNS 服务器，因为大部分 DNS 服务器仅支持 ASCII 字符（参见 RFC 3940）。  
  
### <a name="configuration-files"></a>配置文件  
 此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例演示<xref:System.Uri>类使用的配置, 以支持 IRI 分析和 IDN 名称。  
  
### <a name="code"></a>代码  
  
```xml  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Configuration.IdnElement?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>
- [网络设置架构](index.md)
