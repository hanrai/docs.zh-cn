---
title: 如何：联接不同文件的内容 (LINQ) (C#)
ms.date: 06/27/2018
ms.assetid: aa2d12a6-70a9-492f-a6db-b2b850d46811
ms.openlocfilehash: 14f9c9917aedbc0beeeddae789b835613d1badc8
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593157"
---
# <a name="how-to-join-content-from-dissimilar-files-linq-c"></a>如何：联接不同文件的内容 (LINQ) (C#)

本示例演示如何联接两个逗号分隔文件中的数据，这两个文件共享一个用作匹配键的公共值。 如果需要合并来自两个电子表格的数据，或者从一个电子表格和具有另一种格式的文件合并到一个新文件时，此技术很有用。 可以修改此示例以用于任何类型的结构化文本。  
  
## <a name="to-create-the-data-files"></a>创建数据文件
  
1. 将以下行复制到名为 scores.csv 的文件，并将文件保存到项目文件夹  。 此文件表示电子表格数据。 第 1 列是学生的 ID，第 2 至 5 列是测验分数。  
  
    ```  
    111, 97, 92, 81, 60  
    112, 75, 84, 91, 39  
    113, 88, 94, 65, 91  
    114, 97, 89, 85, 82  
    115, 35, 72, 91, 70  
    116, 99, 86, 90, 94  
    117, 93, 92, 80, 87  
    118, 92, 90, 83, 78  
    119, 68, 79, 88, 92  
    120, 99, 82, 81, 79  
    121, 96, 85, 91, 60  
    122, 94, 92, 91, 91  
    ```  
  
2. 将以下行复制到名为 names.csv 的文件，并将文件保存到项目文件夹  。 此文件表示电子表格，其中包含学生的姓氏、名字和学生 ID。  
  
    ```  
    Omelchenko,Svetlana,111  
    O'Donnell,Claire,112  
    Mortensen,Sven,113  
    Garcia,Cesar,114  
    Garcia,Debra,115  
    Fakhouri,Fadi,116  
    Feng,Hanying,117  
    Garcia,Hugo,118  
    Tucker,Lance,119  
    Adams,Terry,120  
    Zabokritski,Eugene,121  
    Tucker,Michael,122  
    ```  
  
## <a name="example"></a>示例  

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class JoinStrings  
{  
    static void Main()  
    {  
        // Join content from dissimilar files that contain  
        // related information. File names.csv contains the student  
        // name plus an ID number. File scores.csv contains the ID   
        // and a set of four test scores. The following query joins  
        // the scores to the student names by using ID as a  
        // matching key.  
  
        string[] names = System.IO.File.ReadAllLines(@"../../../names.csv");  
        string[] scores = System.IO.File.ReadAllLines(@"../../../scores.csv");  
  
        // Name:    Last[0],       First[1],  ID[2]  
        //          Omelchenko,    Svetlana,  11  
        // Score:   StudentID[0],  Exam1[1]   Exam2[2],  Exam3[3],  Exam4[4]  
        //          111,           97,        92,        81,        60  
  
        // This query joins two dissimilar spreadsheets based on common ID value.  
        // Multiple from clauses are used instead of a join clause  
        // in order to store results of id.Split.  
        IEnumerable<string> scoreQuery1 =  
            from name in names  
            let nameFields = name.Split(',')  
            from id in scores  
            let scoreFields = id.Split(',')  
            where Convert.ToInt32(nameFields[2]) == Convert.ToInt32(scoreFields[0])
            select nameFields[0] + "," + scoreFields[1] + "," + scoreFields[2]   
                   + "," + scoreFields[3] + "," + scoreFields[4];  
  
        // Pass a query variable to a method and execute it  
        // in the method. The query itself is unchanged.  
        OutputQueryResults(scoreQuery1, "Merge two spreadsheets:");  
  
        // Keep console window open in debug mode.  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
  
    static void OutputQueryResults(IEnumerable<string> query, string message)  
    {  
        Console.WriteLine(System.Environment.NewLine + message);  
        foreach (string item in query)  
        {  
            Console.WriteLine(item);  
        }  
        Console.WriteLine("{0} total names in list", query.Count());  
    }  
}  
/* Output:  
Merge two spreadsheets:
Omelchenko, 97, 92, 81, 60
O'Donnell, 75, 84, 91, 39
Mortensen, 88, 94, 65, 91
Garcia, 97, 89, 85, 82
Garcia, 35, 72, 91, 70
Fakhouri, 99, 86, 90, 94
Feng, 93, 92, 80, 87
Garcia, 92, 90, 83, 78
Tucker, 68, 79, 88, 92
Adams, 99, 82, 81, 79
Zabokritski, 96, 85, 91, 60
Tucker, 94, 92, 91, 91
12 total names in list
 */  
```

## <a name="see-also"></a>请参阅

- [LINQ 和字符串 (C#)](./linq-and-strings.md)
- [LINQ 和文件目录 (C#)](./linq-and-file-directories.md)
