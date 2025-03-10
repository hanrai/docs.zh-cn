---
title: 创建数据表
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: eecf9d78-60e3-4fdc-8de0-e56c13a89414
ms.openlocfilehash: 64ba7a8e6bd6361e14d1f16576e377575b088bbe
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205150"
---
# <a name="creating-a-datatable"></a>创建数据表
<xref:System.Data.DataTable> 表示一个内存内关系数据的表，可以独立创建和使用，也可以由其他 .NET Framework 对象使用，最常见的情况是作为 <xref:System.Data.DataSet> 的成员使用。  
  
 您可以使用相应的**datatable**构造函数创建**datatable**对象。 您可以通过使用**add**方法将其添加到**DataTable**对象的**Tables**集合中, 将其添加到**数据集**。  
  
 您还可以通过使用**DataAdapter**对象的**Fill**或**FillSchema**方法, 或使用**ReadXml**的预定义或推断 XML 架构在**数据集中**创建**DataTable**对象**ReadXmlSchema** **数据集**的**InferXmlSchema**方法。 请注意, 将**DataTable**添加为一个**数据集**的**tables**集合的成员后, 不能将其添加到任何其他**数据集**的表的集合中。  
  
 首次创建**DataTable**时, 它没有架构 (即结构)。 若要定义表的架构, 必须创建对象并将其<xref:System.Data.DataColumn>添加到表的**Columns**集合中。 您还可以为表定义主键列, 并创建**约束**对象并将其添加到表的**约束**集合。 为**DataTable**定义了架构之后, 可以通过将**DataRow**对象添加到表的**rows**集合中来向表中添加数据行。  
  
 创建<xref:System.Data.DataTable.TableName%2A> **DataTable**时, 不需要提供属性的值; 您可以在其他时间指定该属性, 也可以将其留空。 但是, 当您将没有**TableName**值的表添加到**数据集**时, 将为该表给定增量默认名称表*N*, 并以 "table" 作为 Table0。  
  
> [!NOTE]
> 当你提供**TableName**值时, 我们建议你避免使用 "Table*N*" 命名约定, 因为所提供的名称可能与**数据集中**的现有默认表名称冲突。 如果提供的名称已经存在，将引发异常。  
  
 下面的示例创建**DataTable**对象的一个实例, 并为其分配名称 "Customers"。  
  
```vb  
Dim workTable as DataTable = New DataTable("Customers")  
```  
  
```csharp  
DataTable workTable = new DataTable("Customers");  
```  
  
 下面的示例通过将 DataTable 添加到**DataSet**的**Tables**集合来创建**DataTable**的实例。  
  
```vb  
Dim customers As DataSet = New DataSet  
Dim customersTable As DataTable = _  
   customers.Tables.Add("CustomersTable")  
```  
  
```csharp  
DataSet customers = new DataSet();  
DataTable customersTable = customers.Tables.Add("CustomersTable");  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Data.DataTable>
- <xref:System.Data.DataTableCollection>
- [数据表](datatables.md)
- [从 DataAdapter 填充数据集](../populating-a-dataset-from-a-dataadapter.md)
- [从 XML 加载数据集](loading-a-dataset-from-xml.md)
- [从 XML 加载数据集构架信息](loading-dataset-schema-information-from-xml.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
