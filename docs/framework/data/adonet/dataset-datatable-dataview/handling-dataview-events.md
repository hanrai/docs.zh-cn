---
title: 处理数据视图事件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5675663-fc91-4e0d-87a9-481b25b64c0f
ms.openlocfilehash: b3a1077bff9bf457b4aef0b05357d4a9260f8973
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70204826"
---
# <a name="handling-dataview-events"></a>处理数据视图事件
可以使用 <xref:System.Data.DataView.ListChanged> 的 <xref:System.Data.DataView> 事件确定某个视图是否已更新。 引发该事件的更新包括添加、删除或修改基础表中的某行；在基础表的架构中添加或删除某列；更改父或子关系。 如果要查看的行的列表由于应用了新的排序顺序或筛选器而发生了重大更改, 则**ListChanged**事件也会通知您。  
  
 **ListChanged**事件<xref:System.ComponentModel>实现 命名空间的ListChangedEventHandler委托,并将对象作为<xref:System.ComponentModel.ListChangedEventArgs>输入。 您可以使用<xref:System.ComponentModel.ListChangedType> **ListChangedEventArgs**对象的**system.componentmodel.listchangedtype>** 属性中的枚举值确定发生的更改类型。 对于涉及添加、删除或移动行的更改, 可以使用**ListChangedEventArgs**对象的**NewIndex**属性来访问已添加或已移动的行和已删除行的上一索引的新索引。 在移动行的情况下, 可以使用**ListChangedEventArgs**对象的**OldIndex**属性访问已移动行的上一个索引。  
  
 **DataViewManager**还公开了一个**ListChanged**事件, 以在表已添加或已删除或者是否对基础**数据集**的**关系**集合进行更改时通知您。  
  
 下面的代码示例演示如何添加**ListChanged**事件处理程序。  
  
```vb  
AddHandler custView.ListChanged, _  
  New System.ComponentModel.ListChangedEventHandler( _  
  AddressOf OnListChanged)  
  
Private Shared Sub OnListChanged( _  
  sender As Object, args As System.ComponentModel.ListChangedEventArgs)  
  Console.WriteLine("ListChanged:")  
  Console.WriteLine(vbTab & "    Type = " & _  
    System.Enum.GetName(args.ListChangedType.GetType(), _  
    args.ListChangedType))  
  Console.WriteLine(vbTab & "OldIndex = " & args.OldIndex)  
  Console.WriteLine(vbTab & "NewIndex = " & args.NewIndex)  
End Sub  
```  
  
```csharp  
custView.ListChanged  += new   
  System.ComponentModel.ListChangedEventHandler(OnListChanged);  
  
protected static void OnListChanged(object sender,   
  System.ComponentModel.ListChangedEventArgs args)  
{  
  Console.WriteLine("ListChanged:");  
  Console.WriteLine("\t    Type = " + args.ListChangedType);  
  Console.WriteLine("\tOldIndex = " + args.OldIndex);  
  Console.WriteLine("\tNewIndex = " + args.NewIndex);  
}  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Data.DataView>
- <xref:System.ComponentModel.ListChangedEventHandler>
- [数据视图](dataviews.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
