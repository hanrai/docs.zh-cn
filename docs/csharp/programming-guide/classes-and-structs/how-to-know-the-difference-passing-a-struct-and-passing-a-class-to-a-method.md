---
title: 如何：了解向方法传递结构与类引用的区别 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- structs [C#], passing as method parameter
- passing parameters [C#], structs vs. classes
- methods [C#], passing classes vs. structs
ms.assetid: 9c1313a6-32a8-4ea7-a59f-450f66af628b
ms.openlocfilehash: 889e1f5719e094d02f0cc27256e1c430ffce0b8e
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596782"
---
# <a name="how-to-know-the-difference-between-passing-a-struct-and-passing-a-class-reference-to-a-method-c-programming-guide"></a>如何：了解向方法传递结构与类引用的区别（C# 编程指南）
下面的示例演示向方法传递[结构](../../language-reference/keywords/struct.md)和向方法传递[类](../../language-reference/keywords/class.md)实例之间的区别。 在此示例中，这两个参数（结构和类实例）都按值传递，并且两个方法都更改了参数的一个字段的值。 但是，由于传递结构和传递类实例时所传递的内容不同，所以这两个方法的结果不同。  
  
 因为结构是[值类型](../../language-reference/keywords/value-types.md)，所以[按值将结构传递](./passing-value-type-parameters.md)给方法时，该方法接收结构参数的副本并在其上运行。 该方法无法访问调用方法中的原始结构，因此无法对其进行任何更改。 它只能更改副本。  
  
 类实例是[引用类型](../../language-reference/keywords/reference-types.md)，不是值类型。 [按值将引用类型传递](./passing-reference-type-parameters.md)给方法时，方法接收对类实例的引用的副本。 也就是说，方法接收实例的地址副本，而不是实例本身的副本。 调用方法中的类实例具有地址，所调用的方法中的参数具有地址副本，且这两个地址引用同一个对象。 由于参数只包含地址副本，因此所调用的方法不能更改调用方法中类实例的地址。 但是，所调用的方法可以使用该地址来访问原始地址和副本引用的类成员。 如果所调用的方法更改了类成员，则调用方法中的原始类实例也会更改。  
  
 以下示例输出对差异进行了说明。 调用 `ClassTaker` 方法更改了类实例的 `willIChange` 字段的值，因为该方法使用参数中的地址来查找类实例的指定字段。 调用 `StructTaker` 方法不会更改调用方法中结构的 `willIChange` 字段，因为该参数的值是结构本身的副本，而不是其地址的副本。 `StructTaker` 更改副本，对 `StructTaker` 的调用完成时，副本丢失。  
  
## <a name="example"></a>示例  
 [!code-csharp[csProgGuideObjects#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#32)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../index.md)
- [类](./classes.md)
- [结构](./structs.md)
- [传递参数](./passing-parameters.md)
