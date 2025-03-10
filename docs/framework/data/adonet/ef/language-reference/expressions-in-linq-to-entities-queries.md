---
title: LINQ to Entities 查询中的表达式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d70b502f-6a15-4120-b4fe-500b173ad9cc
ms.openlocfilehash: 383339241194c56d0c3178f538f2ac08b2f1b437
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950391"
---
# <a name="expressions-in-linq-to-entities-queries"></a>LINQ to Entities 查询中的表达式
表达式是求值结果可以为单个值、对象、方法或命名空间的一段代码。 表达式可以包含文本值、方法调用、运算符及其操作数，或者简单名称。 简单名称可以是变量名、类型成员名、方法参数名、命名空间名或类型名。 表达式可以使用运算符（运算符又可使用其他表达式作为参数）或方法调用（方法调用的参数又可以是其他方法调用）。 因此，表达式可以非常简单，也可以极其复杂。  
  
 在 LINQ to Entities 查询中, 表达式可以包含<xref:System.Linq.Expressions>命名空间中的类型所允许的任何内容, 包括 lambda 表达式。 可在 LINQ to Entities 查询中使用的表达式是可用于查询的[!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)]表达式的超集。  对 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 的查询中使用的表达式仅限于 `ObjectQuery<T>` 和基础数据源所支持的运算。  
  
 在下面的示例中，`Where` 子句中的比较运算就是一个表达式：  
  
 [!code-csharp[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#whereexpression)]
 [!code-vb[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#whereexpression)]  
  
> [!NOTE]
> 特定语言构造 (如C# `unchecked`) 在 LINQ to Entities 中没有意义。  
  
## <a name="in-this-section"></a>本节内容  
 [常量表达式](../../../../../../docs/framework/data/adonet/ef/language-reference/constant-expressions.md)  
  
 [比较表达式](../../../../../../docs/framework/data/adonet/ef/language-reference/comparison-expressions.md)  
  
 [NULL 比较](../../../../../../docs/framework/data/adonet/ef/language-reference/null-comparisons.md)  
  
 [初始化表达式](../../../../../../docs/framework/data/adonet/ef/language-reference/initialization-expressions.md)  
  
 [关系、导航属性和外键](/ef/ef6/fundamentals/relationships)  
  
## <a name="see-also"></a>请参阅

- [ADO.NET 实体框架](../../../../../../docs/framework/data/adonet/ef/index.md)
