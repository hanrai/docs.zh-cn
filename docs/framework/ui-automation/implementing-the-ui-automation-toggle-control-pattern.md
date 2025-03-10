---
title: 实现 UI 自动化 Toggle 控件模式
ms.date: 03/30/2017
helpviewer_keywords:
- Toggle control pattern
- control patterns, Toggle
- UI Automation, Toggle control pattern
ms.assetid: 3cfe875f-b0c0-413d-9703-5f14e6a1a30e
ms.openlocfilehash: 2293dc77369ecf019bd1093808135eeefd99c115
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69932067"
---
# <a name="implementing-the-ui-automation-toggle-control-pattern"></a>实现 UI 自动化 Toggle 控件模式
> [!NOTE]
> 本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关的最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], 请[参阅 Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍实现 <xref:System.Windows.Automation.Provider.IToggleProvider>的准则和约定，包括有关方法和属性的信息。 本主题的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.TogglePattern> 控件模式用于支持可在一组状态间进行循环，并在设置后保持其状态的控件。 有关实现此控件模式的控件示例，请参阅 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>实现准则和约定  
 在实现“切换”控件模式时，请注意以下准则和约定：  
  
- 不保持激活时的状态的控件（如按钮、工具栏按钮和超链接）则必须实现 <xref:System.Windows.Automation.Provider.IInvokeProvider> 。  
  
- 控件必须按以下顺序在其 <xref:System.Windows.Automation.ToggleState> 间进行循环： <xref:System.Windows.Automation.ToggleState.On>、 <xref:System.Windows.Automation.ToggleState.Off> ，以及 <xref:System.Windows.Automation.ToggleState.Indeterminate>（如果支持）。  
  
- <xref:System.Windows.Automation.TogglePattern> 不提供 SetState(newState) 方法，因为不按相应的 <xref:System.Windows.Automation.ToggleState> 顺序进行循环即直接设置三态复选框存在问题。  
  
- 单选按钮控件不会实现 <xref:System.Windows.Automation.Provider.IToggleProvider>，因为它不能在其有效状态间进行循环。  
  
<a name="Required_Members_for_IToggleProvider"></a>   
## <a name="required-members-for-itoggleprovider"></a>IToggleProvider 必需的成员  
 实现 <xref:System.Windows.Automation.Provider.IToggleProvider>需要以下属性和方法。  
  
|必需的成员|成员类型|说明|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.TogglePattern.Toggle%2A>|方法|无|  
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty>|属性|无|  
  
 没有与此控件模式关联的事件。  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>Exceptions  
 没有与此控件模式关联的异常。  
  
## <a name="see-also"></a>请参阅

- [UI 自动化控件模式概述](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)
- [在 UI 自动化提供程序中支持控件模式](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)
- [客户端的 UI 自动化控件模式](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)
- [使用 UI 自动化获取复选框的切换状态](../../../docs/framework/ui-automation/get-the-toggle-state-of-a-check-box-using-ui-automation.md)
- [UI 自动化树概述](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)
- [在 UI 自动化中使用缓存](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)
