---
title: 如何：使用自动实现的属性实现轻量类 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- auto-implemented properties [C#]
- properties [C#], auto-implemented
ms.assetid: 1dc5a8ad-a4f7-4f32-8506-3fc6d8c8bfed
ms.openlocfilehash: 4cbed8145487325d8b06882bbab843321a49d0d3
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596901"
---
# <a name="how-to-implement-a-lightweight-class-with-auto-implemented-properties-c-programming-guide"></a>如何：使用自动实现的属性实现轻量类（C# 编程指南）

本示例演示如何创建一个仅用于封装一组自动实现的属性的不可变轻型类。 当你必须使用引用类型语义时，请使用此种构造而不是结构。

可通过两种方法来实现不可变的属性：
- 可以将 [set](../../language-reference/keywords/set.md) 访问器声明为[专用](../../language-reference/keywords/private.md)。  属性只能在该类型中设置，但它对于使用者是不可变的。

  当你声明一个 private `set` 取值函数时，你无法使用对象初始值设定项来初始化属性。 你必须使用构造函数或工厂方法。
- 也可以仅声明 [get](../../language-reference/keywords/get.md) 访问器，使属性除了能在该类型的构造函数中可变，在其他任何位置都不可变。

## <a name="example"></a>示例

下面的示例演示了实现具有自动实现属性的不可变类的两种方法。 这两种方法均使用 private `set` 声明其中一个属性，使用单独的 `get` 声明另一个属性。  第一个类仅使用构造函数来初始化属性，第二个类则使用可调用构造函数的静态工厂方法。

```csharp
// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// constructor to initialize its properties.
class Contact
{
    // Read-only properties.
    public string Name { get; }
    public string Address { get; private set; }

    // Public constructor.
    public Contact(string contactName, string contactAddress)
    {
        Name = contactName;
        Address = contactAddress;
    }
}

// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// static method and private constructor to initialize its properties.
public class Contact2
{
    // Read-only properties.
    public string Name { get; private set; }
    public string Address { get; }

    // Private constructor.
    private Contact2(string contactName, string contactAddress)
    {
        Name = contactName;
        Address = contactAddress;
    }

    // Public factory method.
    public static Contact2 CreateContact(string name, string address)
    {
        return new Contact2(name, address);
    }
}

public class Program
{
    static void Main()
    {
        // Some simple data sources.
        string[] names = {"Terry Adams","Fadi Fakhouri", "Hanying Feng",
                            "Cesar Garcia", "Debra Garcia"};
        string[] addresses = {"123 Main St.", "345 Cypress Ave.", "678 1st Ave",
                                "12 108th St.", "89 E. 42nd St."};

        // Simple query to demonstrate object creation in select clause.
        // Create Contact objects by using a constructor.
        var query1 = from i in Enumerable.Range(0, 5)
                    select new Contact(names[i], addresses[i]);

        // List elements cannot be modified by client code.
        var list = query1.ToList();
        foreach (var contact in list)
        {
            Console.WriteLine("{0}, {1}", contact.Name, contact.Address);
        }

        // Create Contact2 objects by using a static factory method.
        var query2 = from i in Enumerable.Range(0, 5)
                        select Contact2.CreateContact(names[i], addresses[i]);

        // Console output is identical to query1.
        var list2 = query2.ToList();

        // List elements cannot be modified by client code.
        // CS0272:
        // list2[0].Name = "Eugene Zabokritski";

        // Keep the console open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}

/* Output:
    Terry Adams, 123 Main St.
    Fadi Fakhouri, 345 Cypress Ave.
    Hanying Feng, 678 1st Ave
    Cesar Garcia, 12 108th St.
    Debra Garcia, 89 E. 42nd St.
*/
```

编译器为每个自动实现的属性创建了支持字段。 这些字段无法直接从源代码进行访问。

## <a name="see-also"></a>请参阅

- [属性](./properties.md)
- [struct](../../language-reference/keywords/struct.md)
- [对象和集合初始值设定项](./object-and-collection-initializers.md)
