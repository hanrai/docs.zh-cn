---
title: 中间具体化 (C#)
ms.date: 07/20/2015
ms.assetid: 7922d38f-5044-41cf-8e17-7173d6553a5e
ms.openlocfilehash: 273cd68b9714287f259e763c9b7c534aac1931e6
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69592131"
---
# <a name="intermediate-materialization-c"></a>中间具体化 (C#)
有时，稍不小心就会导致查询中的集合过早具体化，从而显著改变应用程序的内存和性能配置文件。 有些标准查询运算符会在生成单个元素之前导致其源集合具体化。 例如，<xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=nameWithType> 首先循环访问其整个源集合，然后对所有项排序，最后生成第一项。 这意味着获取排序集合中的第一项需要高开销；其后的每一项不需要高开销。 这样做很有意义：该查询运算符将不可能以其他方式操作。  
  
## <a name="example"></a>示例  
 本示例改自上一示例。 `AppendString` 方法在循环访问源之前调用 <xref:System.Linq.Enumerable.ToList%2A>。 这将导致具体化。  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source >{0}<", str);  
            yield return str.ToUpper();  
        }  
    }  
  
    public static IEnumerable<string>  
      AppendString(this IEnumerable<string> source, string stringToAppend)  
    {  
        // the following statement materializes the source collection in a List<T>  
        // before iterating through it  
        foreach (string str in source.ToList())  
        {  
            Console.WriteLine("AppendString: source >{0}<", str);  
            yield return str + stringToAppend;  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        IEnumerable<string> q1 =  
            from s in stringArray.ConvertCollectionToUpperCase()  
            select s;  
  
        IEnumerable<string> q2 =  
            from s in q1.AppendString("!!!")  
            select s;  
  
        foreach (string str in q2)  
        {  
            Console.WriteLine("Main: str >{0}<", str);  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
 该示例产生下面的输出：  
  
```  
ToUpper: source >abc<  
ToUpper: source >def<  
ToUpper: source >ghi<  
AppendString: source >ABC<  
Main: str >ABC!!!<  
  
AppendString: source >DEF<  
Main: str >DEF!!!<  
  
AppendString: source >GHI<  
Main: str >GHI!!!<  
```  
  
 在此示例中，您可以看到，对 <xref:System.Linq.Enumerable.ToList%2A> 的调用会导致 `AppendString` 生成第一项之前枚举其整个源。 如果源是一个大数组，这将显著改变应用程序的内存配置文件。  
  
 标准查询运算符也可以链接在一起。 本教程的最后一个主题将对此进行说明。  
  
- [将标准查询运算符链接在一起 (C#)](./chaining-standard-query-operators-together.md)  
  
## <a name="see-also"></a>请参阅

- [教程：将查询链接在一起 (C#)](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)
