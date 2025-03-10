---
title: mc:Ignorable 特性
ms.date: 03/30/2017
helpviewer_keywords:
- mc XML namespace prefix [WPF]
- mc:Ignorable attribute
- XML [WPF], mc namespace prefix
- XAML [WPF], mc:Ignorable attribute
- mc:ProcessContent attribute
- XAML [WPF], mc:ProcessContent attribute
ms.assetid: acd9a6ef-b7ca-4146-abb6-60f3b366e9ec
ms.openlocfilehash: b68909d94ad8cc5bba75b2c520db82c5ccf1b922
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70206186"
---
# <a name="mcignorable-attribute"></a>mc:Ignorable 特性
指定在[!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]标记文件中遇到的哪些命名空间前缀可能会被[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]处理器忽略。 特性支持用于自定义命名空间映射[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]和版本控制的标记兼容性。 `mc:Ignorable`  
  
## <a name="xaml-attribute-usage-single-prefix"></a>XAML 特性用法 (单前缀)  
  
```  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## <a name="xaml-attribute-usage-two-prefixes"></a>XAML 特性用法 (两个前缀)  
  
```  
<object  
  xmlns:ignorablePrefix1="ignorableUri"  
  xmlns:ignorablePrefix2="ignorableUri2"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix1 ignorablePrefix2"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|*ignorablePrefix、ignorablePrefix1 等。*|根据 XML 1.0 规范的任何有效的前缀字符串。|  
|*ignorableUri*|根据 XML 1.0 规范指定命名空间的任何有效 URI。|  
|*ThisElementCanBeIgnored*|如果基础类型无法解析, 则[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]处理器实现可忽略的元素。|  
  
## <a name="remarks"></a>备注  
 命名空间前缀是映射[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]兼容命名空间`http://schemas.openxmlformats.org/markup-compatibility/2006`时建议使用的前缀约定。 `mc` [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]  
  
 元素名称的前缀部分标识为`mc:Ignorable`的元素或属性将不会在[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]处理器处理时引发错误。 如果该特性未能解析为基础类型或编程构造, 则将忽略该元素。 但请注意, 如果忽略元素, 则忽略的元素可能仍会生成其他元素要求的分析错误。 例如, 特定的元素内容模型可能只需要一个子元素, 但如果指定的子元素在`mc:Ignorable`前缀中, 并且指定的子元素未能解析为类型, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]则处理器可能引发错误。  
  
 `mc:Ignorable`仅适用于命名空间到标识符字符串的映射。 `mc:Ignorable`不适用于将命名空间映射到程序集, 这些程序集指定 CLR 命名空间和程序集 (或作为程序集的当前可执行文件的默认值)。  
  
 如果要实现[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]处理器, 处理器实现对于由标识为`mc:Ignorable`的前缀限定的任何元素或属性, 都不得引发分析或处理错误。 但您的处理器实现仍可能引发异常, 这些异常是无法加载或处理元素的辅助结果, 如前面给出的一个子元素示例。  
  
 默认情况下, [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]处理器将忽略忽略元素内的内容。 但是, 您可以指定一个附加属性[mc: ProcessContent 特性](mc-processcontent-attribute.md), 以要求在下一个可用的父元素中继续处理被忽略元素内的内容。  
  
 可以使用一个或多个空白字符作为分隔符, 在属性中指定多个前缀, 例如: `mc:Ignorable="ignore1 ignore2"`。  

 `http://schemas.openxmlformats.org/markup-compatibility/2006`命名空间定义 SDK 的此区域中未记录的其他元素和特性。 有关详细信息, 请参阅[XML 标记兼容性规范](/office/open-xml/introduction-to-markup-compatibility#markup-compatibility-in-the-open-xml-file-formats-specification)。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Markup.XamlReader>
- [PresentationOptions:Freeze 特性](presentationoptions-freeze-attribute.md)
- [XAML 概述 (WPF)](xaml-overview-wpf.md)
- [WPF 中的文档](documents-in-wpf.md)
