---
title: <add><listeners>的元素<source>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/add
helpviewer_keywords:
- initializeData attribute
- add element for <listeners> for <source>
- <add> element for <listeners> for <source>
ms.assetid: 4ce36ac1-81ef-48e8-b8b2-b5a5b0e2adcb
ms.openlocfilehash: 96bfde3ec425f6f77d1d655808d155eb0e6fcd0f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927202"
---
# <a name="add-element-for-listeners-for-source"></a>\<为源 > 的\< \<侦听器 > 添加 > 元素
将侦听器添加到跟踪源的 `Listeners` 集合中。  
  
 \<configuration>  
\<system.diagnostics>  
\<源 >  
\<源 >  
\<侦听器 >  
\<add>  
  
## <a name="syntax"></a>语法  
  
```xml  
<add name="name"   
  type="TraceListenerClassName, Version, Culture, PublicKeyToken"  
  initializeData="data"/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`type`|必需的属性, 除非引用`sharedListeners`集合中的侦听器, 在这种情况下, 只需按名称引用它 (请参阅[示例](#example))。<br /><br /> 指定侦听器的类型。 必须使用满足指定[完全限定的类型名称](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)中指定的要求的字符串。|  
|`initializeData`|可选特性。<br /><br /> 传递到指定类的构造函数的字符串。 如果类不具有采用字符串的构造函数, 则会引发。<xref:System.Configuration.ConfigurationException>|  
|`name`|可选特性。<br /><br /> 指定侦听器的名称。|  
|`traceOutputOptions`|可选特性。<br /><br /> 指定跟踪<xref:System.Diagnostics.TraceListener.TraceOutputOptions%2A>侦听器的属性值。|  
|[自定义属性]|可选属性。<br /><br /> 为该侦听器的<xref:System.Diagnostics.TraceListener.GetSupportedAttributes%2A>方法所标识的侦听器特定的特性指定值。 <xref:System.Diagnostics.DelimitedListTraceListener.Delimiter%2A>是<xref:System.Diagnostics.DelimitedListTraceListener>类独有的额外特性的一个示例。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<filter>](filter-element-for-add-for-listeners-for-source.md)|将筛选器添加到跟踪源的 `Listeners` 集合中的侦听器。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定用于收集、存储和路由消息的跟踪侦听器以及对跟踪开关设置的级别。|  
|`sources`|包含用于启动跟踪消息的跟踪源。|  
|`source`|指定用于启动跟踪消息的跟踪源。|  
|`listeners`|指定用于收集、存储和路由消息的侦听器。|  
  
## <a name="remarks"></a>备注  
 随 .NET Framework 附带的侦听器类派生自<xref:System.Diagnostics.TraceListener>类。  
  
 如果未指定`name`跟踪侦听器的属性, 则跟踪侦听器的<xref:System.Diagnostics.TraceListener.Name%2A>属性默认为空字符串 ("")。 如果你的应用程序只有一个侦听器, 则可以在不指定名称的情况下添加它, 并且可以通过为名称指定空字符串来删除它。 但是, 如果你的应用程序有多个侦听器, 则应为每个跟踪侦听器指定唯一的名称, 以便你可以在<xref:System.Diagnostics.TraceSource.Listeners%2A?displayProperty=nameWithType>集合中标识和管理单个跟踪侦听器。  
  
> [!NOTE]
> 添加具有相同类型且具有相同名称的多个跟踪侦听器会导致只将该类型和名称的一个跟踪侦听器添加到`Listeners`集合中。 但是, 可以通过编程方式将多个相同的`Listeners`侦听器添加到集合中。  
  
 该`initializeData`属性的值取决于所创建的侦听器的类型。 并非所有跟踪侦听器都要求您指定`initializeData`。  
  
> [!NOTE]
> 使用`initializeData`属性时, 可能会收到编译器警告 "未声明 ' initializeData ' 特性"。 之所以出现此警告<xref:System.Diagnostics.TraceListener>, 是因为配置设置是针对抽象基类验证的, 后者不`initializeData`识别属性。 通常, 对于具有采用参数的构造函数的跟踪侦听器实现, 你可以忽略此警告。  
  
 下表显示了 .NET Framework 附带的跟踪侦听器, 并描述了其`initializeData`属性的值。  
  
|跟踪侦听器类|initializeData 特性值|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A>构造函数的`useErrorStream`值。  将属性设置为 "`true`" 可将跟踪和调试输出写入标准错误流; 将该属性设置为`false`"" 可写入标准输出流。 `initializeData`|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType>|写入的<xref:System.Diagnostics.DelimitedListTraceListener>文件的名称。|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|现有事件日志源的名称。|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.EventSchemaTraceListener>写入的文件的名称。|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.TextWriterTraceListener>写入的文件的名称。|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>|<xref:System.Diagnostics.XmlWriterTraceListener>写入的文件的名称。|  
  
## <a name="configuration-file"></a>配置文件  
 此元素可在计算机配置文件 (Machine.config) 和应用程序配置文件中使用。  
  
## <a name="example"></a>示例  
 下面的示例演示`<add>`如何使用元素将侦听器`console`和`textListener` `Listeners`集合添加到跟踪源`TraceSourceApp`的集合中。 `textListener`侦听器将跟踪输出写入文件 myListener。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console"   
            type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="textListener"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"   
        type="System.Diagnostics.TextWriterTraceListener"   
        initializeData="myListener.log"/>  
    </sharedListeners>  
    <switches>  
      <add name="sourceSwitch" value="Warning"/>  
    </switches>  
  </system.diagnostics>  
</configuration>   
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.TraceListener>
- [跟踪和调试设置架构](index.md)
- [跟踪侦听器](../../../debug-trace-profile/trace-listeners.md)
