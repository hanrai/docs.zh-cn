---
title: <add><listeners>的元素<trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/add
helpviewer_keywords:
- initializeData attribute
- <add> element for <listeners>
- add element for <listeners>
ms.assetid: 81e804a3-ef11-4d39-bbde-bfa012c179e2
ms.openlocfilehash: d4ff919991ab1505b2845a225706d32cc1e57d0a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69920574"
---
# <a name="add-element-for-listeners-for-trace"></a>\<为\<跟踪 > 添加\<侦听器 > > 元素
向**侦听器**集合添加侦听器。  
  
 \<configuration>  
\<system.diagnostics>  
\<trace>  
\<侦听器 >  
\<add>  
  
## <a name="syntax"></a>语法  
  
```xml  
<add name="name"   
     type="trace listener class name, Version, Culture, PublicKeyToken"  
     initializeData="data"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|**type**|必需的特性。<br /><br /> 指定侦听器的类型。 必须使用满足指定[完全限定的类型名称](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)中指定的要求的字符串。|  
|**initializeData**|可选特性。<br /><br /> 传递到指定类的构造函数的字符串。|  
|**名称**|可选特性。<br /><br /> 指定侦听器的名称。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<filter>](filter-element-for-add-for-listeners-for-trace.md)|将筛选器添加到跟踪的`Listeners`集合中的侦听器。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`listeners`|指定用于收集、存储和路由消息的侦听器。 侦听器将跟踪输出定向到适当的目标。|  
|`system.diagnostics`|为 ASP.NET 配置节指定根元素。|  
|`trace`|包含用于收集、存储和路由跟踪消息的侦听器。|  
  
## <a name="remarks"></a>备注  
 和类共享相同的侦听器集合。 <xref:System.Diagnostics.Debug> <xref:System.Diagnostics.Trace> 如果将侦听器对象添加到其中一个类的集合中, 则其他类将使用同一侦听器。 侦听器类派生自<xref:System.Diagnostics.TraceListener>。  
  
 如果未指定`name`跟踪侦听器的属性<xref:System.Diagnostics.TraceListener.Name%2A> , 则跟踪侦听器的默认值为空字符串 ("")。 如果你的应用程序只有一个侦听器, 则可以在不指定名称的情况下进行添加, 并通过为该名称指定一个空字符串来将其删除。 但是, 如果应用程序有多个侦听器, 则应为每个跟踪侦听器指定唯一的名称, 以便在<xref:System.Diagnostics.Debug.Listeners%2A>和<xref:System.Diagnostics.Trace.Listeners%2A>集合中标识和管理单个跟踪侦听器。  
  
> [!NOTE]
> 添加具有相同类型且具有相同名称的多个跟踪侦听器会导致只将该类型和名称的一个跟踪侦听器添加到`Listeners`集合中。 但是, 可以通过编程方式将多个相同的`Listeners`侦听器添加到集合中。  
  
 **InitializeData**属性的值取决于所创建的侦听器的类型。 并非所有跟踪侦听器都需要指定**initializeData**。  
  
> [!NOTE]
> 使用`initializeData`属性时, 可能会收到编译器警告 "未声明 ' initializeData ' 特性"。 之所以出现此警告<xref:System.Diagnostics.TraceListener>, 是因为配置设置是针对抽象基类验证的, 后者不`initializeData`识别属性。 通常, 对于具有采用参数的构造函数的跟踪侦听器实现, 你可以忽略此警告。  
  
 下表显示了 .NET Framework 附带的跟踪侦听器, 并说明了其**initializeData**属性的值。  
  
|跟踪侦听器类|initializeData 特性值|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A>构造函数的`useErrorStream`值。  将属性设置为 "`true`" 可将<xref:System.Console.Error%2A?displayProperty=nameWithType>跟踪和调试输出写入; `initializeData``false`要<xref:System.Console.Out%2A?displayProperty=nameWithType>写入的 ""。|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType>|写入的<xref:System.Diagnostics.DelimitedListTraceListener>文件的名称。|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|现有事件日志源的名称。|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.EventSchemaTraceListener>写入的文件的名称。|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.TextWriterTraceListener>写入的文件的名称。|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.XmlWriterTraceListener>写入的文件的名称。|  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 **\<添加>** 元素添加侦听器`MyListener`并`MyEventListener`到**侦听器**集合。 `MyListener`创建一个名`MyListener.log`为的文件, 并将输出写入文件。 `MyEventListener`在事件日志中创建一个条目。  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
            <add name="MyEventListener"  
                 type="System.Diagnostics.EventLogTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"                 initializeData="MyConfigEventLog"/>  
            <add name="configConsoleListener"  
                 type="System.Diagnostics.ConsoleTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.Debug>
- <xref:System.Diagnostics.EventLogTraceListener>
- <xref:System.Diagnostics.ConsoleTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- [跟踪和调试设置架构](index.md)
- [跟踪侦听器](../../../debug-trace-profile/trace-listeners.md)
