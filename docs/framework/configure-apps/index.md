---
title: 使用配置文件配置应用
ms.date: 03/30/2017
f1_keywords:
- AutoGeneratedOrientationPage
helpviewer_keywords:
- security configuration files
- end tags
- configuration files [.NET Framework], application
- machine configuration files
- .NET Framework application configuration, configuration files
- applications [.NET Framework], configuration files
- application configuration files, security
- application configuration files, format
- configuration files [.NET Framework]
- hosts, application
- application configuration files, machine
- ASP.NET, configuring
- configuration files [.NET Framework], security
- application configuration files, about
- application configuration files
- <runtime> element
- start tags
- configuration files [.NET Framework], machine
- configuration files [.NET Framework], format
ms.assetid: 86bd26d3-737e-4484-9782-19b17f34cd1f
ms.openlocfilehash: 28a06139275f63571d9528d075946d97a19c9f3c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912882"
---
# <a name="configuring-apps-by-using-configuration-files"></a>使用配置文件配置应用
.NET Framework 通过配置文件为开发人员和管理员提供了对应用程序运行方式的控制权和灵活性。 配置文件是可以按需要更改的 XML 文件。 管理员能够控制应用程序可以访问哪些受保护的资源，应用程序将使用哪些版本的程序集，以及远程应用程序和对象位于何处。 开发人员可以将设置置于配置文件中，从而没有必要在每次设置更改时重新编译应用程序。 本节说明可以对什么进行配置以及为什么对应用程序进行配置会有用。  
  
> [!NOTE]
> 托管代码可以使用 <xref:System.Configuration> 命名空间中的类从配置文件中读取设置，但不向这些文件写入设置。  
  
 本主题描述配置文件的语法，并提供有关三种配置文件的信息：计算机配置文件、应用程序配置文件和安全配置文件。  
  
## <a name="configuration-file-format"></a>配置文件格式  
 配置文件包含元素，它们是用来设置配置信息的逻辑数据结构。 在配置文件内，使用标记来标记元素的开头和结尾。 例如，`<runtime>` 元素包括`<runtime>`子元素`</runtime>`。 空元素将写为 `<runtime/>` 或 `<runtime></runtime>`。  
  
 与所有 XML 文件一样，配置文件中的语法区分大小写。  
  
 使用预定义特性来指定配置设置，这些特性是元素开始标记内的名称/值对。 下面的示例为 `<codeBase>` 元素指定两个特性（`version` 和 `href`），该元素指定运行时在何处可以找到程序集（有关详细信息，请参阅[指定程序集的位置](specify-assembly-location.md)）。  
  
```xml  
<codeBase version="2.0.0.0"  
          href="http://www.litwareinc.com/myAssembly.dll"/>  
```  
  
## <a name="machine-configuration-files"></a>计算机配置文件  
 计算机配置文件 Machine.config 包含应用于整个计算机的设置。 此文件位于 %*runtime install path*%\Config 目录中。 Machine.config 包含整个计算机范围内的程序集绑定、内置[远程处理信道](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dkfd3wha(v=vs.100))和 ASP.NET 的配置设置。  
  
 配置系统首先查看计算机配置文件，查找 [ **\<appSettings>** 元素](./file-schema/appsettings/index.md)，然后查看开发人员可能定义的其他配置节。 然后查看应用程序配置文件。 为使计算机配置文件可管理，最好将这些设置放在应用程序配置文件中。 但是，将这些设置放在计算机配置文件中可以使系统更易维护。 例如，如果有第三方组件，且客户端和服务器应用程序同时使用该组件，那么将该组件的设置放在一个位置更方便。 在这种情况下，计算机配置文件是存放设置的合适位置，这样就不会将相同的设置放在两个不同的文件中。  
  
> [!NOTE]
> 使用 XCOPY 部署应用程序将不会复制计算机配置文件中的设置。  
  
 若要深入了解公共语言运行时如何使用计算机配置文件进行程序集绑定，请参阅[运行时如何定位程序集](../deployment/how-the-runtime-locates-assemblies.md)。  
  
## <a name="application-configuration-files"></a>应用程序配置文件  
 应用程序配置文件包含应用特定的设置。 该文件包含公共语言运行时读取的配置设置（如程序集绑定策略、远程处理对象等）以及应用可以读取的设置。  
  
 应用程序配置文件的名称和位置取决于应用的主机，可以是下列项之一：  
  
- 可执行文件承载的应用。  
  
     这些应用具有两个配置文件：一个开发人员在开发过程中修改的源配置文件，一个随应用一起分发的输出文件。  
  
     在 Visual Studio 中进行开发时，将应用的源配置文件放置在项目目录中，并将其“复制到输出目录”属性设置为“始终复制”或“如果较新则复制”。 配置文件的名称是带 .config 扩展名的应用名。 例如，名为 myApp.exe 的应用应具有名为 myApp.exe.config 的源配置文件。  
  
     Visual Studio 会自动将源配置文件复制到已编译程序集所在的目录中，以便创建随应用程序一起部署的输出配置文件。 在某些情况下，Visual Studio 可能修改输出配置文件；有关详细信息，请参阅[重定向程序集版本](redirect-assembly-versions.md)文章中的[重定向应用级别的程序集版本](redirect-assembly-versions.md#BKMK_Redirectingassemblyversionsattheapplevel)一节。  
  
- ASP.NET 承载的应用。  
  
     有关 ASP.NET 配置文件的详细信息, 请参阅[ASP.NET 配置设置](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/b5ysx397(v=vs.100))。
  
- Internet Explorer 承载的应用。  
  
     如果 Internet Explorer 中承载的应用具有配置文件，则该文件的位置是在 `<link>` 标记中使用以下语法指定的：  
  
     \<link rel="*ConfigurationFileName*" href="*location*">  
  
     在该标记中，`location` 是指向该配置文件的 URL。 这将设置应用基。 配置文件必须位于应用所在的网站上。  
  
## <a name="security-configuration-files"></a>安全配置文件  
 安全配置文件包含有关与策略级别关联的代码组层次结构和权限集的信息。 强烈建议使用[代码访问安全性策略工具 (Caspol.exe)](../tools/caspol-exe-code-access-security-policy-tool.md) 修改安全策略，确保策略更改不会损坏安全配置文件。  
  
> [!NOTE]
> 从 .NET Framework 4 开始, 安全配置文件仅在安全策略已更改时存在。  
  
 安全配置文件位于以下位置：  
  
- 企业策略配置文件：%runtime-install-path%\Config\Enterprisesec.config  
  
- 计算机策略配置文件：%runtime-install-path%\Config\Security.config  
  
- 用户策略配置文件：%USERPROFILE%\Application data\Microsoft\CLR security config\vxx.xx\Security.config  
  
## <a name="in-this-section"></a>本节内容  
 [如何：使用 DEVPATH 查找程序集](how-to-locate-assemblies-by-using-devpath.md)  
 描述如何指示运行时在搜索程序集时使用 DEVPATH 环境变量。  
  
 [重定向程序集版本](redirect-assembly-versions.md)  
 描述如何指定程序集的位置以及要使用程序集的哪一版本。  
  
 [指定程序集的位置](specify-assembly-location.md)  
 描述如何指定运行时应搜索程序集的位置。  
  
 [配置加密类](configure-cryptography-classes.md)  
 描述如何将算法名称映射到加密类，以及如何将对象标识符映射到加密算法。  
  
 [如何：创建发布者策略](how-to-create-a-publisher-policy.md)  
 描述应当在何时以及如何添加发行者策略文件，以指定程序集重定向和基本代码设置。  
  
 [配置文件架构](./file-schema/index.md)  
 描述架构的层次结构：启动、运行时、网络和其他配置设置类型。  
  
## <a name="see-also"></a>请参阅

- [配置文件架构](./file-schema/index.md)
- [指定程序集的位置](specify-assembly-location.md)
- [重定向程序集版本](redirect-assembly-versions.md)
- [ASP.NET 网站管理](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/6hy1xzbw(v=vs.90))
- [安全策略管理](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/c1k0eed6(v=vs.100))
- [Caspol.exe（代码访问安全策略工具）](../tools/caspol-exe-code-access-security-policy-tool.md)
- [Assemblies in the Common Language Runtime](../app-domains/assemblies-in-the-common-language-runtime.md)（公共语言运行时中的程序集）
