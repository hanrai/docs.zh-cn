---
title: 实现 UI 自动化 SelectionItem 控件模式
ms.date: 03/30/2017
helpviewer_keywords:
- Selection Item control pattern
- UI Automation, Selection Item control pattern
- control patterns, Selection Item
ms.assetid: 76b0949a-5b23-4cfc-84cc-154f713e2e12
ms.openlocfilehash: aef1d31499f65834fa1268147e45f82294fe560a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69935693"
---
# <a name="implementing-the-ui-automation-selectionitem-control-pattern"></a>实现 UI 自动化 SelectionItem 控件模式
> [!NOTE]
> 本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关的最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], 请[参阅 Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍实现 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>的准则和约定，包括有关属性、方法和事件的信息。 本概述的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.SelectionItemPattern> 控件模式用于支持充当实现 <xref:System.Windows.Automation.Provider.ISelectionProvider>的容器控件的独立可选子项的控件。 有关实现 SelectionItem 控件模式的控件的示例, 请参阅[UI 自动化客户端的控件模式映射](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>实现准则和约定  
 在实现 Selection Item 控件模式时，请注意以下准则和约定：  
  
- 管理实现 <xref:System.Windows.Automation.Provider.IRawElementProviderFragmentRoot>的子控件的单选控件（如“显示属性” 对话框中的“屏幕分辨率” 滑块）应实现 <xref:System.Windows.Automation.Provider.ISelectionProvider> ，且其子级应实现 <xref:System.Windows.Automation.Provider.IRawElementProviderFragment> 和 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>。  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>   
## <a name="required-members-for-iselectionitemprovider"></a>ISelectionItemProvider 必需的成员  
 以下属性、方法和事件都是实现 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>所必需的。  
  
|必需的成员|成员类型|说明|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|Property|无|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|Property|无|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.GetSelection%2A>|方法|无|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|Event|在容器中的选项发生重大更改并需要发送多于 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent> 常量所允许的 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent> 和 <xref:System.Windows.Automation.Provider.AutomationInteropProvider.InvalidateLimit> 事件时引发。|  
  
- 如果 <xref:System.Windows.Automation.SelectionItemPattern.Select%2A>、 <xref:System.Windows.Automation.SelectionItemPattern.AddToSelection%2A>或 <xref:System.Windows.Automation.SelectionItemPattern.RemoveFromSelection%2A> 的结果是单个的选定的项，则应引发 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent> ；否则根据需要发送 <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>/ <xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent> 。  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>Exceptions  
 提供程序必须引发以下异常。  
  
|异常类型|条件|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|尝试下列任一操作时：<br /><br /> -   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> = <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> = `true` 并且已选择元素时。<br />-   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.RemoveFromSelection%2A> = <xref:System.Windows.Automation.SelectionPattern.IsSelectionRequiredProperty> = `true` 并且仅选择了一个元素时。<br />-   <xref:System.Windows.Automation.Provider.ISelectionItemProvider.AddToSelection%2A> = <xref:System.Windows.Automation.SelectionPattern.CanSelectMultipleProperty> = `false` 并且已选择另一个元素时。|  
  
## <a name="see-also"></a>请参阅

- [UI 自动化控件模式概述](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)
- [在 UI 自动化提供程序中支持控件模式](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)
- [客户端的 UI 自动化控件模式](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)
- [实现 UI 自动化 Selection 控件模式](../../../docs/framework/ui-automation/implementing-the-ui-automation-selection-control-pattern.md)
- [UI 自动化树概述](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)
- [在 UI 自动化中使用缓存](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)
- [片段提供程序示例](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771502(v=vs.90))
