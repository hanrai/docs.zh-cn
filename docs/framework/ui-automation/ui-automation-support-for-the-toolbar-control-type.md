---
title: UI 自动化对 ToolBar 控件类型的支持
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Toolbar
- UI Automation, Toolbar control type
- ToolBar control type
ms.assetid: 85152efd-f4c5-430c-8878-3371cc598616
ms.openlocfilehash: 342a8b6567183f6207f78f91265353f5ece5ca59
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69954344"
---
# <a name="ui-automation-support-for-the-toolbar-control-type"></a>UI 自动化对 ToolBar 控件类型的支持
> [!NOTE]
> 本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关的最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], 请[参阅 Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题提供有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 对于工具栏控件类型的支持信息。 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中，控件类型是一组条件，控件必须满足这些条件才能使用 <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> 属性。 这些条件包括针对 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树结构、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性值和控件模式的特定准则。 通过工具栏控件，最终用户可以激活应用程序中包含的命令和工具。  
  
 以下几节定义了工具栏控件类型必需的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树结构、属性、控件模式和事件。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 要求适用于所有工具栏控件，无论对于 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]、 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]还是 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]。  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## <a name="required-ui-automation-tree-structure"></a>必需的 UI 自动化树结构  
 下表介绍与工具栏控件有关的控件视图和 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树的内容视图并介绍可被包含在每个视图中的内容。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树的详细信息，请参阅 [UI Automation Properties Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)。  
  
|控件视图|内容视图|  
|------------------|------------------|  
|ToolBar<br /><br /> -各种控件 (0 个或多个)|ToolBar<br /><br /> -各种控件 (0 个或多个)|  
  
 工具栏控件可以在其子树内包含任何类型的控件。 它们通常包含按钮、组合框和拆分按钮。  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>必需的 UI 自动化属性  
 下表列出 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性，这些属性的值或定义与工具栏控件尤其相关。 有关[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]属性的详细信息, 请参阅[客户端的 UI 自动化属性](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 属性|值|说明|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|请参阅注释。|此属性的值在应用程序的所有控件中都必须保持唯一。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|请参阅注释。|包含整个控件的最外层矩形。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|请参阅注释。|如果存在边界矩形，则受支持。 如果边界矩形中存在无法单击的点，而你要执行专门的命中测试，则重写并提供可单击的点。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|请参阅注释。|如果该控件可以接收键盘焦点，则它必须支持此属性。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|视情况而定|工具栏控件不需要名称，除非应用程序中使用了多个状态栏。 如果存在多个状态栏，则每个状态栏必须具有可分辨的名称（例如“格式”或“大纲”）。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|工具栏控件绝对不会有标签。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ToolBar|此值对于所有 UI 框架均相同。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|“工具栏”|对应于工具栏控件类型的本地化的字符串。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|工具栏控件始终是内容控件。|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|工具栏控件必须始终为控件。|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## <a name="required-ui-automation-control-patterns"></a>必需的 UI 自动化控件模式  
 下表列出需要由工具栏控件支持的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 控件模式。 有关控件模式的详细信息，请参阅 [F:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)。  
  
|控件模式|支持|说明|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.ExpandCollapsePattern>|视情况而定|如果工具栏可以展开和折叠以显示更多项，则它必须支持此模式。|  
|<xref:System.Windows.Automation.DockPattern>|视情况而定|如果工具栏可停靠到屏幕的不同部分，则它必须支持此模式。|  
|<xref:System.Windows.Automation.TransformPattern>|视情况而定|如果工具栏可以调整大小、旋转或移动，则它必须支持此模式。|  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>必需的 UI 自动化事件  
 下表列出需要由所有工具栏控件支持的 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件。 有关事件的详细信息，请参阅 [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md)。  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 事件|支持|说明|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> 属性更改事件。|必需|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> 属性更改事件。|必填|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> 属性更改事件。|必需|无|  
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> 属性更改事件。|视情况而定|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|必填|无|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|必需|无|  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Automation.ControlType.ToolBar>
- [UI 自动化控件类型概述](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)
- [UI 自动化概述](../../../docs/framework/ui-automation/ui-automation-overview.md)
