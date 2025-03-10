---
title: 写入数据集架构信息作为 XSD
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4e530831-695e-49ff-8f0b-e5b0c526b8eb
ms.openlocfilehash: f9664d8e7bc221da68492140f30419ea8fb0d316
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70204361"
---
# <a name="writing-dataset-schema-information-as-xsd"></a>写入数据集架构信息作为 XSD
您可以用 XML 架构定义语言 (XSD) 架构的形式来编写 <xref:System.Data.DataSet> 的架构，以便在 XML 文档中传输包含或不包含相关数据的架构。 XML 架构可以写入文件、流、 <xref:System.Xml.XmlWriter>或字符串; 它可用于生成强类型化**数据集**。 有关强类型化**数据集**对象的详细信息, 请参阅[类型化数据集](typed-datasets.md)。  
  
 您可以使用<xref:System.Data.DataColumn>对象的**ColumnMapping**属性来指定如何在 XML 架构中表示表的列。 有关详细信息, 请参阅以[Xml 数据形式编写数据集内容](writing-dataset-contents-as-xml-data.md)中的 "将列映射到 xml 元素、属性和文本"。  
  
 若要将**数据集**的架构作为 XML 架构写入文件、流或**XmlWriter**, 请使用**DataSet**的**WriteXmlSchema**方法。 **WriteXmlSchema**使用一个参数来指定生成的 XML 架构的目标。 下面的代码示例演示如何通过传递包含文件名和<xref:System.IO.StreamWriter>对象的字符串, 将**数据集**的 XML 架构写入文件。  
  
```vb  
dataSet.WriteXmlSchema("Customers.xsd")  
```  
  
```csharp  
dataSet.WriteXmlSchema("Customers.xsd");  
```  
  
```vb  
Dim writer As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xsd")  
dataSet.WriteXmlSchema(writer)  
writer.Close()  
```  
  
```csharp  
System.IO.StreamWriter writer = new System.IO.StreamWriter("Customers.xsd");  
dataSet.WriteXmlSchema(writer);  
writer.Close();  
```  
  
 若要获取**数据集**的架构并将其作为 XML 架构字符串写入, 请使用**GetXmlSchema**方法, 如以下示例中所示。  
  
```vb  
Dim schemaString As String = dataSet.GetXmlSchema()  
```  
  
```csharp  
string schemaString = dataSet.GetXmlSchema();  
```  
  
## <a name="see-also"></a>请参阅

- [在数据集中使用 XML](using-xml-in-a-dataset.md)
- [以 XML 数据的形式编写数据集内容](writing-dataset-contents-as-xml-data.md)
- [类型化数据集](typed-datasets.md)
- [数据集、数据表和数据视图](index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
