---
title: .NET Framework 概述
ms.date: 03/30/2017
helpviewer_keywords:
- application development [.NET Framework]
- common language runtime
- common language runtime, about
- common language runtime, overview
ms.assetid: 29848c96-fc36-462d-8072-ba223a40b697
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 46dd9c0c1f9f5759bc9160aadeb0538b5403fb52
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917973"
---
# <a name="overview-of-the-net-framework"></a>.NET Framework 概述

.NET Framework 是一种技术，该技术支持生成和运行下一代应用和 XML Web Services。 .NET Framework 旨在实现下列目标：

- 提供一个一致的面向对象的编程环境，而无论对象代码是在本地存储和执行，还是在本地执行但在 Internet 上分布，或者是在远程执行的。

- 提供一个将软件部署和版本控制冲突最小化的代码执行环境。

- 提供一个可提高代码（包括由未知的或不完全受信任的第三方创建的代码）执行安全性的代码执行环境。

- 提供一个可消除脚本环境或解释环境的性能问题的代码执行环境。

- 使开发人员的经验在面对类型大不相同的应用（如基于 Windows 的应用和基于 Web 的应用）时保持一致。

- 按照工业标准生成所有通信，确保基于 .NET Framework 的代码可与任何其他代码集成。

> [!NOTE]
> 有关适用于用户和开发人员的 .NET Framework 的常规说明，请参阅[入门](../../../docs/framework/get-started/index.md)。

.NET Framework 包括公共语言运行时 (CLR) 和 .NET Framework 类库。 公共语言运行时是 .NET Framework 的基础。 可将运行时看作一个在执行时管理代码的代理，它提供内存管理、线程管理和远程处理等核心服务，并且还强制实施严格的类型安全以及可提高安全性和可靠性的其他形式的代码准确性。 事实上，代码管理的概念是运行时的基本原则。 以运行时为目标的代码称为托管代码，而不以运行时为目标的代码称为非托管代码。 类库是一个综合性的面向对象的可重用类型集合，可使用它来开发多种应用，这些应用程序包括传统的命令行或图形用户界面 (GUI) 应用，还包括基于 ASP.NET 提供的最新创新的应用（如 Web 窗体和 XML Web Services）。

.NET Framework 可由非托管组件承载，这些组件将公共语言运行时加载到它们的进程中并启动托管代码的执行，从而创建一个同时利用托管和非托管功能的软件环境。 .NET Framework 不但提供若干个运行时主机，而且还支持第三方运行时主机的开发。

例如，ASP.NET 承载运行时以为托管代码提供可伸缩的服务器端环境。 ASP.NET 直接使用运行时以启用 ASP.NET 应用和 XML Web Services（本主题稍后将对这两者进行讨论）。

Internet Explorer 是承载运行时（以 MIME 类型扩展的形式）的非托管应用的一个示例。 使用 Internet Explorer 承载运行时使您能够在 HTML 文档中嵌入托管组件或 Windows 窗体控件。 以这种方式承载运行时可使托管移动代码成为可能，不过它需要进行只有托管代码才能提供的重大改进（如不完全受信任的执行和独立的文件存储）。

下面的插图显示公共语言运行时和类库与应用之间以及与整个系统之间的关系。 该插图还显示托管代码如何在更大的结构内运行。

![显示托管代码如何在大型体系结构中运行的屏幕截图。](./media/overview/language-runtime-class-library-relationship.gif)

以下各节更详细地描述 .NET Framework 的主要功能。

## <a name="features-of-the-common-language-runtime"></a>公共语言运行时的功能

公共语言运行时管理内存、线程执行、代码执行、代码安全验证、编译以及其他系统服务。 这些功能是在公共语言运行时上运行的托管代码所固有的。

至于安全性，取决于包括托管组件的来源（如 Internet、企业网络或本地计算机）在内的一些因素，托管组件被赋予不同程度的信任。 这意味着即使用在同一活动应用中，托管组件既可能能够执行文件访问操作、注册表访问操作或其他须小心使用的功能，也可能不能够执行这些功能。

运行时还通过实现称为常规类型系统 (CTS) 的严格类型验证和代码验证基础结构来加强代码可靠性。 CTS 确保所有托管代码都是可以自我描述的。 各种 Microsoft 编译器和第三方语言编译器都可生成符合 CTS 的托管代码。 这意味着托管代码可在严格实施类型保真和类型安全的同时使用其他托管类型和实例。

此外，运行时的托管环境还消除了许多常见的软件问题。 例如，运行时自动处理对象布局并管理对对象的引用，在不再使用它们时将它们释放。 这种自动内存管理解决了两个最常见的应用错误：内存泄漏和无效内存引用。

运行时还提高了开发人员的工作效率。 例如，程序员用他们选择的开发语言编写应用，却仍能充分利用其他开发人员用其他语言编写的运行时、类库和组件。 任何选择以运行时为目标的编译器供应商都可以这样做。 以 .NET Framework 为目标的语言编译器使得用该语言编写的现有代码可以使用 .NET Framework 的功能，这大大减轻了现有应用的迁移过程的工作负担。

尽管运行时是为未来的软件设计的，但是它也支持现在和以前的软件。 托管和非托管代码之间的互操作性使开发人员能够继续使用所需的 COM 组件和 DLL。

运行时旨在增强性能。 尽管公共语言运行时提供许多标准运行时服务，但是它从不解释托管代码。 一种称为实时 (JIT) 编译的功能使所有托管代码能够以它在其上执行的系统的本机语言运行。 同时，内存管理器排除了出现零碎内存的可能性，并增大了内存引用区域以进一步提高性能。

最后，运行时可由高性能的服务器端应用（如 Microsoft SQL Server 和 Internet Information Services (IIS)）承载。 此基础结构使您在享受支持运行时承载的行业最佳企业服务器的优越性能的同时，能够使用托管代码编写业务逻辑。

## <a name="net-framework-class-library"></a>.NET Framework Class Library — .NET Framework 类库

.NET Framework 类库是一个与公共语言运行时紧密集成的可重用的类型集合。 该类库是面向对象的，并提供某些类型，可供你自己的托管代码从中派生功能。 这不但使 .NET Framework 类型易于使用，而且还减少了学习 .NET Framework 的新功能所需要的时间。 此外，第三方组件与 .NET Framework 中的类无缝集成。

例如，.NET Framework 集合类实现一组用于开发自己的集合类的接口。 你的集合类与 .NET Framework 中的类无缝地混合。

正如您对面向对象的类库所希望的那样，.NET Framework 类型使您能够完成一系列常见编程任务（包括诸如字符串管理、数据收集、数据库连接以及文件访问等任务）。 除这些常规任务之外，类库还包括支持多种专用开发方案的类型。 使用 .NET Framework 开发下列类型的应用和服务：

- Console 应用。 请参阅[生成控制台应用程序](../../standard/building-console-apps.md)。

- Windows GUI 应用（Windows 窗体）。 请参阅 [Windows 窗体](../../../docs/framework/winforms/index.md)。

- Windows Presentation Foundation (WPF) 应用。 请参阅 [Windows Presentation Foundation](../../../docs/framework/wpf/index.md)。

- ASP.NET 应用。 请参阅[使用 ASP.NET 的 Web 应用程序](../../../docs/framework/develop-web-apps-with-aspnet.md)。

- Windows 服务。 请参阅 [Windows 服务应用程序简介](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)。

- 使用 Windows Communication Foundation (WCF) 的面向服务的应用。 请参阅[使用 WCF 的面向服务的应用程序](../../../docs/framework/wcf/index.md)。

- 使用 Windows Workflow Foundation (WF) 的启用工作流程的应用。 请参阅[Windows Workflow Foundation](../windows-workflow-foundation/index.md)。

Windows 窗体类是一组综合性的可重用的类型，它们大大简化了 Windows GUI 的开发。 如果要编写 ASP.NET Web 窗体应用，可使用 Web 窗体类。

## <a name="see-also"></a>请参阅

- [系统要求](../../../docs/framework/get-started/system-requirements.md)
- [安装指南](../../../docs/framework/install/index.md)
- [开发指南](../../../docs/framework/development-guide.md)
- [工具](../../../docs/framework/tools/index.md)
- [.NET 示例和教程](../../samples-and-tutorials/index.md)
- [.NET Framework 类库](https://go.microsoft.com/fwlink/?LinkID=227195)
