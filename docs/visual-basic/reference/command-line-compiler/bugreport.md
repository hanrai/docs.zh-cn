---
title: -bugreport
ms.date: 03/08/2018
helpviewer_keywords:
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
ms.openlocfilehash: 75c3e5842447a8f0812d5a90d7157f7a6a496936
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962447"
---
# <a name="-bugreport"></a>-bugreport
创建一个文件, 该文件可在您提交 bug 报告时使用。  
  
## <a name="syntax"></a>语法  
  
```  
-bugreport:file  
```  
  
## <a name="arguments"></a>自变量  
  
|术语|定义|  
|---|---|  
|`file`|必需。 将包含 bug 报告的文件的名称。 如果名称包含空格, 请将文件名用引号 ("") 引起来。|  
  
## <a name="remarks"></a>备注  
 以下信息已添加到`file`:  
  
- 编译中所有源代码文件的副本。  
  
- 在编译中使用的编译器选项的列表。  
  
- 有关编译器、公共语言运行时和操作系统的版本信息。  
  
- 编译器输出（如有）。  
  
- 提示你的问题的说明。  
  
- 有关你如何思考问题的说明, 请对此进行提示。  
  
 由于中`file`包含所有源代码文件的副本, 因此你可能需要在最短的程序中再现 (怀疑) 代码缺陷。  
  
> [!IMPORTANT]
> 选项`-bugreport`将生成一个包含潜在敏感信息的文件。 这包括当前时间、编译器版本、.NET Framework 版本、OS 版本、用户名、运行编译器时所用的命令行参数、所有源代码和任何被引用程序集的二进制格式。 通过在 web.config 文件中为 ASP.NET 应用程序的服务器端编译指定命令行选项, 可以访问此选项。 若要防止出现这种情况, 请修改 Machine.config 文件, 禁止用户在服务器上进行编译。  
  
 如果此选项`-errorreport:prompt`与、 `-errorreport:queue`或`-errorreport:send`一起使用, 并且你的应用程序遇到内部编译器错误, 则中`file`的信息将发送到 Microsoft Corporation。 该信息将帮助 Microsoft 工程师找出错误的原因, 并帮助改进 Visual Basic 的下一版本。 默认情况下, 不会向 Microsoft 发送任何信息。 但是, 当你使用`-errorreport:queue`(默认情况下已启用) 编译应用程序时, 应用程序将收集其错误报告。 然后, 当计算机的管理员登录时, "错误报告系统" 会显示一个弹出窗口, 使管理员能够将自登录后发生的任何错误报告转发给 Microsoft。  
  
> [!NOTE]
> 此`/bugreport`选项在 Visual Studio 开发环境中不可用; 它仅在从命令行编译时可用。  
  
## <a name="example"></a>示例  
 下面的示例将`T2.vb`所有错误报告信息编译并放入文件`Problem.txt`中。  
  
```  
vbc -bugreport:problem.txt t2.vb  
```  
  
## <a name="see-also"></a>请参阅

- [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)
- [-debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)
- [-errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)
- [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Ws-securitypolicy 的 trustLevel 元素 (ASP.NET 设置架构)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as399f0x(v=vs.100))
