---
title: 联接运算 (C#)
ms.date: 07/20/2015
ms.assetid: 5105e0da-1267-4c00-837a-f0e9602279b8
ms.openlocfilehash: 95661e2d0d7f4f0e75c1fa1b10e1f322923189b1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69592077"
---
# <a name="join-operations-c"></a>联接运算 (C#)
联接  两个数据源就是将一个数据源中的对象与另一个数据源中具有相同公共属性的对象相关联。  
  
 当查询所面向的数据源相互之间具有无法直接领会的关系时，联接就成为一项重要的运算。 在面向对象的编程中，这可能意味着在未建模对象之间进行关联，例如对单向关系进行反向推理。 下面是单向关系的一个示例：Customer 类有一个类型为 City 的属性，但 City 类没有作为 Customer 对象集合的属性。 如果你具有一个 City 对象列表，并且要查找每个城市中的所有客户，则可以使用联接运算完成此项查找。  
  
 LINQ 框架中提供的 join 方法包括 <xref:System.Linq.Enumerable.Join%2A> 和 <xref:System.Linq.Enumerable.GroupJoin%2A>。 这些方法执行同等联接，即根据 2 个数据源的键是否相等来匹配这 2 个数据源的联接。 （与此相较，Transact-SQL 支持除“等于”之外的联接运算符，例如“小于”运算符。）用关系数据库术语表达，就是说 <xref:System.Linq.Enumerable.Join%2A> 实现了内部联接，这种联接只返回那些在另一个数据集中具有匹配项的对象。 <xref:System.Linq.Enumerable.GroupJoin%2A> 方法在关系数据库术语中没有直接等效项，但实现了内部联接和左外部联接的超集。 左外部联接是指返回第一个（左侧）数据源的每个元素的联接，即使其他数据源中没有关联元素。  
  
 下图显示了一个概念性视图，其中包含两个集合以及这两个集合中的包含在内部联接或左外部联接中的元素。  
  
 ![显示内部/外部的两个重叠圆圈。](./media/join-operations/join-method-overlapping-circles.png)  
  
## <a name="methods"></a>方法  
  
|方法名|说明|C# 查询表达式语法|详细信息|  
|-----------------|-----------------|---------------------------------|----------------------|  
|联接|根据键选择器函数联接两个序列并提取值对。|`join … in … on … equals …`|<xref:System.Linq.Enumerable.Join%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Join%2A?displayProperty=nameWithType>|  
|GroupJoin|根据键选择器函数联接两个序列，并对每个元素的结果匹配项进行分组。|`join … in … on … equals … into …`|<xref:System.Linq.Enumerable.GroupJoin%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupJoin%2A?displayProperty=nameWithType>|  
  
## <a name="see-also"></a>请参阅

- <xref:System.Linq>
- [标准查询运算符概述 (C#)](./standard-query-operators-overview.md)
- [匿名类型](../../classes-and-structs/anonymous-types.md)
- [构建联接和叉积查询](../../../../framework/data/adonet/sql/linq/formulate-joins-and-cross-product-queries.md)
- [join 子句](../../../language-reference/keywords/join-clause.md)
- [如何：使用组合键进行联接](../../linq-query-expressions/how-to-join-by-using-composite-keys.md)
- [如何：联接不同文件的内容 (LINQ) (C#)](./how-to-join-content-from-dissimilar-files-linq.md)
- [如何：对 join 子句的结果进行排序](../../linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)
- [如何：执行自定义联接操作](../../linq-query-expressions/how-to-perform-custom-join-operations.md)
- [如何：执行分组联接](../../linq-query-expressions/how-to-perform-grouped-joins.md)
- [如何：执行内部联接](../../linq-query-expressions/how-to-perform-inner-joins.md)
- [如何：执行左外部联接](../../linq-query-expressions/how-to-perform-left-outer-joins.md)
- [如何：从多个源填充对象集合 (LINQ) (C#)](./how-to-populate-object-collections-from-multiple-sources-linq.md)
