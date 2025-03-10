---
title: 如何：对 Windows 窗体上的对象分层
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms controls, layering
- controls [Windows Forms], layering
- z order
- controls [Windows Forms], positioning
- z-order
ms.assetid: 1acc4281-2976-4715-86f4-bda68134baaf
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2e4c6a3236b3a2a2afaad73fee21c3cf59b992b8
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987569"
---
# <a name="how-to-layer-objects-on-windows-forms"></a>如何：Windows 窗体上的层对象

当你创建复杂的用户界面或使用多文档界面 (MDI) 窗体时, 通常需要将控件和子窗体分层以创建更复杂的用户界面 (UI)。 若要在组的上下文中移动和跟踪控件和窗口, 请处理其*z 顺序*。 Z 顺序是窗体上的控件沿窗体的 z 轴 (深度) 的可视化分层。 Z 顺序顶部的窗口与所有其他窗口重叠。 所有其他窗口都与 z 顺序底部的窗口重叠。

## <a name="to-layer-controls-at-design-time"></a>在设计时将控件分层

1. 在 Visual Studio 中, 选择要分层的控件。

2. 在 "**格式**" 菜单上, 选择 "**顺序**", 然后选择 "**置于顶层**" 或 "置于**底层**"。

## <a name="to-layer-controls-programmatically"></a>以编程方式对控件进行分层

<xref:System.Windows.Forms.Control.BringToFront%2A>使用和<xref:System.Windows.Forms.Control.SendToBack%2A>方法来操作控件的 z 顺序。

例如, 如果<xref:System.Windows.Forms.TextBox> `txtFirstName`控件位于另一个控件之下, 并且你想要将其置于顶层, 请使用以下代码:

```vb
txtFirstName.BringToFront()
```

```csharp
txtFirstName.BringToFront();
```

```cpp
txtFirstName->BringToFront();
```

> [!NOTE]
> Windows 窗体支持*控件包含*。 控件包含涉及到在包含控件中放置许多控件, 如<xref:System.Windows.Forms.RadioButton> <xref:System.Windows.Forms.GroupBox>控件中的多个控件。 然后, 可以将控件分层到包含控件中。 移动组框也将移动控件, 因为这些控件包含在其中。

## <a name="see-also"></a>请参阅

- [Windows 窗体控件](index.md)
- [标记各个 Windows 窗体控件并创建它们的快捷键](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
- [在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)
- [按功能列出的 Windows 窗体控件](windows-forms-controls-by-function.md)
