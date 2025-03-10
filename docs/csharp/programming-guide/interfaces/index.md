---
title: 接口 - C# 编程指南
ms.custom: seodec18
ms.date: 08/21/2018
helpviewer_keywords:
- interfaces [C#]
- C# language, interfaces
ms.assetid: 2feda177-ce11-432d-81b4-d50f5f35fd37
ms.openlocfilehash: 30c44b9f98bcc61d54b8103b6b40d14fd35715f4
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589181"
---
# <a name="interfaces-c-programming-guide"></a>接口（C# 编程指南）

接口包含[类](../../language-reference/keywords/class.md)或[结构](../../language-reference/keywords/struct.md)可以实现的一组相关功能的定义。
  
例如，使用接口可以在类中包括来自多个源的行为。 该功能在 C# 中十分重要，因为该语言不支持类的多重继承。 此外，如果要模拟结构的继承，也必须使用接口，因为它们无法实际从另一个结构或类继承。  
  
可使用 [interface](../../language-reference/keywords/interface.md) 关键字定义接口。 如以下示例所示。  
  
 [!code-csharp[csProgGuideInheritance#47](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#47)]  

结构名称必须是有效的 C# [标识符名称](../inside-a-program/identifier-names.md)。 按照约定，接口名称以大写字母 `I` 开头。

实现 <xref:System.IEquatable%601> 接口的任何类或结构都必须包含与该接口指定的签名匹配的 <xref:System.IEquatable%601.Equals%2A> 方法的定义。 因此，可以依靠实现 `IEquatable<T>` 的类来包含 `Equals` 方法，类的实例可以通过该方法确定它是否等于相同类的另一个实例。  
  
`IEquatable<T>` 的定义不为 `Equals` 提供实现。 该接口仅定义签名。 这样，C# 中的接口便类似于其中所有方法都是抽象方法的抽象类。 但是，类或结构可以实现多个接口，但是类只能继承单个类（抽象或不抽象）。
  
有关抽象类的详细信息，请参阅[抽象类、密封类及类成员](../classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
接口可以包含方法、属性、事件、索引器或这四种成员类型的任意组合。 有关示例的链接，请参阅[相关部分](./index.md#BKMK_RelatedSections)。 接口不能包含常量、字段、运算符、实例构造函数、终结器或类型。 接口成员会自动成为公共成员，不能包含任何访问修饰符。 成员也不能是[静态](../../language-reference/keywords/static.md)成员。  
  
若要实现接口成员，实现类的对应成员必须是公共、非静态，并且具有与接口成员相同的名称和签名。  
  
当类或结构实现接口时，类或结构必须为该接口定义的所有成员提供实现。 接口本身不提供类或结构可以通过继承基类功能的方式来继承的任何功能。 但是，如果基类实现接口，则从基类派生的任何类都会继承该实现。  
  
下面的示例演示 <xref:System.IEquatable%601> 接口的实现。 实现类 `Car` 必须提供 <xref:System.IEquatable%601.Equals%2A> 方法的实现。  
  
 [!code-csharp[csProgGuideInheritance#48](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#48)]  
  
类的属性和索引器可以为接口中定义的属性或索引器定义额外的访问器。 例如，接口可能会声明包含 [get](../../language-reference/keywords/get.md) 取值函数的属性。 实现此接口的类可以声明包含 `get` 和 [set](../../language-reference/keywords/set.md) 取值函数的同一属性。 但是，如果属性或索引器使用显式实现，则访问器必须匹配。 有关显式实现的详细信息，请参阅[显式接口实现](explicit-interface-implementation.md)和[接口属性](../classes-and-structs/interface-properties.md)。  

接口可以从其他接口继承。 类可能通过它继承的基类或通过其他接口继承的接口来多次包含某个接口。 但是，类只能提供接口的实现一次，并且仅当类将接口作为类定义的一部分 (`class ClassName : InterfaceName`) 进行声明时才能提供。 如果由于继承实现接口的基类而继承了接口，则基类会提供接口的成员的实现。 但是，派生类可以重新实现任何虚拟接口成员，而不是使用继承的实现。  
  
基类还可以使用虚拟成员实现接口成员。 在这种情况下，派生类可以通过重写虚拟成员来更改接口行为。 有关虚拟成员的详细信息，请参阅[多态性](../classes-and-structs/polymorphism.md)。  
  
## <a name="interfaces-summary"></a>接口摘要

接口具有以下属性：  

- 接口类似于只有抽象成员的抽象基类。 实现接口的任何类或结构都必须实现其所有成员。
- 接口无法直接进行实例化。 其成员由实现接口的任何类或结构来实现。
- 接口可以包含事件、索引器、方法和属性。
- 接口不包含方法的实现。
- 一个类或结构可以实现多个接口。 一个类可以继承一个基类，还可实现一个或多个接口。

## <a name="in-this-section"></a>本节内容

[显式接口实现](explicit-interface-implementation.md)  
 说明如何创建特定于接口的类成员。  
  
 [如何：显式实现接口成员](how-to-explicitly-implement-interface-members.md)  
 提供有关如何显式实现接口的成员的示例。  
  
 [如何：显式实现两个接口的成员](how-to-explicitly-implement-members-of-two-interfaces.md)  
 提供有关如何使用继承显式实现接口的成员的示例。  
  
## <a name="BKMK_RelatedSections"></a>相关部分

- [接口属性](../classes-and-structs/interface-properties.md)  
- [接口中的索引器](../indexers/indexers-in-interfaces.md)  
- [如何：实现接口事件](../events/how-to-implement-interface-events.md)  
- [类和结构](../classes-and-structs/index.md)  
- [继承](../classes-and-structs/inheritance.md)  
- [方法](../classes-and-structs/methods.md)  
- [多态性](../classes-and-structs/polymorphism.md)  
- [抽象类、密封类及类成员](../classes-and-structs/abstract-and-sealed-classes-and-class-members.md)  
- [属性](../classes-and-structs/properties.md)  
- [事件](../events/index.md)  
- [索引器](../indexers/index.md)  
  
## <a name="featured-book-chapter"></a>重要章节

[学习 C# 3.0：掌握 C# 3.0 基础知识](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652493%28v%253dorm.10%29)中的[接口](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652489%28v%3Dorm.10%29)

## <a name="see-also"></a>请参阅

- [C# 编程指南](../index.md)
- [继承](../classes-and-structs/inheritance.md)
- [标识符名称](../inside-a-program/identifier-names.md)
