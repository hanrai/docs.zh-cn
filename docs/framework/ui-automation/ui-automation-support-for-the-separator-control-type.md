---
title: UI 自动化对 Separator 控件类型的支持
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Separator control type
- Separator control type
- control types, Separator
ms.assetid: 89f42247-c699-4afa-91e1-2baaf0d86c9d
ms.openlocfilehash: 791026865d37b1db060e83ac6d18a0b67841d351
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69954743"
---
# <a name="ui-automation-support-for-the-separator-control-type"></a>UI 自动化对 Separator 控件类型的支持
> [!NOTE]
> 本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关的最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], 请[参阅 Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题提供了有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 对于 Separator 控件类型的支持信息。 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中，控件类型是一组条件，控件必须满足这些条件才能使用 <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> 属性。 这些条件包括针对 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树结构、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性值和控件模式的特定准则。  
  
 Separator 控件用于直观地将一个空间划分为两个区域。 例如，分隔符控件可以是一个条形图，在窗口中定义两个窗格。 如果可以移动该分隔符，则应将该控件公开为控件类型中的 Thumb。  
  
 以下几节定义了 Separator 控件类型必需的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树结构、属性、控件模式和事件。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 要求适用于所有列表控件，无论控件是 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]、 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]还是 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## <a name="required-ui-automation-tree-structure"></a>必需的 UI 自动化树结构  
 下表描述了与 Separator 控件有关的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树的控件视图和内容视图，以及每个视图中可包含的内容。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树的详细信息，请参阅 [UI Automation Properties Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)。  
  
|控件视图|内容视图|  
|------------------|------------------|  
|Separator|-Separator 控件绝不包含内容。|  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>必需的 UI 自动化属性  
 下表列出了 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性，这些属性的值或定义与 Separator 控件尤其相关。 有关[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]属性的详细信息, 请参阅[客户端的 UI 自动化属性](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性|值|说明|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|请参见备注|此属性的值在应用程序的所有控件中都必须保持唯一。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|请参见备注|包含整个控件的最外层矩形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|请参见备注|如果存在边界矩形，则受支持。 如果边界矩形中存在无法单击的点，而你要执行专门的命中测试，则重写并提供可单击的点。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|请参见备注|如果该控件可以接收键盘焦点，则它必须支持此属性。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|""|Separator 控件不需要 NameProperty。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`null`|Separator 控件没有静态标签。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Separator|此值对于所有 UI 框架均相同。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|“分隔符”|与 Separator 控件类型相对应的已本地化字符串。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|False|Separator 控件不包含内容。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Separator 控件必须始终是一个控件。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## <a name="required-ui-automation-control-patterns"></a>必需的 UI 自动化控件模式  
 Separator 控件不需要支持任何控件模式。  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>必需的 UI 自动化事件  
 下表列出了需要由所有 Separator 控件支持的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件。 有关事件的详细信息，请参阅 [F:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty](../../../docs/framework/ui-automation/ui-automation-events-overview.md)。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件|支持|说明|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 属性更改事件|必填|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 属性更改事件|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性更改事件|必填|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必填|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必需|无|  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Automation.ControlType.Separator>
- [UI 自动化控件类型概述](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)
- [UI 自动化概述](../../../docs/framework/ui-automation/ui-automation-overview.md)
