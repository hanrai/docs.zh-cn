---
title: <bypassTrustedAppStrongNames> 元素
ms.date: 03/30/2017
helpviewer_keywords:
- strong-name bypass feature
- bypassTrustedAppStrongNames element
- strong-named assemblies, loading into trusted application domains
- <bypassTrustedAppStrongNames> element
ms.assetid: 71b2ebf6-3843-41e2-ad52-ffa5cd083a40
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 92873277b4b25e4c1c5981628187078ac7cb5704
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69920891"
---
# <a name="bypasstrustedappstrongnames-element"></a>\<bypassTrustedAppStrongNames> 元素
指定是否在加载到完全信任<xref:System.AppDomain>的完全信任程序集上绕过强名称验证。  
  
 \<configuration>  
\<运行时 >  
\<bypassTrustedAppStrongNames>  
  
## <a name="syntax"></a>语法  
  
```xml  
<bypassTrustedAppStrongNames    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`enabled`|必需的特性。<br /><br /> 指定是否启用回避功能, 以避免为完全信任程序集验证强名称。 当启用此功能时, 加载程序集时, 不会验证强名称是否正确。 默认值为 `true`。|  
  
## <a name="enabled-attribute"></a>enabled 特性  
  
|值|描述|  
|-----------|-----------------|  
|`true`|将程序集加载到完全信任<xref:System.AppDomain>时, 不会验证完全信任程序集上的强名称签名。 这是默认设置。|  
|`false`|将程序集加载到完全信任<xref:System.AppDomain>时, 会验证完全信任程序集上的强名称签名。 仅对签名正确性检查强名称签名;与另一个匹配的强名称没有比较。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|  
  
## <a name="remarks"></a>备注  
 强名称跳过功能可避免完全信任程序集的强名称签名验证的系统开销。  
  
 跳过功能适用于使用强名称进行签名及具有以下特征的任何程序集：  
  
- 完全受信任, <xref:System.Security.Policy.StrongName>无需证据 (如具有`MyComputer`区域证据)。  
  
- 加载到完全受信任的 <xref:System.AppDomain>。  
  
- 加载自该 <xref:System.AppDomain> 的 <xref:System.AppDomainSetup.ApplicationBase%2A> 属性下的某个位置。  
  
- 签名没有延迟。  
  
> [!NOTE]
> 如果对计算机上的所有应用程序使用注册表项关闭了绕过功能, 则此配置文件设置将不起作用。 有关详细信息，请参阅[如何：禁用强名称绕过功能](../../../app-domains/how-to-disable-the-strong-name-bypass-feature.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何指定对完全信任程序集的强名称签名进行验证的行为。  
  
```xml  
<configuration>  
   <runtime>  
      <bypassTrustedAppStrongNames enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- [运行时设置架构](index.md)
- [配置文件架构](../index.md)
- [如何：禁用强名称跳过功能](../../../app-domains/how-to-disable-the-strong-name-bypass-feature.md)
