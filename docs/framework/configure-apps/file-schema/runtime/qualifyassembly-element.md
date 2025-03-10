---
title: <qualifyAssembly> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#qualifyAssembly
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/qualifyAssembly
helpviewer_keywords:
- container tags, <qualifyAssembly> element
- <qualifyAssembly> element
- qualifyAssembly element
ms.assetid: ad6442f6-1a9d-43b6-b733-04ac1b7f9b82
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4aa90a378630c9aff74923d8e8600aed15a77a5e
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69663505"
---
# <a name="qualifyassembly-element"></a>\<B l y > 元素
指定使用部分名称时应动态加载的程序集全名。  
  
 \<configuration>  
\<运行时 >  
\<assemblyBinding>  
\<qualifyAssembly>  
  
## <a name="syntax"></a>语法  
  
```xml  
      <qualifyAssembly partialName=  
      "PartialAssemblyName"  
                 fullName="FullAssemblyName"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`partialName`|必需的特性。<br /><br /> 指定程序集在代码中出现的部分名称。|  
|`fullName`|必需的特性。<br /><br /> 指定程序集在全局程序集缓存中出现时的完整名称。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`assemblyBinding`|包含有关程序集版本重定向和程序集位置的信息。|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## <a name="remarks"></a>备注  
 使用部分程序集名称调用方法会导致公共语言运行时仅查找应用程序基目录中的程序集。<xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 使用应用程序配置文件中的 **\<b l y >** 元素可提供完整的程序集信息 (名称、版本、公钥标记和区域性), 并导致公共语言运行时在全局程序集缓存。  
  
 **FullName**特性必须包含程序集标识的四个字段: 名称、版本、公钥标记和区域性。 **PartialName**属性必须部分引用程序集。 必须至少指定程序集的文本名称 (最常见的情况), 但也可以包括版本、公钥标记或区域性 (或四个 (但不是全部四个) 的任意组合。 **PartialName**必须与在调用中指定的名称相匹配。 例如, 你不能在`"math"`配置文件中将指定为**partialName**属性, 然后`Assembly.Load("math, Version=3.3.3.3")`在代码中调用。  
  
## <a name="example"></a>示例  
 下面的示例以逻辑方式将`Assembly.Load("math")`调用`Assembly.Load("math,version=1.0.0.0,publicKeyToken=a1690a5ea44bab32,culture=neutral")`转换为。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <qualifyAssembly partialName="math"   
                         fullName=  
"math,version=1.0.0.0,publicKeyToken=a1690a5ea44bab32,culture=neutral"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- [运行时设置架构](index.md)
- [运行时如何定位程序集](../../../deployment/how-the-runtime-locates-assemblies.md)
- [部分程序集引用](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/0a7zy9z5(v=vs.100))
