---
title: 使用 LINQ 进行数据转换 (C#)
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], data transformations
- source elements [LINQ in C#]
- joining multiple inputs [LINQ in C#]
- multiple outputs for one output sequence [LINQ in C#]
- subset of source elements [LINQ in C#]
- data sources [LINQ in C#], data transformations
- data transformations [LINQ in C#]
ms.assetid: 674eae9e-bc72-4a88-aed3-802b45b25811
ms.openlocfilehash: f042042f36e373ec05e8f0f15c14027463653578
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924316"
---
# <a name="data-transformations-with-linq-c"></a>使用 LINQ 进行数据转换 (C#)
[!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] 不只是检索数据。 它也是用于转换数据的强大工具。 通过使用 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询，可以使用源序列作为输入，并通过多种方式对其进行修改，以创建新的输出序列。 通过排序和分组，你可以修改序列本身，而无需修改这些元素本身。 但也许 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询最强大的功能是创建新类型。 这可以在 [select](../../../language-reference/keywords/select-clause.md) 子句中完成。 例如，可以执行下列任务：  
  
- 将多个输入序列合并为具有新类型的单个输出序列。  
  
- 创建其元素由源序列中每个元素的一个或多个属性组成的输出序列。  
  
- 创建其元素由对源数据执行的操作结果组成的输出序列。  
  
- 创建其他格式的输出序列。 例如，可以将数据从 SQL 行或文本文件转换为 XML。  
  
 这只是几个例子。 当然，可以以各种方式在同一查询中组合这些转换。 此外，一个查询的输出序列可以用作新查询的输入序列。  
  
## <a name="joining-multiple-inputs-into-one-output-sequence"></a>将多个输入联接到一个输出序列中  
 可以使用 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询创建包含元素的输出序列，这些元素来自多个输入序列。 以下示例演示如何组合两个内存中数据结构，但相同的原则可应用于组合来自 XML 或 SQL 或数据集源的数据。 假设以下两种类类型：  
  
 [!code-csharp[CsLINQGettingStarted#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#7)]  
  
 以下示例演示了查询：  
  
 [!code-csharp[CSLinqGettingStarted#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#8)]  
  
 有关详细信息，请参阅 [join 子句](../../../language-reference/keywords/join-clause.md)和 [select 子句](../../../language-reference/keywords/select-clause.md)。  
  
## <a name="selecting-a-subset-of-each-source-element"></a>选择每个源元素的子集  
 有两种主要方法来选择源序列中每个元素的子集：  
  
1. 若要仅选择源元素的一个成员，请使用点操作。 在以下示例中，假设 `Customer` 对象包含多个公共属性，包括名为 `City` 的字符串。 在执行时，此查询将生成字符串的输出序列。  
  
    ```csharp
    var query = from cust in Customers  
                select cust.City;  
    ```  
  
2. 若要创建包含多个源元素属性的元素，可以使用带有命名对象或匿名类型的对象初始值设定项。 以下示例演示如何使用匿名类型封装每个 `Customer` 元素的两个属性：  
  
    ```csharp
    var query = from cust in Customer  
                select new {Name = cust.Name, City = cust.City};  
    ```  
  
 有关详细信息，请参阅[对象和集合初始值设定项](../../classes-and-structs/object-and-collection-initializers.md)和[匿名类型](../../classes-and-structs/anonymous-types.md)。  
  
## <a name="transforming-in-memory-objects-into-xml"></a>将内存中对象转换为 XML  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询可以轻松地在内存中数据结构、SQL 数据库、ADO.NET 数据集和 XML 流或文档之间转换数据。 以下示例将内存中数据结构中的对象转换为 XML 元素。  
  
 [!code-csharp[CsLINQGettingStarted#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#9)]  
  
 此代码生成以下 XML 输出：  
  
```xml  
<Root>  
  <student>  
    <First>Svetlana</First>  
    <Last>Omelchenko</Last>  
    <Scores>97,92,81,60</Scores>  
  </student>  
  <student>  
    <First>Claire</First>  
    <Last>O'Donnell</Last>  
    <Scores>75,84,91,39</Scores>  
  </student>  
  <student>  
    <First>Sven</First>  
    <Last>Mortensen</Last>  
    <Scores>88,94,65,91</Scores>  
  </student>  
</Root>  
```  
  
 有关详细信息，请参阅[在 C# 中创建 XML 树 (LINQ to XML)](./creating-xml-trees-linq-to-xml-2.md)。  
  
## <a name="performing-operations-on-source-elements"></a>对源元素执行操作  
 输出序列可能不包含源序列中的任何元素或元素属性。 输出可能是使用源元素作为输入参数而计算得出的值序列。 以下简单查询在执行时会输出一串字符串，其值表示基于 `double` 类型的元素的源序列的计算结果。  
  
> [!NOTE]
> 如果查询将被转换为另一个域，则不支持在查询表达式中调用方法。 例如，不能在 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 中调用普通的 C# 方法，因为 SQL Server 没有用于它的上下文。 但是，可以将存储过程映射到方法并调用这些方法。 有关详细信息，请参阅[存储过程](../../../../framework/data/adonet/sql/linq/stored-procedures.md)。  
  
 [!code-csharp[CsLINQGettingStarted#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#10)]  
  
## <a name="see-also"></a>请参阅

- [语言集成查询 (LINQ) (C#)](./index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)
- [LINQ to XML (C#)](./linq-to-xml-overview.md)
- [LINQ 查询表达式](../../linq-query-expressions/index.md)
- [select 子句](../../../language-reference/keywords/select-clause.md)
