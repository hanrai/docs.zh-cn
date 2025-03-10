---
title: 基本查询操作 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- data sources [LINQ in Visual Basic]
- Join clause [LINQ in Visual Basic]
- ordering data [LINQ in Visual Basic]
- projections [LINQ in Visual Basic]
- LINQ [Visual Basic], query operations
- Order By clause [LINQ in Visual Basic]
- joining data [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], basic operations
- selecting data [LINQ in Visual Basic]
- Group By clause [LINQ in Visual Basic]
- grouping data [LINQ in Visual Basic]
- Select clause [LINQ in Visual Basic]
ms.assetid: 1146f6d0-fcb8-4f4d-8223-c9db52620d21
ms.openlocfilehash: 12f10f30dd767f3435044f2bbebe0eb865c29d0c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939366"
---
# <a name="basic-query-operations-visual-basic"></a>基本查询操作 (Visual Basic)
本主题简要介绍[!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]了 Visual Basic 中的表达式, 以及在查询中执行的一些典型操作。 有关详细信息，请参阅下列主题：  
  
 [Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)  
  
 [查询](../../../../visual-basic/language-reference/queries/index.md)  
  
 [演练：在 Visual Basic 中编写查询](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)  
  
## <a name="specifying-the-data-source-from"></a>指定数据源 (从)  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]在查询中, 第一步是指定要查询的数据源。 因此, 查询`From`中的子句始终是第一个。 查询运算符根据源的类型选择并生成结果。  
  
 [!code-vb[VbLINQBasicOps#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#1)]  
  
 子句指定`customers`数据源、 `cust`和*范围变量。* `From` 范围变量类似于循环迭代变量, 但在查询表达式中, 不会发生实际迭代。 当执行查询时, 通常使用`For Each`循环, 范围变量充当对中`customers`每个后续元素的引用。 由于编译器可以推断 `cust` 的类型，因此无需显式指定它。 有关用和编写的查询的示例, 但没有显式类型化, 请参阅[查询操作中的类型关系 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md)。  
  
 有关如何在 Visual Basic 中使用子句的`From`详细信息, 请参阅[from 子句](../../../../visual-basic/language-reference/queries/from-clause.md)。  
  
## <a name="filtering-data-where"></a>筛选数据 (位置)  
 可能最常见的查询操作是以布尔表达式的形式应用筛选器。 然后, 查询仅返回表达式为 true 的元素。 `Where`子句用于执行筛选。 筛选器指定数据源中要包括在结果序列中的元素。 在下面的示例中, 只包括具有伦敦地址的客户。  
  
 [!code-vb[VbLINQBasicOps#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#2)]  
  
 可以使用逻辑运算符 (如和`And` `Or` ) 在`Where`子句中合并筛选表达式。 例如, 若要仅返回来自伦敦并且其名称为 Devon 的客户, 请使用以下代码:  
  
```vb  
Where cust.City = "London" And cust.Name = "Devon"   
```  
  
 若要返回伦敦或巴黎的客户, 请使用以下代码:  
  
```vb  
Where cust.City = "London" Or cust.City = "Paris"   
```  
  
 有关如何在 Visual Basic 中使用子句的`Where`详细信息, 请参阅[Where 子句](../../../../visual-basic/language-reference/queries/where-clause.md)。  
  
## <a name="ordering-data-order-by"></a>数据排序 (排序方式)  
 将返回的数据按特定顺序排序通常是非常方便的。 `Order By`子句将导致返回的序列中的元素按指定的一个或多个字段进行排序。 例如, 下面的查询基于`Name`属性对结果进行排序。 由于`Name`是一个字符串, 因此返回的数据将按字母顺序从 a 到 Z 排序。  
  
 [!code-vb[VbLINQBasicOps#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#3)]  
  
 要对结果进行从 Z 到 A 的逆序排序，请使用 `Order By...Descending` 子句。 `Ascending`如果和均`Descending`未指定, 则默认值为。 `Ascending`  
  
 有关如何在 Visual Basic 中使用子句的`Order By`详细信息, 请参阅[Order By 子句](../../../../visual-basic/language-reference/queries/order-by-clause.md)。  
  
## <a name="selecting-data-select"></a>选择数据 (选择)  
 `Select`子句指定返回元素的形式和内容。 例如, 您可以指定您的结果是包含完整`Customer`的对象、只包含一个`Customer`属性、一个属性子集、不同数据源的属性组合还是基于计算的某些新的结果类型。 当 `Select` 子句生成除源元素副本以外的内容时，该操作称为投影。  
  
 若要检索由完整`Customer`的对象组成的集合, 请选择范围变量本身:  
  
 [!code-vb[VbLINQBasicOps#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#4)]  
  
 如果实例是具有多个字段的大型对象, 而您要检索的只是该名称, 则可以选择`cust.Name`, 如以下示例中所示。 `Customer` 局部类型推理可识别这会将结果类型从`Customer`对象的集合更改为字符串的集合。  
  
 [!code-vb[VbLINQBasicOps#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#5)]  
  
 若要从数据源中选择多个字段, 您有两种选择:  
  
- `Select`在子句中, 指定要包含在结果中的字段。 编译器将定义一个匿名类型, 该类型将这些字段作为其属性。 有关详细信息，请参阅[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
     由于以下示例中返回的元素是匿名类型的实例, 因此不能在代码中的其他位置以名称引用该类型。 该类型的编译器指定名称包含在正常 Visual Basic 代码中无效的字符。 在下面的示例中, 中`londonCusts4`查询返回的集合中的元素是匿名类型的实例  
  
     [!code-vb[VbLINQBasicOps#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#6)]  
  
     或  
  
- 定义包含要包含在结果中的特定字段的命名类型, 并在`Select`子句中创建和初始化该类型的实例。 仅在以下情况下使用此选项: 必须在返回的集合之外使用各个结果, 或者必须在方法调用中将它们作为参数传递。 以下示例`londonCusts5`中的类型为 IEnumerable (of NamePhone)。  
  
     [!code-vb[VbLINQBasicOps#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#7)]  
  
     [!code-vb[VbLINQBasicOps#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#8)]  
  
 有关如何在 Visual Basic 中使用子句的`Select`详细信息, 请参阅[Select 子句](../../../../visual-basic/language-reference/queries/select-clause.md)。  
  
## <a name="joining-data-join-and-group-join"></a>联接数据 (联接和分组联接)  
 可以通过多种方式在`From`子句中组合多个数据源。 例如, 以下代码使用两个数据源, 并在结果中隐式组合这两个数据源的属性。 查询选择姓氏以元音开头的学生。  
  
 [!code-vb[VbLINQBasicOps#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#9)]  
  
> [!NOTE]
> 你可以通过在如何以下操作中[创建的学生列表运行此代码:创建项](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)列表。  
  
 关键字等效于 SQL 中的`INNER JOIN`。 `Join` 它基于两个集合中的元素之间的匹配键值合并两个集合。 查询返回所有或部分具有匹配键值的集合元素。 例如, 以下代码将复制上一个隐式联接的操作。  
  
 [!code-vb[VbLINQBasicOps#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#10)]  
  
 `Group Join`将集合组合为单个层次结构集合, 就像`LEFT JOIN` SQL 中的一样。 有关详细信息, 请参阅[Join 子句](../../../../visual-basic/language-reference/queries/join-clause.md)和[Group Join 子句](../../../../visual-basic/language-reference/queries/group-join-clause.md)。  
  
## <a name="grouping-data-group-by"></a>数据分组 (Group By)  
 您可以添加一个`Group By`子句, 以便根据元素的一个或多个字段对查询结果中的元素进行分组。 例如, 下面的代码按课程年份对学生进行分组。  
  
 [!code-vb[VbLINQBasicOps#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#11)]  
  
 如果运行此代码, 请使用在[如何:创建项](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)列表, `For Each`语句的输出为:  
  
 年初级  
  
 Tucker、Michael  
  
 Garcia、Hugo  
  
 Garcia、Debra  
  
 Tucker、Lance  
  
 年高级  
  
 Omelchenko, Svetlana  
  
 Osada、Michiko  
  
 Fakhouri, Fadi  
  
 Feng、冯汉英 (  
  
 Adams, Terry  
  
 年Freshman  
  
 Mortensen, Sven  
  
 Garcia、Cesar  
  
 以下代码中显示的变体对类年进行排序, 然后按姓氏对每年内的学生进行排序。  
  
 [!code-vb[VbLINQBasicOps#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#12)]  
  
 有关`Group By`的详细信息, 请参阅[Group by 子句](../../../../visual-basic/language-reference/queries/group-by-clause.md)。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Collections.Generic.IEnumerable%601>
- [Visual Basic 中的 LINQ 入门](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)
- [查询](../../../../visual-basic/language-reference/queries/index.md)
- [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
