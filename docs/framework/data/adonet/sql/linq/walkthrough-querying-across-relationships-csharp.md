---
title: 演练：跨关系查询 (C#)
ms.date: 03/30/2017
ms.assetid: 552abeb1-18f2-4e93-a9c6-ef7b2db30c32
ms.openlocfilehash: a9e0583b14c07df2b1de23ba37fa88552a4c5c7c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69946947"
---
# <a name="walkthrough-querying-across-relationships-c"></a>演练：跨关系查询 (C#)
本演练演示如何使用[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] *关联*来表示数据库中的外键关系。  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 本演练是使用 Visual C# 开发设置编写的。  
  
## <a name="prerequisites"></a>系统必备  
 您必须完成[以下演练:简单对象模型和查询 (C#)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-simple-object-model-and-query-csharp.md)。 本演练建立在该演练基础之上，包括在 c:\linqtest5 中须存在 northwnd.mdf 文件。  
  
## <a name="overview"></a>概述  
 本演练由三项主要任务组成：  
  
- 添加一个实体类以表示 Northwind 示例数据库中的 Orders 表。  
  
- 向 `Customer` 类补充一些批注，以增强 `Customer` 和 `Order` 类之间的关系。  
  
- 创建并运行查询以测试能否通过使用 `Order` 类获取 `Customer` 信息。  
  
## <a name="mapping-relationships-across-tables"></a>跨表映射关系  
 在 `Customer` 类定义的后面，创建包含如下代码的 `Order` 实体类定义，这些代码表示 `Order.Customer` 作为外键与 `Customer.CustomerID` 相关。  
  
### <a name="to-add-the-order-entity-class"></a>添加 Order 实体类  
  
- 在 `Customer` 类后面键入或粘贴如下代码：  
  
     [!code-csharp[DLinqWalk2CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#1)]  
  
## <a name="annotating-the-customer-class"></a>对 Customer 类进行批注  
 在此步骤中，您要对 `Customer` 类进行批注，以指示它与 `Order` 类的关系。 （这种添加批注的操作并非绝对必需的，因为定义任一方向上的关系都足以满足创建链接的需要。 但添加此批注确实便于您在任一方向上定位对象。）  
  
### <a name="to-annotate-the-customer-class"></a>对 Customer 类进行批注  
  
- 将下面的代码键入或粘贴到 `Customer` 类中：  
  
     [!code-csharp[DLinqWalk2CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#2)]  
  
## <a name="creating-and-running-a-query-across-the-customer-order-relationship"></a>跨 Customer-Order 关系创建并运行查询  
 现在您可以直接从 `Order` 对象访问 `Customer` 对象，或反过来进行访问。 客户和订单之间不需要显式*联接*。  
  
### <a name="to-access-order-objects-by-using-customer-objects"></a>使用 Customer 对象访问 Order 对象  
  
1. 通过将下面的代码键入或粘贴到 `Main` 方法中修改此方法：  
  
     [!code-csharp[DLinqWalk2CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#3)]  
  
2. 按 F5 调试应用程序。  
  
    > [!NOTE]
    > 你可以通过注释掉 `db.Log = Console.Out;` 来消除控制台窗口中的 SQL 代码。  
  
3. 在控制台窗口中按 Enter，以停止调试。  
  
## <a name="creating-a-strongly-typed-view-of-your-database"></a>创建数据库的强类型化视图  
 从数据库的强类型化视图着手要容易得多。 通过将 <xref:System.Data.Linq.DataContext> 对象强类型化，您无需调用 <xref:System.Data.Linq.DataContext.GetTable%2A>。 当您使用强类型化的 <xref:System.Data.Linq.DataContext> 对象时，您可以在所有查询中使用强类型化表。  
  
 在以下步骤中，您将创建 `Customers` 作为映射到数据库中的 Customers 表的强类型化表。  
  
### <a name="to-strongly-type-the-datacontext-object"></a>对 DataContext 对象进行强类型化  
  
1. 将下面的代码添加到 `Customer` 类声明的上方。  
  
     [!code-csharp[DLinqWalk2CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#4)]  
  
2. 将 `Main` 方法修改为使用强类型化的 <xref:System.Data.Linq.DataContext>，如下所示：  
  
     [!code-csharp[DLinqWalk2CS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk2CS/cs/Program.cs#5)]  
  
3. 按 F5 调试应用程序。  
  
     控制台窗口输出如下：  
  
     `ID=WHITC`  
  
4. 在控制台窗口中按 Enter，以停止调试。  
  
## <a name="next-steps"></a>后续步骤  
 下一个演练 ([演练:操作 data (C#)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-manipulating-data-csharp.md)) 演示如何处理数据。 该演练不要求您保存本系列中已经完成的两个演练的结果。  
  
## <a name="see-also"></a>请参阅

- [通过演练学习](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)
