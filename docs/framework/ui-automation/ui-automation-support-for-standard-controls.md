---
title: UI 自动化对标准控件的支持
ms.date: 03/30/2017
helpviewer_keywords:
- controls, UI Automation support for
- UI Automation, support for standard controls
ms.assetid: 3770ea8a-2655-4add-9c59-fe0610ad5084
ms.openlocfilehash: d83713a81e7675a68482890c2401f1a0a6803abc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69914232"
---
# <a name="ui-automation-support-for-standard-controls"></a>UI 自动化对标准控件的支持
> [!NOTE]
> 本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关的最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], 请[参阅 Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题包含有关对为 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 、 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]和 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]框架所开发的应用程序中标准控件的 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] 支持的信息。  
  
<a name="Windows_Presentation_Foundation_Controls"></a>   
## <a name="windows-presentation-foundation-controls"></a>Windows Presentation Foundation 控件  
 为用户交互提供信息或支持的所有 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 控件元素均具有对 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的完整本机支持。 面板等其他元素对 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]不可见。  
  
<a name="Win32_Controls"></a>   
## <a name="win32-controls"></a>Win32 控件  
 大多数 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 控件都通过 UIAutomationClientsideProviders.dll 中的客户端提供程序向 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 公开。 此程序集将自动注册，以用于 UI 自动化客户端应用程序。  
  
 仅对 ComCtrl32.dll 版本 6（随 [!INCLUDE[TLA#tla_winxp](../../../includes/tlasharptla-winxp-md.md)] 和更高版本提供）中的控件提供完全支持。  
  
 支持以下控件。  
  
|类名|控件类型|  
|----------------|------------------|  
|Button|Button|  
|Button|RadioButton|  
|Button|Group|  
|Button|CheckBox|  
|Button|超链接|  
|Button|SplitButton|  
|Button|CheckBox|  
|ComboBoxEx32|组合框|  
|组合框|组合框|  
|Edit|Document|  
|Edit|Edit|  
|SysLink|超链接|  
|Static|文本|  
|Static|图像|  
|SysIPAddress32|自定义|  
|SysHeader32|Header/HeaderItem|  
|SysListView32|DataGrid|  
|SysListView32|列表|  
|ListBox|列表|  
|ListBox|ListItem|  
|#32768|菜单|  
|#32768|MenuItem|  
|msctls_progress32|ProgressBar|  
|RichEdit|Document。 请参阅注释。|  
|RichEdit20A|Document|  
|RichEdit20W|Document|  
|RichEdit50W|Document|  
|ScrollBar|Slider|  
|msctls_trackbar32|Slider|  
|msctls_updown32|Spinner|  
|msctls_statusbar32|StatusBar|  
|SysTabControl32|Tab|  
|SysTabControl32|TabItem|  
|ToolbarWindow32|ToolBar|  
|ToolbarWindow32|MenuItem|  
|ToolbarWindow32|Button|  
|ToolbarWindow32|CheckBox|  
|ToolbarWindow32|RadioButton|  
|ToolbarWindow32|Separator|  
|tooltips_class32|ToolTip|  
|#32774|ToolTip|  
|ReBarWindow32|Toolbar|  
|SysTreeView32|树|  
|SysTreeView32|TreeItem|  
  
 **注意** 仅在随 [!INCLUDE[TLA#tla_winvista](../../../includes/tlasharptla-winvista-md.md)] 一起提供的版本中（在 RichEd20.dll 中为版本 3.1 和更高版本，在 MsftEdit.dll 中为版本 4.1 和更高版本）支持 RichEdit 控件。  
  
 不支持以下控件。  
  
|类名|控件类型|  
|----------------|------------------|  
|SysAnimate32|图像|  
|SysPager|Spinner|  
|SysDateTimePick32|自定义|  
|SysMonthCal32|Calendar|  
|MS_WINNOTE|ToolTip|  
|VBBubble|ToolTip|  
|ScrollBar（在用作独立控件时）|Slider|  
|SuperGrid|自定义|  
  
<a name="Windows_Forms_Controls"></a>   
## <a name="windows-forms-controls"></a>Windows 窗体控件  
 通过 uiautomationclientsideproviders.dll 中的客户[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]端提供程序向 Windows 窗体控件公开。 此程序集将自动注册，以用于 UI 自动化客户端应用程序。  
  
 通常, [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]支持作为公共控件的托管包装器 Windows 窗体控件。 支持以下控件。  
  
|类名|  
|----------------|  
|Button|  
|CheckBox|  
|CheckedListBox|  
|ColorDialog|  
|组合框|  
|FolderBrowser|  
|FontDialog|  
|GroupBox|  
|HscrollBar|  
|ImageList|  
|Label|  
|ListBox|  
|ListView|  
|MainMenu/ContextMenu|  
|MonthCalendar|  
|NotifyIcon|  
|OpenFileDialog|  
|PageSetupDialog|  
|PrintDialog|  
|ProgressBar|  
|RadioButton|  
|RichTextBox|  
|SaveFileDialog|  
|ScrollableControl|  
|SoundPlayer|  
|StatusBar|  
|TabControl/TabPage|  
|文本框|  
|计时器|  
|ToolBar|  
|ToolTip|  
|TrackBar|  
|TreeView|  
|VscrollBar|  
|Web 浏览器|  
  
 以下控件[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]仅通过其对 Microsoft Active Accessibility 的支持公开。 某些功能可能不可用。  
  
|控件名称|  
|------------------|  
|BindingSource|  
|DataGrid|  
|DataGridView|  
|DataNavigator|  
|DomainUpDown|  
|ErrorProvider|  
|FlowLayoutPanel|  
|窗体|  
|LinkLabel|  
|HelpProvider|  
|MaskedTextBox|  
|MenuStrip/ContextMenuStrip|  
|NumericUpDown|  
|Panel|  
|PictureBox|  
|PrintDocument|  
|PrintPreview-Control|  
|PrintPreview-Dialog|  
|PropertyGrid|  
|用户控件|  
|ToolStrip|  
|TableLayoutPanel|  
|SplitContainer/SplitterPanel|  
|Splitter|  
|RaftingContainer|  
|StatusStrip|  
  
## <a name="see-also"></a>请参阅

- [UI 自动化控件类型](../../../docs/framework/ui-automation/ui-automation-control-types.md)
