---
title: 指定程序集的位置
ms.date: 03/30/2017
helpviewer_keywords:
- configuration [.NET Framework], applications
- application configuration [.NET Framework]
- assemblies [.NET Framework], specifying location
ms.assetid: 1cb92bd7-6bab-44cf-8fd3-36303ce84fea
ms.openlocfilehash: 43cd1d0edbb607f69f27661aae3372e93564b3b7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69932339"
---
# <a name="specifying-an-assemblys-location"></a>指定程序集的位置
可以通过两种方法来指定程序集的位置:  
  
- 使用 codeBase [ >元素。\<](./file-schema/runtime/codebase-element.md)  
  
- 使用探测[ >元素。\<](./file-schema/runtime/probing-element.md)  
  
 你还可以使用[.NET Framework 配置工具 (mscorcfg.msc)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/2bc0cxhc(v=vs.100))来指定程序集位置或指定公共语言运行时用于探测程序集的位置。  
  
## <a name="using-the-codebase-element"></a>\<使用 codeBase > 元素  
 只能在计算机配置或同时重定向程序集版本的发行者策略文件中使用 **\<codeBase >** 元素。 当运行时确定要使用的程序集版本时, 它将从确定版本的文件应用基本代码设置。 如果未指定任何代码库, 则运行时以正常方式探测程序集。 有关详细信息, 请参阅[运行时如何定位程序集](../deployment/how-the-runtime-locates-assemblies.md)。  
  
 下面的示例演示如何指定程序集的位置。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
       <dependentAssembly>  
         <assemblyIdentity name="myAssembly"  
                           publicKeyToken="32ab4ba45e0a69a1"  
                           culture="en-us" />  
         <codeBase version="2.0.0.0"  
                   href="http://www.litwareinc.com/myAssembly.dll"/>  
       </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 对于所有具有强名称的程序集, **version**特性都是必需的, 但对于不具有强名称的程序集, 应忽略该特性。 **
          \<Base>** 元素需要 **href** 属性。 不能在 **\<codeBase >** 元素中指定版本范围。  
  
> [!NOTE]
> 如果要为不具有强名称的程序集提供基本代码提示, 则提示必须指向应用程序基目录或应用程序基目录的子目录。  
  
## <a name="using-the-probing-element"></a>\<使用探测 > 元素  
 运行时通过探测来查找没有代码库的程序集。 有关探测的详细信息, 请参阅[运行时如何定位程序集](../deployment/how-the-runtime-locates-assemblies.md)。  
  
 您可以使用应用程序配置文件中的[ \<探测 >](./file-schema/runtime/probing-element.md)元素指定运行时在查找程序集时应搜索的子目录。 下面的示例演示如何指定运行时应搜索的目录。  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <probing privatePath="bin;bin2\subbin;bin3"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 **PrivatePath**属性包含运行时应搜索程序集的目录。 如果应用程序位于 C:\Program Files\MyApp, 则运行时将查找未在 C:\Program Files\MyApp\Bin、C:\Program Files\MyApp\Bin2\Subbin 和 C:\Program Files\MyApp\Bin3. 中指定基本代码的程序集。 在**privatePath**中指定的目录必须是应用程序基目录的子目录。  
  
## <a name="see-also"></a>请参阅

- [Assemblies in the Common Language Runtime](../app-domains/assemblies-in-the-common-language-runtime.md)（公共语言运行时中的程序集）
- [使用程序集编程](../app-domains/programming-with-assemblies.md)
- [运行时如何定位程序集](../deployment/how-the-runtime-locates-assemblies.md)
- [使用配置文件配置应用程序](index.md)
