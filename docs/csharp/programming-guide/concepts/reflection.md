---
title: 反射 (C#)
ms.date: 07/20/2015
ms.assetid: f80a2362-953b-4e8e-9759-cd5f334190d4
ms.openlocfilehash: 9b4322d83ad43cd3e49647df49c15bb5c917e1be
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924093"
---
# <a name="reflection-c"></a>反射 (C#)
反射提供描述程序集、模块和类型的对象（<xref:System.Type> 类型）。 可以使用反射动态地创建类型的实例，将类型绑定到现有对象，或从现有对象中获取类型，然后调用其方法或访问其字段和属性。 如果代码中使用了特性，可以利用反射来访问它们。 有关更多信息，请参阅[特性](../../../standard/attributes/index.md)。  
  
 下面一个简单的反射示例，使用静态方法 `GetType`被 `Object` 基类的所有类型继承）以获取变量类型：  
  
```csharp  
// Using GetType to obtain type information:  
int i = 42;  
System.Type type = i.GetType();  
System.Console.WriteLine(type);  
```  
  
 输出为：  
  
 `System.Int32`  
  
 下面的示例使用反射获取已加载的程序集的完整名称。  
  
```csharp  
// Using Reflection to get information of an Assembly:  
System.Reflection.Assembly info = typeof(System.Int32).Assembly;  
System.Console.WriteLine(info);  
```  
  
 输出为：  
  
 `mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`  
  
> [!NOTE]
> C# 关键字 `protected` 和 `internal` 在 IL 中没有任何意义，且不会用于反射 API 中。 在 IL 中对应的术语为“系列”  和“程序集”  。 若要标识 `internal` 使用反射的方法，请使用 <xref:System.Reflection.MethodBase.IsAssembly%2A> 属性。 若要标识 `protected internal` 方法，请使用 <xref:System.Reflection.MethodBase.IsFamilyOrAssembly%2A>。  
  
## <a name="reflection-overview"></a>反射概述  
 反射在以下情况下很有用：  
  
- 需要访问程序元数据中的特性时。 有关详细信息，请参阅[检索存储在特性中的信息](../../../standard/attributes/retrieving-information-stored-in-attributes.md)。  
  
- 检查和实例化程序集中的类型。  
  
- 在运行时构建新类型。 使用 <xref:System.Reflection.Emit> 中的类。  
  
- 执行后期绑定，访问在运行时创建的类型上的方法。 请参阅主题 [Dynamically Loading and Using Types](../../../framework/reflection-and-codedom/dynamically-loading-and-using-types.md)（动态加载和使用类型）。  
  
## <a name="related-sections"></a>相关章节  
 更多相关信息：  
  
- [反射](../../../framework/reflection-and-codedom/reflection.md)  
  
- [查看类型信息](../../../framework/reflection-and-codedom/viewing-type-information.md)  
  
- [反射类型和泛型类型](../../../framework/reflection-and-codedom/reflection-and-generic-types.md)  
  
- <xref:System.Reflection.Emit>  
  
- [检索存储在特性中的信息](../../../standard/attributes/retrieving-information-stored-in-attributes.md)  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../index.md)
- [Assemblies in the Common Language Runtime](../../../framework/app-domains/assemblies-in-the-common-language-runtime.md)（公共语言运行时中的程序集）
