---
title: <configSections> 的 <clear> 元素
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/clear
helpviewer_keywords:
- clear Element
- <clear> Element
ms.assetid: 77f1d761-ff45-4001-8f36-3a3e5c41fa63
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: c06fca8b83638fb47bedb21863cb9b200cd211f3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927734"
---
# <a name="clear-element-for-configsections"></a>\<清除 configSections 的\<> 元素 >

清除所有之前定义的部分和节组。

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp;[ **\<configSections>** ](configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<clear>**

## <a name="syntax"></a>语法

```xml
<clear/>
```

## <a name="attribute"></a>特性

|           | 描述 |
| --------- | ----------- |
| **名称**  | 必需的特性。<br><br>指定要删除的节或节组的名称。 |

## <a name="parent-element"></a>父元素

|     | 描述 |
| --- | ----------- |
| [ **configSections>\<** 元素](configsections-element-for-configuration.md) | 包含配置节和命名空间声明。 |

## <a name="child-elements"></a>子元素

无

## <a name="remarks"></a>备注

**\<Clear >** 元素将从应用程序中删除之前在当前配置文件或配置文件层次结构中的更高级别定义的所有节和节组。

## <a name="example"></a>示例

此示例定义了计算机配置文件和应用程序配置文件, 并演示了如何使用应用程序配置文件中的 **\<clear >** 元素清除之前在计算机配置中定义的部分文件.

以下计算机配置文件代码声明了两部分:  **\<sampleSection >** 和 **\<anotherSampleSection >** , 这些部分在应用程序配置文件之前读取:

```xml
<!-- Machine.config file -->
<configuration>
  <configSections>
    <section name="sampleSection"
             type="System.Configuration.SingleTagSectionHandler" />
    <section name="anotherSampleSection"
             type="System.Configuration.NameValueSectionHandler" />
  </configSections>
  <sampleSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

以下应用程序配置文件代码将清除以前声明的所有部分。 应用程序不能使用或检索在计算机配置文件中声明的任一部分中的设置。 但是, 它可以使用 **\<anotherSection >** 的 **\<** 设置, 因为它位于 clear > 元素之后。

```xml
<!-- Application configuration file -->
<configuration>
  <configSections>
    <clear/>
    <section name="anotherSection"
             type="System.Configuration.NameValueSectionHandler" />
  </configSections>
  <anotherSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a>配置文件

此元素可用于应用程序配置文件、计算机配置文件 (*machine.config*) 和不在应用程序目录级别的 web.config 文件。

## <a name="see-also"></a>请参阅

- [.NET Framework 的配置文件架构](index.md)
