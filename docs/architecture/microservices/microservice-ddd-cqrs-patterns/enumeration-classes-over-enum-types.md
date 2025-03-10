---
title: 使用枚举类（而不是枚举类型）
description: 适用于容器化 .NET 应用程序的 .NET 微服务体系结构 | 了解如何使用枚举类来解决枚举的某些局限性。
ms.date: 10/08/2018
ms.openlocfilehash: ba687b700d7a6105baf71aa08a0d888afc9a8ec3
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70202735"
---
# <a name="use-enumeration-classes-instead-of-enum-types"></a>使用枚举类（而不是枚举类型）

[枚举](../../../csharp/language-reference/keywords/enum.md)（或枚举类型）是围绕整型类型的精简语言包装器  。 建议在存储一组封闭值中的一个值时，限制对它们的使用。 基于大小（小、中、大）的分类是一个很好的示例。 对控制流或更强健的抽象使用枚举可成为[代码气味](https://deviq.com/code-smells/)。 这种使用方式会使代码很脆弱，并且会使许多控制流语句检查枚举值。

相反，你可以创建枚举类，启动面向对象语言的所有丰富功能。

但这不是关键点，在许多情况下，为了简便起见，如果喜欢，仍然可以使用常规[枚举类型](../../../csharp/language-reference/keywords/enum.md)。 总之，枚举类的使用与业务相关概念的关系更密切。

## <a name="implement-an-enumeration-base-class"></a>实现枚举基类

eShopOnContainers 中的订购微服务提供了一个示例枚举基类实现，如下例所示：

```csharp
public abstract class Enumeration : IComparable
{
    public string Name { get; private set; }

    public int Id { get; private set; }

    protected Enumeration(int id, string name) 
    {
        Id = id; 
        Name = name; 
    }

    public override string ToString() => Name;

    public static IEnumerable<T> GetAll<T>() where T : Enumeration
    {
        var fields = typeof(T).GetFields(BindingFlags.Public | 
                                         BindingFlags.Static | 
                                         BindingFlags.DeclaredOnly); 

        return fields.Select(f => f.GetValue(null)).Cast<T>();
    }

    public override bool Equals(object obj) 
    {
        var otherValue = obj as Enumeration; 

        if (otherValue == null) 
            return false;

        var typeMatches = GetType().Equals(obj.GetType());
        var valueMatches = Id.Equals(otherValue.Id);

        return typeMatches && valueMatches;
    }

    public int CompareTo(object other) => Id.CompareTo(((Enumeration)other).Id); 

    // Other utility methods ... 
}
```

可将此类用作任何实体或值对象中的类型，如以下 `CardType` : `Enumeration` 类：

```csharp
public class CardType : Enumeration
{
    public static CardType Amex = new CardType(1, "Amex");
    public static CardType Visa = new CardType(2, "Visa");
    public static CardType MasterCard = new CardType(3, "MasterCard");

    public CardType(int id, string name)
        : base(id, name)
    {
    }
}
```

## <a name="additional-resources"></a>其他资源

- **Enum’s are evil—update （枚举有弊无利：更新）**  \
  <https://www.planetgeek.ch/2009/07/01/enums-are-evil/>

- **Daniel Hardman.How Enums Spread Disease — And How To Cure It （枚举如何扩大问题以及如何应对）**  \
  <https://codecraft.co/2012/10/29/how-enums-spread-disease-and-how-to-cure-it/>

- **Jimmy Bogard。Enumeration classes （枚举类）**  \
  <https://lostechies.com/jimmybogard/2008/08/12/enumeration-classes/>

- **Steve Smith.Enum Alternatives in C# （C# 中枚举的替代方案）**  \
  <https://ardalis.com/enum-alternatives-in-c>

- **Enumeration.cs.** eShopOnContainers 中的基础枚举类 \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/SeedWork/Enumeration.cs>

- **CardType.cs**. eShopOnContainers 中的枚举类示例。 \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/AggregatesModel/BuyerAggregate/CardType.cs>
    
- **SmartEnum**。 Ardalis - 帮助在 .NET 中生成强类型智能枚举的类。 \
  <https://www.nuget.org/packages/Ardalis.SmartEnum/>

>[!div class="step-by-step"]
>[上一页](implement-value-objects.md)
>[下一页](domain-model-layer-validations.md)
