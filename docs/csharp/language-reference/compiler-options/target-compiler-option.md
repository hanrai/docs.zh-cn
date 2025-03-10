---
title: -target（C# 编译器选项）
ms.date: 07/20/2015
f1_keywords:
- /target
helpviewer_keywords:
- target compiler options [C#]
- /target compiler options [C#]
- assemblies [C#], compiling
- -target compiler options [C#]
ms.assetid: a18bbd8e-bbf7-49e7-992c-717d0eb1f76f
ms.openlocfilehash: 0630639433aed4c8dfddbf0144e9802ed3f4ee73
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606450"
---
# <a name="-target-c-compiler-options"></a>-target（C# 编译器选项）
-target 编译器选项可指定为以下四种形式之一  ：  
  
 [/target:appcontainerexe](./target-appcontainerexe-compiler-option.md)  
 创建 [!INCLUDE[win8_appname_long](~/includes/win8-appname-long-md.md)]应用的 .exe 文件。  
  
 [/target:exe](./target-exe-compiler-option.md)  
 创建 .exe 文件。  
  
 [/target:library](./target-library-compiler-option.md)  
 创建代码库。  
  
 [/target:module](./target-module-compiler-option.md)  
 创建模块。  
  
 [/target:winexe](./target-winexe-compiler-option.md)  
 创建 Windows 程序。  
  
 [/target:winmdobj](./target-winmdobj-compiler-option.md)  
 创建一个 .winmdobj 中间文件。  
  
 如果不指定 -target:module，-target 会将 .NET Framework 程序集清单放入输出文件中   。 有关详细信息，请参阅[公共语言运行时中的程序集](../../../framework/app-domains/assemblies-in-the-common-language-runtime.md)和[公共特性](../../programming-guide/concepts/attributes/common-attributes.md)。  
  
 程序集清单放置在编译中的第一个 .exe 输出文件中，如果没有 .exe 输出文件，会放置在第一个 DLL 中。 例如，在以下的命令行中，清单将放置在 `1.exe` 中：  
  
```console  
csc -out:1.exe t1.cs -out:2.netmodule t2.cs  
```  
  
 编译器每次编译只创建一个程序集清单。 关于编译中所有文件的信息都放在程序集清单中。 除用 -target:module 创建的文件之外，所有输出文件都可包含程序集清单  。 在命令行生成多个输出文件时，只能创建一个程序集清单，且该清单必须放置在命令行上指定的第一个输出文件中。 无论第一个输出文件是什么（-target:exe、-target:winexe、-target:library 或 -target:module），在同一编译中生成的任何其他输出文件都必须是模块 (-target:module)      。  
  
 如果创建了一个程序集，则可以用 <xref:System.CLSCompliantAttribute> 属性指示全部或部分代码是符合 CLS 的。  
  
```csharp  
// target_clscompliant.cs  
[assembly:System.CLSCompliant(true)]   // specify assembly compliance  
  
[System.CLSCompliant(false)]   // specify compliance for an element  
public class TestClass  
{  
    public static void Main() {}  
}  
```  
  
 有关如何以编程方式设置此编译器选项的详细信息，请参阅 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## <a name="see-also"></a>请参阅

- [C# 编译器选项](./index.md)
- [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)
- [-subsystemversion（C# 编译器选项）](./subsystemversion-compiler-option.md)
