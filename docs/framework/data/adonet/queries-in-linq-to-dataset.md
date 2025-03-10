---
title: 在 LINQ to DataSet 中查询
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c1a78fa8-9f0c-40bc-a372-5575a48708fe
ms.openlocfilehash: f6677e894e09b41e1f406d6b6485abf4168b5d6e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69946260"
---
# <a name="queries-in-linq-to-dataset"></a>在 LINQ to DataSet 中查询
查询是一种从数据源检索数据的表达式。 查询通常用专用查询语言表示，如用于关系数据库的 SQL 和用于 XML 的 XQuery。 因此，开发人员对于他们查询的每种类型的数据源或数据格式，都不得不学习一种新的查询语言。 [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 提供了一种较为简单的一致模型，适用于各种数据源和格式的数据。 在 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 查询中，您始终使用编程对象。  
  
 一个 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 查询操作包含三个操作：获取数据源、创建查询和执行查询。  
  
 实现 <xref:System.Collections.Generic.IEnumerable%601> 泛型接口的数据源可以通过 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 进行查询。 对<xref:System.Data.DataTableExtensions.AsEnumerable%2A>调用将<xref:System.Data.DataTable>返回一个对象, 该对象实现<xref:System.Collections.Generic.IEnumerable%601>泛型接口, 该接口用作 LINQ to DataSet 查询的数据源。  
  
 在查询中，您可以确切指定要从数据源检索哪些信息。 查询也可以指定返回信息之前信息的排序、分组和表现方式。 在 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 中，查询存储在变量中。 如果查询旨在返回一系列值，则查询变量本身也必须为可枚举类型。 此查询变量不执行任何操作，也不返回任何数据；它只存储查询信息。 创建查询后必须执行该查询以检索任何数据。  
  
 在返回一系列值的查询中，查询变量本身从不保存查询结果，它只存储查询命令。 查询的执行将推迟到在 `foreach` 或 `For Each` 循环中循环访问查询变量之后进行。 这称为 "*延迟执行*";也就是说, 在构造查询后, 将执行查询。 这意味着您可以根据需要频繁地执行查询。 例如，当您的数据库由其他应用程序不断更新时，此功能将会很有用。 在您的应用程序中，您可以创建查询以检索最新信息并重复执行查询，每次返回更新的信息。  
  
 与返回一系列值的延迟查询相反，返回单一实例值的查询将立即执行。 <xref:System.Linq.Enumerable.Count%2A>、<xref:System.Linq.Enumerable.Max%2A>、<xref:System.Linq.Enumerable.Average%2A> 和 <xref:System.Linq.Enumerable.First%2A> 是单一实例查询的一些示例。 因为需要查询结果来计算单一实例结果，因此这些查询将会立即执行。 例如，若要计算查询结果的平均值，则必须执行查询，以便求平均值函数具有要使用的输入数据。 您也可以对查询使用 <xref:System.Linq.Enumerable.ToList%2A> 或 <xref:System.Linq.Enumerable.ToArray%2A> 方法以强制立即执行不生成单一实例值的查询。 当想要缓存查询结果时，这些强制立即执行的技术可能会很有用。
  
## <a name="queries"></a>查询  
 可以采用两种不同的语法来表述 LINQ to DataSet 查询: 查询表达式语法和基于方法的查询语法。  
  
### <a name="query-expression-syntax"></a>查询表达式语法  
 查询表达式是一种声明性查询语法。 此语法使开发人员能够以类似于 SQL 的格式用 C# 或 Visual Basic 编写查询。 通过使用查询表达式语法，你可以用最少的代码对数据源执行复杂的筛选、排序和分组操作。 有关详细信息, 请参阅[LINQ 查询表达式](../../../csharp/linq/index.md#query-expression-overview)和[基本查询操作 (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md)。
  
 .NET Framework 公共语言运行时 (CLR) 无法读取查询表达式语法本身。 因此，在编译时，查询表达式将转换为 CLR 能理解的形式，即方法调用。 这些方法称为“标准查询运算符”。 作为开发人员，您可以选择使用方法语法而不使用查询语法直接调用这些方法。 有关详细信息，请参阅 [LINQ 中的查询语法和方法语法](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)。 有关标准查询运算符的详细信息, 请参阅[标准查询运算符概述](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
 下面的示例使用 <xref:System.Linq.Enumerable.Select%2A> 返回 `Product` 表中的所有行并显示产品名称。  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectSimple1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectsimple1)]
 [!code-vb[DP LINQ to DataSet Examples#SelectSimple1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectsimple1)]  
  
### <a name="method-based-query-syntax"></a>基于方法的查询语法  
 表述 LINQ to DataSet 查询的另一种方法是使用基于方法的查询。 基于方法的查询语法是对 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 运算符方法的一系列直接方法调用，将 Lambda 表达式作为参数进行传递。 有关详细信息，请参阅 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)。  
  
 此示例使用 <xref:System.Linq.Enumerable.Select%2A> 返回 `Product` 中的所有行并显示产品名称。  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectAnonymousTypes_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectanonymoustypes_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SelectAnonymousTypes_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectanonymoustypes_mq)]  
  
## <a name="composing-queries"></a>编写查询  
 如本主题前面所述，当查询旨在返回一系列值时，查询变量本身只存储查询命令。 如果查询不包含可使查询立即执行的方法，则查询的实际执行将会推迟，直到在 `foreach` 或 `For Each` 循环中循环访问查询变量。 延迟执行可使多个查询组合在一起或使查询得到扩展。 扩展查询时，将修改查询以包括新操作，最终执行将反映这些更改。 在下面的示例中，第一个查询返回所有产品。 第二个查询通过使用 `Where` 扩展第一个查询，以返回大小为“L”的所有产品：  
  
 [!code-csharp[DP LINQ to DataSet Examples#Composing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#composing)]
 [!code-vb[DP LINQ to DataSet Examples#Composing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#composing)]  
  
 执行一个查询后，不会再编写其他查询，并且所有后续查询都将使用驻留在内存中的 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 运算符。 当在 `foreach` 或 `For Each` 语句中循环访问查询变量或通过调用可导致立即执行的 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 转换运算符之一时，查询将会开始执行。 这些运算符包括：<xref:System.Linq.Enumerable.ToList%2A>、<xref:System.Linq.Enumerable.ToArray%2A>、<xref:System.Linq.Enumerable.ToLookup%2A> 和 <xref:System.Linq.Enumerable.ToDictionary%2A>。  
  
 在下面的示例中，第一个查询返回按定价排序的所有产品。 <xref:System.Linq.Enumerable.ToArray%2A> 方法用于强制立即执行查询：  
  
 [!code-csharp[DP LINQ to DataSet Examples#ToArray2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#toarray2)]
 [!code-vb[DP LINQ to DataSet Examples#ToArray2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#toarray2)]  
  
## <a name="see-also"></a>请参阅

- [编程指南](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)
- [查询数据集](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)
- [C# 中的 LINQ 入门](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)
- [Visual Basic 中的 LINQ 入门](../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)
