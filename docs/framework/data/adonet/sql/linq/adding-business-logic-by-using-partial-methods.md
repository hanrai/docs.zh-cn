---
title: 通过使用分部方法添加业务逻辑
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3a73991e-fd4e-4610-93fb-7ced4dc6b7f9
ms.openlocfilehash: e3f82c260a2cab85270a9f33a87eb9a9f04b72c7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964145"
---
# <a name="adding-business-logic-by-using-partial-methods"></a>通过使用分部方法添加业务逻辑
您可以通过使用C# [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] *分部方法*自定义项目中的 Visual Basic 和生成的代码。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 生成的代码定义签名作为分部方法的一部分。 如果您要实现此方法，您可以添加自己的分部方法。 如果您不添加自己的实现，编译器将丢弃分部方法签名并调用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中的默认方法。  
  
> [!NOTE]
> 如果使用的是 Visual Studio, 则可以使用对象关系设计器向实体类添加验证及其他自定义项。  
  
 例如，Northwind 示例数据库中 `Customer` 类的默认映射包括下面的分部方法：  
  
 [!code-csharp[DLinqOverrideDefault#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#2)]
 [!code-vb[DLinqOverrideDefault#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#2)]  
  
 您可以向自己的分部 `Customer` 类添加诸如以下内容的代码来实现自己的方法。  
  
 [!code-csharp[DLinqOverrideDefault#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/Program.cs#3)]
 [!code-vb[DLinqOverrideDefault#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/Module1.vb#3)]  
  
 在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中通常使用这种方式来重写 `Insert`、`Update`、`Delete` 的默认方法以及在对象生命周期事件过程中验证属性。  
  
 有关详细信息, 请参阅[分部方法](../../../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md)(Visual Basic) 或[分部 (方法)C# ](../../../../../csharp/language-reference/keywords/partial-method.md) C#("")。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例首先显示了 `ExampleClass`，因为它可能是由像 SQLMetal 这样的代码生成工具定义的；然后，此示例演示了如何只实现两个方法之一。  
  
### <a name="code"></a>代码  
 [!code-csharp[DLinqSubmittingChanges#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#4)]
 [!code-vb[DLinqSubmittingChanges#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#4)]  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例用到了 `Shipper` 和 `Order` 实体之间的关系。 请注意这些方法中的分部方法 `InsertShipper` 和 `DeleteShipper`。 这些方法重写了由 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 映射提供的默认分部方法。  
  
### <a name="code"></a>代码  
 [!code-csharp[DLinqOverrideDefault#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#1)]
 [!code-vb[DLinqOverrideDefault#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#1)]  
  
## <a name="see-also"></a>请参阅

- [进行和提交数据更改](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)
- [自定义插入、更新和删除操作](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)
