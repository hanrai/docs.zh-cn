---
title: 建议的文档注释标记 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- XML [C#], tags
- XML documentation [C#], tags
ms.assetid: 6e98f7a9-38f4-4d74-b644-1ff1b23320fd
ms.openlocfilehash: ac8629dacbb8c1fde1f55468e5d2aeaf78cfe017
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69928027"
---
# <a name="recommended-tags-for-documentation-comments-c-programming-guide"></a>建议的文档注释标记（C# 编程指南）
C# 编译器处理代码中的文档注释，并在文件中将其设置为 XML 格式，该文件的名称通过 /doc 命令行选项指定  。 若要基于编译器生成的文件创建最终文档，可以创建一个自定义工具，也可以使用 [DocFX](https://dotnet.github.io/docfx/) 或 [Sandcastle](https://github.com/EWSoftware/SHFB) 等工具。  
  
 在类型和类型成员等代码构造中处理标记。  
  
> [!NOTE]
> 不可对命名空间应用文档注释。  
  
 编译器将处理属于有效 XML 形式的任何标记。 下列标记提供用户文档的中常用功能。  
  
## <a name="tags"></a>Tags  
  
||||  
|---|---|---|  
|[\<c>](./code-inline.md)|[\<para>](./para.md)|[\<see>](./see.md)*|  
|[\<code>](./code.md)|[\<param>](./param.md)*|[\<seealso>](./seealso.md)*|  
|[\<example>](./example.md)|[\<paramref>](./paramref.md)|[\<summary>](./summary.md)|  
|[\<exception>](./exception.md)*|[\<permission>](./permission.md)*|[\<typeparam>](./typeparam.md)*|  
|[\<include>](./include.md)*|[\<remarks>](./remarks.md)|[\<typeparamref>](./typeparamref.md)|  
|[\<list>](./list.md)|[\<returns>](./returns.md)|[\<value>](./value.md)|  
  
 （* 表示编译器验证语法。）  
  
 如果希望在文档注释的文本中显示尖括号，请使用 `<` 和 `>` 的 HTML 编码，分别为 `&lt;` 和 `&gt;`。 下面的示例对此编码进行了演示：
  
```csharp  
/// <summary>
/// This property always returns a value &lt; 1.
/// </summary>
```
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../index.md)
- [/doc（C# 编译器选项）](../../language-reference/compiler-options/doc-compiler-option.md)
- [XML 文档注释](./index.md)
