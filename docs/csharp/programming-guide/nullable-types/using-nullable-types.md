---
title: 使用可以为 null 的类型 - C# 编程指南
ms.custom: seodec18
description: 了解如何使用 C# 可以为 null 的类型
ms.date: 08/02/2018
helpviewer_keywords:
- nullable types [C#], about nullable types
ms.assetid: 0bacbe72-ce15-4b14-83e1-9c14e6380c28
ms.openlocfilehash: 75b8889f5f1f1b0dab4aa365daa34ef5ae226b02
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588831"
---
# <a name="using-nullable-types-c-programming-guide"></a>使用可以为 null 的类型（C# 编程指南）

可以为 null 的类型是表示基础值类型 `T` 的所有值的类型，还可表示一个 [NULL](../../language-reference/keywords/null.md) 值。 有关详细信息，请参阅[可以为 null 的类型](index.md)主题。

可使用以下任何一种形式引用可以为 null 的类型：`Nullable<T>` 或 `T?`。 这两种形式是可互换的。  
  
## <a name="declaration-and-assignment"></a>声明和赋值

由于值类型可隐式转换为相应的可以为 null 的类型，因此可像为其基础值类型赋值一样，为可以为 null 的类型赋值。 还可分配 `null` 值。  例如:
  
[!code-csharp[declare and assign](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#1)]

## <a name="examination-of-a-nullable-type-value"></a>检查可以为 null 的类型的值

使用以下只读属性检查可以为 null 的类型的实例是否为 null，并检索基础类型的值：  
  
- <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> 指示可以为 null 的类型的实例是否具有其基础类型的值。
  
- 如果 <xref:System.Nullable%601.HasValue%2A> 为 `true`，则 <xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> 获取基础类型的值。 如果 <xref:System.Nullable%601.HasValue%2A> 为 `false`，则 <xref:System.Nullable%601.Value%2A> 属性将引发 <xref:System.InvalidOperationException>。
  
以下示例中的代码使用 `HasValue` 属性在显示值之前测试变量是否包含该值：
  
[!code-csharp-interactive[use HasValue](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#2)]
  
还可将可以为 null 的类型的变量与 `null` 进行比较，而不是使用 `HasValue` 属性，如以下示例所示：  
  
[!code-csharp-interactive[use comparison with null](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#3)]

从 C# 7.0 开始，可以使用[模式匹配](../../pattern-matching.md)来检查和获取可以为 null 的类型的值：

[!code-csharp-interactive[use pattern matching](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#4)]

## <a name="conversion-from-a-nullable-type-to-an-underlying-type"></a>从可以为 null 的类型转换为基础类型

如果需要将可以为 null 的类型的值分配给不可以为 null 的类型，请使用 [null-coalescing 运算符`??`](../../language-reference/operators/null-coalescing-operator.md)指定可以为 null 的类型的值为 null 时要分配的值（也可使用 <xref:System.Nullable%601.GetValueOrDefault(%600)?displayProperty=nameWithType> 方法来执行此操作）：
  
[!code-csharp-interactive[?? operator](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#5)]

如果可以为 null 的类型的值为 null 时要使用的值应为基础值类型的默认值，请使用 <xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType> 方法。
  
可显式地将可以为 null 的类型强制转换为不可以为 null 的类型。 例如:  
  
[!code-csharp[explicit cast](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#6)]

在运行时，如果可以为 null 的类型的值为 null，则显式强制转换将引发 <xref:System.InvalidOperationException>。

不可以为 null 的值类型隐式转换为相应的可以为 null 的类型。
  
## <a name="operators"></a>运算符

可为 null 的类型还可使用预定义的一元运算符和二元运算符以及任何用于值类型的用户定义的运算符。 如果一个或两个操作数为 null，则这些运算符将生成一个 null 值；否则，运算符使用所包含的值来计算结果。 例如:  
  
[!code-csharp[operators](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#7)]

> [!NOTE]
> 对于 `bool?` 类型，预定义的 `&` 和 `|` 运算符不遵循此部分中描述的规则：即使其中一个操作数为 null，运算符计算结果也可以不为 null。 有关详细信息，请参阅[布尔逻辑运算符](../../language-reference/operators/boolean-logical-operators.md)一文的[可以为 null 的布尔逻辑运算符](../../language-reference/operators/boolean-logical-operators.md#nullable-boolean-logical-operators)部分。
  
对于关系运算符（`<`、`>`、`<=`、`>=`），如果一个或两个操作数为 null，则结果为 `false`。 请勿作出如下假定：由于某个特定的比较（例如 `<=`）返回 `false`，则相反的比较 (`>`) 返回 `true`。 以下示例显示 10

- 既不大于等于 null，
- 也不小于 null。
  
[!code-csharp-interactive[relational and equality operators](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#8)]
  
以上示例还表明，对两个均为 null 的可以为 null 的类型进行相等比较，其计算结果为 `true`。

有关详细信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)中的[提升运算符](~/_csharplang/spec/expressions.md#lifted-operators)部分。

## <a name="boxing-and-unboxing"></a>装箱和取消装箱

可通过以下规则将可以为 null 的值类型[装箱](../types/boxing-and-unboxing.md)：

- 如果 <xref:System.Nullable%601.HasValue%2A> 返回 `false`，则生成空引用。  
- 如果 <xref:System.Nullable%601.HasValue%2A> 返回 `true`，则基础值类型 `T` 的值将装箱，而不对 <xref:System.Nullable%601> 的实例进行装箱。

可将已装箱的值类型取消装箱到相应的可以为 null 的类型，如以下示例所示：

[!code-csharp-interactive[boxing and unboxing](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#9)]

## <a name="see-also"></a>请参阅

- [可以为 null 的类型](index.md)
- [C# 编程指南](../index.md)
- [“提升”的准确含义是什么？](https://blogs.msdn.microsoft.com/ericlippert/2007/06/27/what-exactly-does-lifted-mean/)
