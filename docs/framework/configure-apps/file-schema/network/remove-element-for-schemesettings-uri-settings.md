---
title: schemeSettings 的 <remove> 元素（Uri 设置）
ms.date: 03/30/2017
ms.assetid: 4095ba51-de20-4f87-b562-018abe422c91
ms.openlocfilehash: 4a891eb8a2fd2d66b6435e2ae774ecd4a157c0f9
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659224"
---
# <a name="remove-element-for-schemesettings-uri-settings"></a>\<删除 schemeSettings 的 > 元素 (Uri 设置)
删除方案名称的方案设置。  
  
 \<configuration>  
\<uri >  
\<schemeSettings>  
\<remove>  
  
## <a name="syntax"></a>语法  
  
```xml  
<remove
  name="http|https"
/>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|NAME|应用此设置的方案名称。 唯一受支持的值为 name = "http" 和 name = "https"。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<schemeSettings> 元素（Uri 设置）](schemesettings-element-uri-settings.md)|指定如何分析特定方案的 <xref:System.Uri>。|  
  
## <a name="remarks"></a>备注  
 默认情况下, <xref:System.Uri?displayProperty=nameWithType>在执行路径压缩之前, 类会取消转义编码的路径分隔符。 这是作为一种安全机制实现的, 针对以下攻击:  
  
 `http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 如果将此 URI 向下传递到模块, 而不是正确处理百分号编码字符, 则可能会导致服务器执行以下命令:  
  
 `c:\Windows\System32\cmd.exe /c dir c:\`  
  
 出于此原因, <xref:System.Uri?displayProperty=nameWithType>类首先取消转义路径分隔符, 然后应用路径压缩。 将上述恶意 URL 传递到<xref:System.Uri?displayProperty=nameWithType>类构造函数的结果将生成以下 URI:  
  
 `http://www.microsoft.com/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 使用特定方案的 schemeSettings 配置选项, 可以将此默认行为修改为不取消转义百分号编码的路径分隔符。  
  
## <a name="configuration-files"></a>配置文件  
 此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。  
  
## <a name="example"></a>示例  
 下面的示例演示了<xref:System.Uri>类使用的配置, 该配置删除了 http 方案的任何方案设置。  
  
```xml  
<configuration>  
  <uri>  
    <schemeSettings>  
      <remove name="http"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Configuration.SchemeSettingElement?displayProperty=nameWithType>
- <xref:System.Configuration.SchemeSettingElementCollection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection.SchemeSettings%2A?displayProperty=nameWithType>
- <xref:System.GenericUriParserOptions?displayProperty=nameWithType>
- <xref:System.Uri?displayProperty=nameWithType>
- [网络设置架构](index.md)
