---
title: Visual Basic 中的运算符优先级
ms.date: 07/20/2015
helpviewer_keywords:
- arithmetic operators [Visual Basic], precedence
- operator precedence
- logical operators [Visual Basic], precedence
- operators [Visual Basic], associativity
- operators [Visual Basic], resolution
- associativity of operators [Visual Basic]
- operators [Visual Basic], precedence
- precedence [Visual Basic], of operators
- comparison operators [Visual Basic], precedence
- math operators [Visual Basic]
- order of precedence
ms.assetid: cbbdb282-f572-458e-a520-008a675f8063
ms.openlocfilehash: df40aced45442c9c7895c8d10ece64b21e292508
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659929"
---
# <a name="operator-precedence-in-visual-basic"></a>Visual Basic 中的运算符优先级
当表达式中发生多个操作时, 将按预先确定的顺序 (称为*运算符优先级*) 来计算和解析各个部分。

## <a name="precedence-rules"></a>优先规则
 当表达式包含多个类别中的运算符时, 将根据以下规则对其进行评估:

- 算术运算符和串联运算符具有以下部分中描述的优先级顺序, 并且其优先级比比较、逻辑和按位运算符的优先级高。

- 所有比较运算符都具有相同的优先级, 并且其优先级比逻辑 and 位运算符更高, 但优先级低于算术运算符和串联运算符。

- 逻辑运算符和位运算符具有以下部分中描述的优先级顺序, 并且其优先级低于算术运算符、串联运算符和比较运算符。

- 具有相同优先级的运算符将按照它们在表达式中出现的顺序从左到右进行计算。

## <a name="precedence-order"></a>优先顺序
 运算符的优先顺序如下:

### <a name="await-operator"></a>Await 运算符
 Await

### <a name="arithmetic-and-concatenation-operators"></a>算术和串联运算符
 幂 (`^`)

 一元恒等运算 (`+`, `–`)

 乘法和浮点除法 (`*`,) `/`

 整数除法 (`\`)

 模块化算法`Mod`()

 加法和减法 (`+`, `–`)

 字符串串联 (`&`)

 算术移位 (`<<`, `>>`)

### <a name="comparison-operators"></a>比较运算符
 所有比较运算符 (`=`、 `<>` `<` `<=` 、、`>`、、 、`>=`、、 、...`TypeOf` `Like` `Is` `IsNot``Is`)

### <a name="logical-and-bitwise-operators"></a>逻辑运算符和位运算符
 求反`Not`()

 结合 (`And`、 `AndAlso`)

 包含析取`Or`( `OrElse`,)

 排他性析取`Xor`()

### <a name="comments"></a>注释
 `=`运算符只是相等比较运算符, 而不是赋值运算符。

 字符串串联运算符 (`&`) 不是算术运算符, 但其优先级与算术运算符组合在一起。

 `Is` 和`IsNot`运算符是对象引用比较运算符。 它们不会比较两个对象的值;它们仅检查以确定两个对象变量是否引用同一对象实例。

## <a name="associativity"></a>结合性
 当相同优先级的运算符同时出现在表达式中时 (例如, 乘法和除法), 编译器将按从左至右的顺序计算每个运算。 下面的示例阐释了这一点。

```vb
Dim n1 As Integer = 96 / 8 / 4
Dim n2 As Integer = (96 / 8) / 4
Dim n3 As Integer = 96 / (8 / 4)
```

 第一个表达式计算相除后的 96/8 (结果为 12), 然后是除法 12/4, 这会产生三个结果。 由于编译器会按`n1`从左至右的顺序计算运算, 因此当显式`n2`指示该顺序时, 计算是相同的。 `n1` 和`n2`都具有三个结果。 相反, `n3`结果为 48, 因为括号强制编译器首先计算 8/4。

 由于此行为, 在 Visual Basic 中, 运算符被称为*左结合*。

## <a name="overriding-precedence-and-associativity"></a>重写优先级和关联性
 您可以使用括号来强制在其他部分中计算表达式。 这可以覆盖优先级顺序和左侧相关性。 Visual Basic 始终执行括在括号内的操作。 但在括号中, 它将保持普通的优先级和关联性, 除非在括号内使用括号。 下面的示例阐释了这一点。

```vb
Dim a, b, c, d, e, f, g As Double
a = 8.0
b = 3.0
c = 4.0
d = 2.0
e = 1.0
f = a - b + c / d * e
' The preceding line sets f to 7.0. Because of natural operator
' precedence and associativity, it is exactly equivalent to the
' following line.
f = (a - b) + ((c / d) * e)
' The following line overrides the natural operator precedence
' and left associativity.
g = (a - (b + c)) / (d * e)
' The preceding line sets g to 0.5.
```

## <a name="see-also"></a>请参阅

- [= 运算符](../../../visual-basic/language-reference/operators/assignment-operator.md)
- [Is 运算符](../../../visual-basic/language-reference/operators/is-operator.md)
- [IsNot 运算符](../../../visual-basic/language-reference/operators/isnot-operator.md)
- [Like 运算符](../../../visual-basic/language-reference/operators/like-operator.md)
- [TypeOf 运算符](../../../visual-basic/language-reference/operators/typeof-operator.md)
- [Await 运算符](../../../visual-basic/language-reference/operators/await-operator.md)
- [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
