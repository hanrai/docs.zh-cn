---
title: 如何：编写扩展方法 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- extending data types [Visual Basic]
- writing extension methods [Visual Basic]
- extension methods [Visual Basic]
ms.assetid: fb2739cc-958d-4ef4-a38b-214a74c93413
ms.openlocfilehash: 7a7a9d16d9f69071e9d1dacb0558f7ca92e1d21e
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68631035"
---
# <a name="how-to-write-an-extension-method-visual-basic"></a>如何：编写扩展方法 (Visual Basic)
扩展方法使你能够向现有类添加方法。 可以调用扩展方法, 就像它是该类的实例一样。

### <a name="to-define-an-extension-method"></a>定义扩展方法

1. 在 Visual Studio 中打开新的或现有的 Visual Basic 应用程序。

2. 在要在其中定义扩展方法的文件的顶部, 请包含以下 import 语句:

    ```vb
    Imports System.Runtime.CompilerServices
    ```

3. 在新应用程序或现有应用程序的模块中, 使用扩展属性开始方法定义:

    ```vb
    <Extension()>
    ```

4. 用普通方法声明方法, 但第一个参数的类型必须是要扩展的数据类型。

    ```vb
    <Extension()>
    Public Sub SubName (ByVal para1 As ExtendedType, <other parameters>)
         ' < Body of the method >
    End Sub
    ```

## <a name="example"></a>示例
 下面的示例声明了模块`StringExtensions`中的扩展方法。 第二个模块`Module1`导入`StringExtensions`并调用方法。 在调用扩展方法时, 该方法必须在范围内。 扩展方法`PrintAndPunctuate`使用一个<xref:System.String>方法来扩展类, 该方法将后跟以参数形式发送的标点符号字符串作为参数。
  
```vb
' Declarations will typically be in a separate module.
Imports System.Runtime.CompilerServices

Module StringExtensions
    <Extension()>
    Public Sub PrintAndPunctuate(ByVal aString As String,
                                 ByVal punc As String)
        Console.WriteLine(aString & punc)
    End Sub

End Module
```

```vb
' Import the module that holds the extension method you want to use,
' and call it.

Imports ConsoleApplication2.StringExtensions

Module Module1
  
    Sub Main()
        Dim example = "Hello"
        example.PrintAndPunctuate("?")
        example.PrintAndPunctuate("!!!!")
    End Sub
    
End Module
```
  
 请注意, 方法是用两个参数定义的, 并且只能用一个参数调用。 方法定义中的`aString`第一个参数绑定到`example`调用方法的实例`String` 。 示例输出如下所示：
  
 `Hello?`  
  
 `Hello!!!!`  
  
## <a name="see-also"></a>请参阅

- <xref:System.Runtime.CompilerServices.ExtensionAttribute>
- [扩展方法](./extension-methods.md)
- [Module 语句](../../../../visual-basic/language-reference/statements/module-statement.md)
- [过程参数和自变量](./procedure-parameters-and-arguments.md)
- [范围 Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
