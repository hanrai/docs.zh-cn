---
title: C# 运算符 - C# 参考
ms.date: 08/20/2019
f1_keywords:
- cs.operators
helpviewer_keywords:
- operators [C#]
- operator precedence [C#]
- operator associativity [C#]
- expressions [C#]
ms.assetid: 0301e31f-22ad-49af-ac3c-d5eae7f0ac43
ms.openlocfilehash: 0f7e99aaa171160a813b14dc818846052766551e
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70168599"
---
# <a name="c-operators-c-reference"></a>C# 运算符（C# 参考）

C# 提供了许多由内置类型支持的运算符。 例如，[算术运算符](arithmetic-operators.md)使用数值操作数执行算术运算，[布尔逻辑运算符](boolean-logical-operators.md)使用 [bool](../keywords/bool.md) 操作数执行逻辑运算。 特定的运算符可[重载](operator-overloading.md)。 使用运算符重载，可以为用户定义类型的操作数指定运算符行为。

在[表达式](../../programming-guide/statements-expressions-operators/expressions.md)中，运算符优先级和结合性决定了操作的执行顺序。 可以使用括号更改由运算符优先级和结合性决定的计算顺序。

## <a name="operator-precedence"></a>运算符优先级

在包含多个运算符的表达式中，先按优先级较高的运算符计算，再按优先级较低的运算符计算。 在下面的示例中，首先执行乘法，因为其优先级高于加法：

```csharp-interactive
var a = 2 + 2 * 2;
Console.WriteLine(a); //  output: 6
```

使用括号更改运算符优先级所施加的计算顺序：

```csharp-interactive
var a = (2 + 2) * 2;
Console.WriteLine(a); //  output: 8
```

下表按最高优先级到最低优先级的顺序列出 C# 运算符。 每行中运算符的优先级相同。

| 运算符 | 类别或名称 |
| --------- | ---------------- |
| [x.y](member-access-operators.md#member-access-operator-)、[x?.y](member-access-operators.md#null-conditional-operators--and-)、[x?[y]](member-access-operators.md#null-conditional-operators--and-)、[f(x)](member-access-operators.md#invocation-operator-)、[a&#91;i&#93;](member-access-operators.md#indexer-operator-)、[x++](arithmetic-operators.md#increment-operator-)、[x--](arithmetic-operators.md#decrement-operator---)、[new](new-operator.md)、[typeof](type-testing-and-cast.md#typeof-operator)、[checked](../keywords/checked.md)、[unchecked](../keywords/unchecked.md)、[default](default.md)、[nameof](nameof.md)、[delegate](delegate-operator.md)、[sizeof](sizeof.md)、[stackalloc](stackalloc.md)、[x->y](pointer-related-operators.md#pointer-member-access-operator--) | 基本 |
| [+x](arithmetic-operators.md#unary-plus-and-minus-operators)、[-x](arithmetic-operators.md#unary-plus-and-minus-operators)、[\!x](boolean-logical-operators.md#logical-negation-operator-)、[~x](bitwise-and-shift-operators.md#bitwise-complement-operator-)、[++x](arithmetic-operators.md#increment-operator-)、[--x](arithmetic-operators.md#decrement-operator---)、[(T)x](type-testing-and-cast.md#cast-operator-)、[await](await.md)、[&x](pointer-related-operators.md#address-of-operator-)、[*x](pointer-related-operators.md#pointer-indirection-operator-)、[true 和 false](true-false-operators.md) | 一元 |
| [x * y](arithmetic-operators.md#multiplication-operator-)、[x / y](arithmetic-operators.md#division-operator-)、[x % y](arithmetic-operators.md#remainder-operator-) | 乘法|
| [x + y](arithmetic-operators.md#addition-operator-)、[x – y](arithmetic-operators.md#subtraction-operator--) | 加法 |
| [x \<\<  y](bitwise-and-shift-operators.md#left-shift-operator-)、[x >> y](bitwise-and-shift-operators.md#right-shift-operator-) | 移位 |
| [x \< y](comparison-operators.md#less-than-operator-)、[x > y](comparison-operators.md#greater-than-operator-)、[x \<= y](comparison-operators.md#less-than-or-equal-operator-)、[x >= y](comparison-operators.md#greater-than-or-equal-operator-)、[is](type-testing-and-cast.md#is-operator)、[as](type-testing-and-cast.md#as-operator) | 关系和类型测试 |
| [x == y](equality-operators.md#equality-operator-)、[x != y](equality-operators.md#inequality-operator-) | 相等 |
| `x & y` | [布尔逻辑 AND](boolean-logical-operators.md#logical-and-operator-) 或[按位逻辑 AND](bitwise-and-shift-operators.md#logical-and-operator-) |
| `x ^ y` | [布尔逻辑 XOR](boolean-logical-operators.md#logical-exclusive-or-operator-) 或[按位逻辑 XOR](bitwise-and-shift-operators.md#logical-exclusive-or-operator-) |
| <code>x &#124; y</code> | [布尔逻辑 OR](boolean-logical-operators.md#logical-or-operator-) 或[按位逻辑 OR](bitwise-and-shift-operators.md#logical-or-operator-) |
| [x && y](boolean-logical-operators.md#conditional-logical-and-operator-) | 条件“与” |
| [x &#124;&#124; y](boolean-logical-operators.md#conditional-logical-or-operator-) | 条件“或” |
| [x ?? y](null-coalescing-operator.md) | Null 合并运算符 |
| [c ? t : f](conditional-operator.md) | 条件运算符 |
| [x = y](assignment-operator.md)、[x += y](arithmetic-operators.md#compound-assignment)、[x -= y](arithmetic-operators.md#compound-assignment)、[x *= y](arithmetic-operators.md#compound-assignment)、[x /= y](arithmetic-operators.md#compound-assignment)、[x %= y](arithmetic-operators.md#compound-assignment)、[x &= y](boolean-logical-operators.md#compound-assignment)、[x &#124;= y](boolean-logical-operators.md#compound-assignment)、[x ^= y](boolean-logical-operators.md#compound-assignment)、[x <<= y](bitwise-and-shift-operators.md#compound-assignment)、[x >>= y](bitwise-and-shift-operators.md#compound-assignment)、[=>](lambda-operator.md) | 赋值和 lambda 声明 |

## <a name="operator-associativity"></a>运算符结合性

当运算符的优先级相同，运算符的结合性决定了运算的执行顺序：

- 左结合运算符按从左到右的顺序计算。  除[赋值运算符](assignment-operator.md)和 [null 合并运算符 `??`](null-coalescing-operator.md)外，所有二元运算符都是左结合运算符。 例如，`a + b - c` 将计算为 `(a + b) - c`。
- 右结合运算符按从右到左的顺序计算。  赋值运算符、null 合并运算符 `??` 和[条件运算符 `?:`](conditional-operator.md)是右结合运算符。 例如，`x = y = z` 将计算为 `x = (y = z)`。

使用括号更改运算符结合性所施加的计算顺序：

```csharp-interactive
int a = 13 / 5 / 2;
int b = 13 / (5 / 2);
Console.WriteLine($"a = {a}, b = {b}");  // output: a = 1, b = 6
```

## <a name="operand-evaluation"></a>操作数计算

与运算符的优先级和结合性无关，从左到右计算表达式中的操作数。 以下示例展示了运算符和操作数的计算顺序：

| 表达式 | 计算顺序 |
| ---------- | ------------------- |
|`a + b`|a, b, +|
|`a + b * c`|a, b, c, *, +|
|`a / b + c * d`|a, b, /, c, d, *, +|
|`a / (b + c) * d`|a, b, c, +, /, d, *|

通常，会计算所有运算符操作数。 某些运算符有条件地计算操作数。 也就是说，此类运算符的第一个操作数的值定义了是否应计算其他操作数，或计算其他哪些操作数。 这些运算符有条件逻辑 [AND (`&&`)](boolean-logical-operators.md#conditional-logical-and-operator-) 和 [OR (`||`)](boolean-logical-operators.md#conditional-logical-or-operator-) 运算符、[null 合并运算符 `??`](null-coalescing-operator.md)、[null 条件运算符 `?.` 和和 `?[]`](member-access-operators.md#null-conditional-operators--and-)，以及[条件运算符 `?:`](conditional-operator.md)。 有关更多详细信息，请参阅每个运算符的说明。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)中的[运算符](~/_csharplang/spec/expressions.md#operators)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [表达式](../../programming-guide/statements-expressions-operators/expressions.md)
