---
title: <legacyImpersonationPolicy> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#legacyImpersonationPolicy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/legacyImpersonationPolicy
helpviewer_keywords:
- <legacyImpersonationPolicy> element
- legacyImpersonationPolicy element
ms.assetid: 6e00af10-42f3-4235-8415-1bb2db78394e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: da01d0dac2e67d6c0131a2b5965472bbd19213fe
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927317"
---
# <a name="legacyimpersonationpolicy-element"></a>\<legacyImpersonationPolicy > 元素
指定 Windows 标识不流经异步点，而不考虑当前线程上执行上下文的流设置。  
  
 \<configuration>  
\<运行时 >  
\<legacyImpersonationPolicy>  
  
## <a name="syntax"></a>语法  
  
```xml  
<legacyImpersonationPolicy    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定不流经异步点, 无论<xref:System.Threading.ExecutionContext>当前线程上的流设置如何。 <xref:System.Security.Principal.WindowsIdentity>|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`false`|<xref:System.Security.Principal.WindowsIdentity>根据当前线程的<xref:System.Threading.ExecutionContext>流设置, 跨异步点流动。 这是默认设置。|  
|`true`|<xref:System.Security.Principal.WindowsIdentity>不流经异步点, 无论<xref:System.Threading.ExecutionContext>当前线程上的流设置如何。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## <a name="remarks"></a>备注  
 在 .NET Framework 版本1.0 和1.1 中, <xref:System.Security.Principal.WindowsIdentity>不在任何用户定义的异步点上流动。 从 .NET Framework 版本2.0 开始, 有一个<xref:System.Threading.ExecutionContext>对象, 该对象包含当前正在执行的线程的相关信息, 并在应用程序域中的异步点之间流动。 <xref:System.Security.Principal.WindowsIdentity>包含在此执行上下文中, 因此也会流过异步点, 这意味着, 如果存在模拟上下文, 它也会流动。  
  
 从 .NET Framework 2.0 开始, 可以使用`<legacyImpersonationPolicy>`元素<xref:System.Security.Principal.WindowsIdentity>指定不流经异步点。  
  
> [!NOTE]
> 公共语言运行时 (CLR) 知道仅使用托管代码执行的模拟操作, 而不是在托管代码之外执行的模拟, 例如通过平台调用到非托管代码或通过直接调用 Win32 函数。 只有托管<xref:System.Security.Principal.WindowsIdentity>对象才能流经异步点, 除非该`alwaysFlowImpersonationPolicy`元素已设置为 true (`<alwaysFlowImpersonationPolicy enabled="true"/>`)。 `alwaysFlowImpersonationPolicy`将元素设置为 true 可指定无论模拟的执行方式如何, Windows 标识总是流经异步点。 有关跨异步点流动非托管模拟的详细信息, 请参阅[ \<alwaysFlowImpersonationPolicy > 元素](alwaysflowimpersonationpolicy-element.md)。  
  
 可以通过两种其他方式更改此默认行为:  
  
1. 在托管代码中, 在每个线程的基础上。  
  
     <xref:System.Threading.ExecutionContext>通过使用、或<xref:System.Security.SecurityContext.SuppressFlow%2A?displayProperty=nameWithType>方法修改和<xref:System.Security.SecurityContext>设置, <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A?displayProperty=nameWithType>可以按线程禁止显示流。 <xref:System.Threading.ExecutionContext.SuppressFlow%2A?displayProperty=nameWithType>  
  
2. 在调用非托管承载接口以加载公共语言运行时 (CLR)。  
  
     如果使用非托管宿主接口 (而不是简单的托管可执行文件) 加载 CLR, 则可以在调用[CorBindToRuntimeEx 函数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)函数时指定特殊标志。 若要为整个进程启用兼容模式, 请将`flags` [CorBindToRuntimeEx 函数](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)的参数设置为 STARTUP_LEGACY_IMPERSONATION。  
  
 有关详细信息, 请参阅[ \<alwaysFlowImpersonationPolicy > 元素](alwaysflowimpersonationpolicy-element.md)。  
  
## <a name="configuration-file"></a>配置文件  
 在 .NET Framework 应用程序中, 此元素只能在应用程序配置文件中使用。  
  
 对于 ASP.NET 应用程序, 可以在\<Windows 文件夹 > \Microsoft.NET\Framework\vx.x.xxxx 目录中找到的 aspnet .config 文件中配置模拟流。  
  
 默认情况下, ASP.NET 使用以下配置设置禁用 aspnet 文件中的模拟流:  
  
``` xml
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
      <alwaysFlowImpersonationPolicy enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
 在 ASP.NET 中, 如果要改为允许模拟流, 则必须显式使用以下配置设置:  
  
```xml  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="false"/>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="example"></a>示例  
 下面的示例演示如何指定不跨异步点流式传输 Windows 标识的旧行为。  
  
```xml  
<configuration>  
   <runtime>  
      <legacyImpersonationPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- [运行时设置架构](index.md)
- [配置文件架构](../index.md)
- [\<alwaysFlowImpersonationPolicy > 元素](alwaysflowimpersonationpolicy-element.md)
