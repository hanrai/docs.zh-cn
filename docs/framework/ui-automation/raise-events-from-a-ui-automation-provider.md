---
title: 从 UI 自动化提供程序中引发事件
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, raising events
- raising UI Automation events
ms.assetid: 9fe2f01b-f7d8-49a8-a185-d4472b9976c0
ms.openlocfilehash: c973d6ddba498f4bdab4be764a4be6bff1cacf9e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966363"
---
# <a name="raise-events-from-a-ui-automation-provider"></a>从 UI 自动化提供程序中引发事件
> [!NOTE]
> 本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关的最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], 请[参阅 Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题包含演示如何从 UI 自动化提供程序中引发事件的代码示例。  
  
## <a name="example"></a>示例  
 下面的示例在自定义按钮控件的实现中引发了 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件。 该实现使 UI 自动化客户端应用程序能够模拟按钮单击。  
  
 若要避免不必要的处理，示例将检查 <xref:System.Windows.Automation.Provider.AutomationInteropProvider.ClientsAreListening%2A> 以确定是否应引发事件。  
  
 [!code-csharp[UIAProvider_snip#150](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAProvider_snip/CSharp/FragmentRoot.cs#150)]  
  
## <a name="see-also"></a>请参阅

- [UI 自动化提供程序概述](../../../docs/framework/ui-automation/ui-automation-providers-overview.md)
