---
title: 如何：投影匿名类型 (C#)
ms.date: 07/20/2015
ms.assetid: 5cb9be13-5ac4-4373-a034-b3520a5b2dec
ms.openlocfilehash: cd05c0ad7ab5a683b95e110cb0b1bb75b8a1dd2a
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593029"
---
# <a name="how-to-project-an-anonymous-type-c"></a>如何：投影匿名类型 (C#)
在某些情况下，您可能需要将查询投影到新类型，即使您知道只是短时间使用此类型。 创建仅在投影中使用的新类型需要大量额外工作。 在这种情况下，一种更有效的方法是投影到匿名类型。 匿名类型允许您定义一个类，然后在不给出类名称的情况下声明并初始化该类的对象。  
  
 匿名类型是“元组”这一数学概念的 C# 实现。  数学术语元组源自序列单元组、双元组、三元组、四元组、五元组和 n 元组。 它指有限的对象序列，每个对象具有特定的类型。 有时，它称为名称/值对的列表。 例如，[示例XML文件：典型采购订单 (LINQ to XML)](./sample-xml-file-typical-purchase-order-linq-to-xml-1.md) XML 文档中的地址内容可表示如下：  
  
```  
Name: Ellen Adams  
Street: 123 Maple Street  
City: Mill Valley  
State: CA  
Zip: 90952  
Country: USA  
```  
  
 在创建匿名类型的实例时，可以将其想像为创建 n 阶元组。 如果编写一个将在 `select` 子句中创建元组的查询，该查询将返回该元组的一个 `IEnumerable`。  
  
## <a name="example"></a>示例  
 在此示例中，`select` 子句投影一个匿名类型。 然后，示例使用 `var` 创建 `IEnumerable` 对象。 在 `foreach` 循环中，该迭代变量成为在查询表达式中创建的匿名类型的实例。  
  
 此示例使用下面的 XML 文档：[示例 XML 文件：客户和订单 (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md)。  
  
```csharp  
XElement custOrd = XElement.Load("CustomersOrders.xml");  
var custList =  
    from el in custOrd.Element("Customers").Elements("Customer")  
    select new {  
        CustomerID = (string)el.Attribute("CustomerID"),  
        CompanyName = (string)el.Element("CompanyName"),  
        ContactName = (string)el.Element("ContactName")  
    };  
foreach (var cust in custList)  
    Console.WriteLine("{0}:{1}:{2}", cust.CustomerID, cust.CompanyName, cust.ContactName);  
```  
  
 此代码生成以下输出：  
  
```  
GREAL:Great Lakes Food Market:Howard Snyder  
HUNGC:Hungry Coyote Import Store:Yoshi Latimer  
LAZYK:Lazy K Kountry Store:John Steel  
LETSS:Let's Stop N Shop:Jaime Yorres  
```  
  