---
title: 保护异常处理
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- code security, exception handling
- security [.NET Framework], exception handling
- secure coding, exception handling
- exception handling, security
ms.assetid: 1f3da743-9742-47ff-96e6-d0dd1e9e1c19
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 95dbaddc59a80b4f499a629dd00a52be678b4665
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69910876"
---
# <a name="securing-exception-handling"></a>保护异常处理
在 Visual C++和 Visual Basic 中, 堆栈中的一个筛选器表达式将在任何**finally**语句之前运行。 与该筛选器相关联的**catch**块在**finally**语句之后运行。 有关详细信息, 请参阅[使用用户筛选的异常](../../standard/exceptions/using-user-filtered-exception-handlers.md)。 本部分将介绍此顺序的安全隐患。 请考虑以下伪代码示例, 该示例演示 filter 语句和**finally**语句的运行顺序。  
  
```cpp  
void Main()   
{  
    try   
    {  
        Sub();  
    }   
    except (Filter())   
    {  
        Console.WriteLine("catch");  
    }  
}  
bool Filter () {  
    Console.WriteLine("filter");  
    return true;  
}  
void Sub()   
{  
    try   
    {  
        Console.WriteLine("throw");  
        throw new Exception();  
    }   
    finally   
    {  
        Console.WriteLine("finally");  
    }  
}                        
```  
  
 此代码将打印以下代码。  
  
```  
Throw  
Filter  
Finally  
Catch  
```  
  
 该筛选器在**finally**语句之前运行, 因此, 在执行其他代码的情况下, 可能会发生状态更改的任何内容引入安全问题。 例如:  
  
```cpp  
try   
{  
    Alter_Security_State();  
    // This means changing anything (state variables,  
    // switching unmanaged context, impersonation, and   
    // so on) that could be exploited if malicious   
    // code ran before state is restored.  
    Do_some_work();  
}   
finally   
{  
    Restore_Security_State();  
    // This simply restores the state change above.  
}  
```  
  
 此伪代码允许堆栈上较高的筛选器运行任意代码。 具有类似效果的其他操作示例是对其他标识的临时模拟、设置跳过某些安全检查的内部标志或更改与线程关联的区域性。 建议的解决方案是引入异常处理程序, 以将代码的更改从调用方的筛选器块隔离到线程状态。 但是, 必须正确地引入异常处理程序, 否则不会解决此问题。 下面的示例将切换 UI 区域性, 但任何类型的线程状态更改都可能会以同样的方式公开。  
  
```cpp  
YourObject.YourMethod()  
{  
   CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
   try {  
      Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
      // Do something that throws an exception.  
}  
   finally {  
      Thread.CurrentThread.CurrentUICulture = saveCulture;  
   }  
}  
```  
  
```vb  
Public Class UserCode  
   Public Shared Sub Main()  
      Try  
         Dim obj As YourObject = new YourObject  
         obj.YourMethod()  
      Catch e As Exception When FilterFunc  
         Console.WriteLine("An error occurred: '{0}'", e)  
         Console.WriteLine("Current Culture: {0}",   
Thread.CurrentThread.CurrentUICulture)  
      End Try  
   End Sub  
  
   Public Function FilterFunc As Boolean  
      Console.WriteLine("Current Culture: {0}", Thread.CurrentThread.CurrentUICulture)  
      Return True  
   End Sub  
  
End Class  
```  
  
 在这种情况下, 正确的修复方法是在**try**/**catch**块中包装现有**try**/**finally**块。 只需将**catch throw**子句引入现有**try**/**finally**块中, 就不能解决问题, 如以下示例中所示。  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
  
    try   
    {  
        Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
        // Do something that throws an exception.  
    }  
    catch { throw; }  
    finally   
    {  
        Thread.CurrentThread.CurrentUICulture = saveCulture;  
    }  
}  
```  
  
 这并不能解决此问题,因为在`FilterFunc`获取控件之前, finally 语句尚未运行。  
  
 下面的示例通过确保在将异常提供给调用方的异常筛选器块之前执行了**finally**子句来解决此问题。  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
    try    
    {  
        try   
        {  
            Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
            // Do something that throws an exception.  
        }  
        finally   
        {  
            Thread.CurrentThread.CurrentUICulture = saveCulture;  
        }  
    }  
    catch { throw; }  
}  
```  
  
## <a name="see-also"></a>请参阅

- [安全编码准则](../../standard/security/secure-coding-guidelines.md)
