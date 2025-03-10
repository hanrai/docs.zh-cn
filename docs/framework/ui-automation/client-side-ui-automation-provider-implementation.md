---
title: 客户端 UI 自动化提供程序的实现
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, client-side provider implementation
- client-side UI Automation provider, implementation
- provider implementation, UI Automation
ms.assetid: 3584c0a1-9cd0-4968-8b63-b06390890ef6
ms.openlocfilehash: 9079dfa03ab81bfa6875e43bfa8a6e5351e0a35d
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015106"
---
# <a name="client-side-ui-automation-provider-implementation"></a>客户端 UI 自动化提供程序的实现
> [!NOTE]
> 本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关的最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], 请[参阅 Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 Microsoft 操作系统[!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)]中使用几种不同的框架, 包括[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]、 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]和[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]。 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 向客户公开有关 UI 元素的信息。 但是， [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 本身并不了解存在于这些框架中的不同类型的控件以及从中提取信息所需的技术。 而是将此任务留给称为提供程序的对象。 一个提供程序从特定控件中提取信息，并将该信息传递给 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，后者随后以一致的方式将其呈现给客户端。  
  
 提供程序可以存在于服务器端或客户端上。 服务器端提供程序由控件本身实现。 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 元素实现提供程序，正如可以在考虑到 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的情况下写入第三方控件一样。  
  
 但较旧的控件（例如 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] 中的控件）不直接支持 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]。 这些控件都将改为由存在于客户端进程中的提供程序提供，并且使用跨进程通信获取有关控件的信息；例如，通过监视在窗口与控件之间来回的消息。 此类客户端提供程序有时称为代理。  
  
 [!INCLUDE[TLA2#tla_winvista](../../../includes/tla2sharptla-winvista-md.md)]为标准[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]控件和 Windows 窗体控件提供提供程序。 此外, 回退提供程序为任何不[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]由另一个服务器端提供程序或代理提供但具有 Microsoft Active Accessibility 实现的控件提供部分支持。 所有这样的提供程序均已自动加载，并且可供客户端应用程序使用。  
  
 有关对[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]和 Windows 窗体控件的支持的详细信息, 请参阅[UI 自动化对标准控件的支持](../../../docs/framework/ui-automation/ui-automation-support-for-standard-controls.md)。  
  
 应用程序还可以注册其他客户端提供程序。  
  
<a name="Distributing_Client-Side_Providers"></a>   
## <a name="distributing-client-side-providers"></a>分布客户端提供程序  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 预期在托管代码程序集中查找客户端提供程序。 此程序集中命名空间的名称应与程序集名称相同。 例如，名为 ContosoProxies.dll 的程序集将包含 ContosoProxies 命名空间。 在命名空间内创建一个 <xref:UIAutomationClientsideProviders.UIAutomationClientSideProviders> 类。 在静态 <xref:UIAutomationClientsideProviders.UIAutomationClientSideProviders.ClientSideProviderDescriptionTable> 字段的实现中，创建一个描述提供程序的 <xref:System.Windows.Automation.ClientSideProviderDescription> 结构数组。  
  
<a name="Registering_and_Configuring_Client-Side_Providers"></a>   
## <a name="registering-and-configuring-client-side-providers"></a>注册并配置客户端提供程序  
 动态链接库 (DLL) 中的客户端提供程序通过调用<xref:System.Windows.Automation.ClientSettings.RegisterClientSideProviderAssembly%2A>加载。 客户端应用程序不需要任何进一步的操作即可使用提供程序。  
  
 在客户端自己的代码中实现的提供程序通过使用 <xref:System.Windows.Automation.ClientSettings.RegisterClientSideProviders%2A>注册。 此方法将 <xref:System.Windows.Automation.ClientSideProviderDescription> 结构数组作为参数，每个结构均指定以下属性：  
  
- 创建提供程序对象的回调函数。  
  
- 提供程序将提供的控件的类名。  
  
- 提供程序将提供的应用程序（通常为可执行文件的完整名称）的映像名称。  
  
- 控制如何将类名与在目标应用程序中找到的窗口类进行匹配的标志。  
  
 最后两个参数为可选。 当客户端需要为不同的应用程序使用不同的提供程序时，它可能会指定目标应用程序的映像名称。 例如，客户端可能会为支持“多视图”模式的已知应用程序中的 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 列表视图控件使用一个提供程序，为不支持“多视图”模式的另一个已知应用程序中的类似控件使用另一个提供程序。  
  
## <a name="see-also"></a>请参阅

- [创建客户端 UI 自动化提供程序](../../../docs/framework/ui-automation/create-a-client-side-ui-automation-provider.md)
- [在客户端应用程序中实现 UI 自动化提供程序](../../../docs/framework/ui-automation/implement-ui-automation-providers-in-a-client-application.md)
