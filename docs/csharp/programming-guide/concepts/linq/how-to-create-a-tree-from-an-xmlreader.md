---
title: 如何：从 XmlReader 创建树 (C#)
ms.date: 07/20/2015
ms.assetid: 60951c9c-7087-406c-b5bb-c60e58609b21
ms.openlocfilehash: f632bbdad7d52ea37e2587516792dfd13178d702
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593872"
---
# <a name="how-to-create-a-tree-from-an-xmlreader-c"></a>如何：从 XmlReader 创建树 (C#)
本主题演示如何直接从 <xref:System.Xml.XmlReader> 创建 XML 树。 若要从 <xref:System.Xml.Linq.XElement> 创建 <xref:System.Xml.XmlReader>，必须将 <xref:System.Xml.XmlReader> 定位在元素节点上。 <xref:System.Xml.XmlReader> 将跳过注释和处理指令，但如果 <xref:System.Xml.XmlReader> 定位在文本节点上，则将引发错误。 若要避免这类错误，请在从 <xref:System.Xml.XmlReader> 创建 XML 树之前，始终将 <xref:System.Xml.XmlReader> 定位在元素上。  
  
## <a name="example"></a>示例  
 此示例使用下面的 XML 文档：[示例 XML 文件：图书 (LINQ to XML)](./sample-xml-file-books-linq-to-xml.md)。  
  
 下面的代码创建一个 `T:System.Xml.XmlReader` 对象，然后读取节点，直到找到第一个元素节点。 然后加载 <xref:System.Xml.Linq.XElement> 对象。  
  
```csharp  
XmlReader r = XmlReader.Create("books.xml");  
while (r.NodeType != XmlNodeType.Element)  
    r.Read();  
XElement e = XElement.Load(r);  
Console.WriteLine(e);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Catalog>  
   <Book id="bk101">  
      <Author>Garghentini, Davide</Author>  
      <Title>XML Developer's Guide</Title>  
      <Genre>Computer</Genre>  
      <Price>44.95</Price>  
      <PublishDate>2000-10-01</PublishDate>  
      <Description>An in-depth look at creating applications   
      with XML.</Description>  
   </Book>  
   <Book id="bk102">  
      <Author>Garcia, Debra</Author>  
      <Title>Midnight Rain</Title>  
      <Genre>Fantasy</Genre>  
      <Price>5.95</Price>  
      <PublishDate>2000-12-16</PublishDate>  
      <Description>A former architect battles corporate zombies,   
      an evil sorceress, and her own childhood to become queen   
      of the world.</Description>  
   </Book>  
</Catalog>  
```  
  
## <a name="see-also"></a>请参阅

- [分析 XML (C#)](./parsing-xml.md)
