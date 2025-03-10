---
title: <appDomainManagerAssembly> 元素
ms.date: 03/30/2017
helpviewer_keywords:
- <appDomainManagerAssembly> element
- appDomainManagerAssembly element
ms.assetid: c7c56e39-a700-44f5-b94e-411bfce339d9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3a293af73fde5ee72ba02c7e6613e9c57eae1b9b
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69658947"
---
# <a name="appdomainmanagerassembly-element"></a>\<B l y > 元素
指定为过程中的默认应用程序域提供应用程序域管理器的程序集。  
  
 \<configuration>  
\<运行时 >  
\<appDomainManagerAssembly>  
  
## <a name="syntax"></a>语法  
  
```xml  
<appDomainManagerAssembly   
   value="assembly display name" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`value`|必需的特性。 指定为进程中的默认应用程序域提供应用程序域管理器的程序集的显示名称。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## <a name="remarks"></a>备注  
 若要指定应用程序域管理器的类型, 必须同时指定此元素和[ \<y p e >](appdomainmanagertype-element.md)元素。 如果未指定这些元素中的任何一个, 则会忽略另一个。  
  
 在加载默认应用程序域时, <xref:System.TypeLoadException>如果指定的程序集不存在, 或者如果程序集不包含[ \<y p e >](appdomainmanagertype-element.md)元素指定的类型, 则将引发; 该进程将无法start. 如果找到程序集, 但版本信息不匹配, <xref:System.IO.FileLoadException>则会引发。  
  
 指定默认应用程序域的应用程序域管理器类型时, 从默认应用程序域创建的其他应用程序域将继承应用程序域管理器类型。 <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=nameWithType>使用和<xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=nameWithType>属性为新的应用程序域指定不同的应用程序域管理器类型。  
  
 指定应用程序域管理器类型要求应用程序具有完全信任。 (例如, 在桌面上运行的应用程序具有完全信任。)如果应用程序不具有完全信任, <xref:System.TypeLoadException>则会引发。  
  
 有关程序集显示名称的格式, 请参见<xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType>属性。  
  
 此配置元素仅在 .NET Framework 4 及更高版本中可用。  
  
## <a name="example"></a>示例  
 下面的示例演示如何指定进程的默认应用程序域的应用程序域管理器是`MyMgr` `AdMgrExample`程序集中的类型。  
  
```xml  
<configuration>  
   <runtime>  
      <appDomainManagerType value="MyMgr" />  
      <appDomainManagerAssembly   
         value="AdMgrExample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=6856bccf150f00b3" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=nameWithType>
- <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=nameWithType>
- [\<Y p e > 元素](appdomainmanagertype-element.md)
- [运行时设置架构](index.md)
- [配置文件架构](../index.md)
- [SetAppDomainManagerType 方法](../../../unmanaged-api/hosting/iclrcontrol-setappdomainmanagertype-method.md)
