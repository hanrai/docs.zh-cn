---
title: 如何：基于位置查找子元素 (XPath-LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: e35bb269-ec86-4c96-8321-12491a0eb2c3
ms.openlocfilehash: b55e2df5a97446da9d02fd3979f5d8d584228ba2
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593499"
---
# <a name="how-to-find-child-elements-based-on-position-xpath-linq-to-xml-c"></a>如何：基于位置查找子元素 (XPath-LINQ to XML) (C#)
有时需要根据元素的位置查找元素。 您可能想查找第二个元素，或者查找第三到第五个元素。  
  
 XPath 表达式为：  
  
 `Test[position() >= 2 and position() <= 4]`  
  
 有两种方法以迟缓方式编写此 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 查询。 可以使用 <xref:System.Linq.Enumerable.Skip%2A> 和 <xref:System.Linq.Enumerable.Take%2A> 运算符，也可以使用接受索引的 <xref:System.Linq.Enumerable.Where%2A> 重载。 使用 <xref:System.Linq.Enumerable.Where%2A> 重载时，要使用 lambda 表达式来获得两个参数。 下面的示例演示了根据位置选择的这两种方法。  
  
## <a name="example"></a>示例  
 本示例查找第二到第四个 `Test` 元素。 结果是一个元素集合。  
  
 此示例使用下面的 XML 文档：[示例 XML 文件：测试配置 (LINQ to XML)](./sample-xml-file-test-configuration-linq-to-xml.md)。  
  
```csharp  
XElement testCfg = XElement.Load("TestConfig.xml");  
  
// LINQ to XML query  
IEnumerable<XElement> list1 =  
    testCfg  
    .Elements("Test")  
    .Skip(1)  
    .Take(3);  
  
// LINQ to XML query  
IEnumerable<XElement> list2 =  
    testCfg  
    .Elements("Test")  
    .Where((el, idx) => idx >= 1 && idx <= 3);  
  
// XPath expression  
IEnumerable<XElement> list3 =  
  testCfg.XPathSelectElements("Test[position() >= 2 and position() <= 4]");  
  
if (list1.Count() == list2.Count() &&  
    list1.Count() == list3.Count() &&  
    list1.Intersect(list2).Count() == list1.Count() &&  
    list1.Intersect(list3).Count() == list1.Count())  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 该示例产生下面的输出：  
  
```  
Results are identical  
<Test TestId="0002" TestType="CMD">  
  <Name>Find succeeding characters</Name>  
  <CommandLine>Examp2.EXE</CommandLine>  
  <Input>abc</Input>  
  <Output>def</Output>  
</Test>  
<Test TestId="0003" TestType="GUI">  
  <Name>Convert multiple numbers to strings</Name>  
  <CommandLine>Examp2.EXE /Verbose</CommandLine>  
  <Input>123</Input>  
  <Output>One Two Three</Output>  
</Test>  
<Test TestId="0004" TestType="GUI">  
  <Name>Find correlated key</Name>  
  <CommandLine>Examp3.EXE</CommandLine>  
  <Input>a1</Input>  
  <Output>b1</Output>  
</Test>  
```  
