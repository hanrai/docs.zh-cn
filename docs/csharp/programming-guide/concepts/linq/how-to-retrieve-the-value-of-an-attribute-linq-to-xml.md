---
title: 如何：检索特性的值 (LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: 817bbe89-5979-4234-bf0c-46f63692ac8c
ms.openlocfilehash: 54ea4b532669ed2c615fcde02011fdd1228705a3
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69592466"
---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml-c"></a>如何：检索特性的值 (LINQ to XML) (C#)
本主题说明如何获取属性的值。 主要有两种方法：可以将 <xref:System.Xml.Linq.XAttribute> 强制转换为所需的类型；然后，显式转换运算符将元素或属性的内容转换为指定的类型。 此外，还可以使用 <xref:System.Xml.Linq.XAttribute.Value%2A> 属性。 但是，强制转换通常是更好的方法。 在检索可能存在也可能不存在的属性的值时，如果将属性强制转换为可以为 null 的类型，则代码会更易于编写。 有关此技术的示例，请参见[如何：检索元素的值 (LINQ to XML) (C#)](./how-to-retrieve-the-value-of-an-element-linq-to-xml.md)。  
  
## <a name="example"></a>示例  
 若要检索属性的值，只需将 <xref:System.Xml.Linq.XAttribute> 对象强制转换为所需的类型即可。  
  
```csharp  
XElement root = new XElement("Root",  
                    new XAttribute("Attr", "abcde")  
                );  
Console.WriteLine(root);  
string str = (string)root.Attribute("Attr");  
Console.WriteLine(str);  
```  
  
 该示例产生下面的输出：  
  
```  
<Root Attr="abcde" />  
abcde  
```  
  
## <a name="example"></a>示例  
 下面的示例演示在属性处于命名空间中时，如何检索属性的值。 有关详细信息，请参阅[命名空间概述(LINQ to XML) (C#)](namespaces-overview-linq-to-xml.md)。  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
                    new XAttribute(aw + "Attr", "abcde")  
                );  
string str = (string)root.Attribute(aw + "Attr");  
Console.WriteLine(str);  
```  
  
 该示例产生下面的输出：  
  
```  
abcde  
```  
  
## <a name="see-also"></a>请参阅

- [LINQ to XML 轴 (C#)](./linq-to-xml-axes-overview.md)
