---
title: 创建数据集
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 57629d8f-393e-4677-8b83-29ffde27f5fc
ms.openlocfilehash: 19badb009ebe95c52ab1dbbaef96f280c769553b
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205152"
---
# <a name="creating-a-dataset"></a>创建数据集
可以通过调用 <xref:System.Data.DataSet> 构造函数来创建 <xref:System.Data.DataSet> 的实例。 可以选择指定一个名称自变量。 如果没有为 <xref:System.Data.DataSet> 指定名称，则该名称会设置为“NewDataSet”。  
  
 也可以基于现有的 <xref:System.Data.DataSet> 来创建新的 <xref:System.Data.DataSet>。 新的 <xref:System.Data.DataSet> 可以是：现有 <xref:System.Data.DataSet> 的原样副本；<xref:System.Data.DataSet> 的复本，它复制关系结构（即架构）但不包含现有 <xref:System.Data.DataSet> 中的任何数据；或 <xref:System.Data.DataSet> 的子集，它仅包含现有 <xref:System.Data.DataSet> 中已使用 <xref:System.Data.DataSet.GetChanges%2A> 方法修改的行。 有关详细信息, 请参阅[复制数据集内容](copying-dataset-contents.md)。  
  
 以下代码示例演示了如何构造 <xref:System.Data.DataSet> 的实例。  
  
```vb  
Dim customerOrders As DataSet = New DataSet("CustomerOrders")  
```  
  
```csharp  
DataSet customerOrders = new DataSet("CustomerOrders");  
```  
  
## <a name="see-also"></a>请参阅

- [从 DataAdapter 填充数据集](../populating-a-dataset-from-a-dataadapter.md)
- [数据集、数据表和数据视图](index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
