---
title: 如何：为枚举创建新方法 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [C#]
- extension methods [C#], for enums
- enum extensibility [C#]
ms.assetid: 100106f9-1e54-462c-8ebe-3892fe23b6eb
ms.openlocfilehash: 99a2005e1a64fa214776145a903341fb162f0633
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597043"
---
# <a name="how-to-create-a-new-method-for-an-enumeration-c-programming-guide"></a>如何：为枚举创建新方法（C# 编程指南）
可使用扩展方法添加特定于某个特定枚举类型的功能。  
  
## <a name="example"></a>示例  
 在下面的示例中，`Grades` 枚举表示学生可能在班里收到的字母等级分。 该示例将一个名为 `Passing` 的扩展方法添加到 `Grades` 类型中，以便该类型的每个实例现在都“知道”它是否表示合格的等级分。  
  
 [!code-csharp[csProgGuideExtensionMethods#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#2)]  
  
 请注意，`Extensions` 类还包含一个动态更新的静态变量，并且扩展方法的返回值反映了该变量的当前值。 这表明在幕后，将在定义扩展方法的静态类上直接调用这些方法。  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../index.md)
- [扩展方法](./extension-methods.md)
