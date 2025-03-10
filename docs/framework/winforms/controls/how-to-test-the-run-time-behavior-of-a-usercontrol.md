---
title: 如何：测试 UserControl 的运行时行为
ms.date: 03/30/2017
helpviewer_keywords:
- UserControl class [Windows Forms], testing
- user controls [Windows Forms], testing
- composite controls [Windows Forms], testing
- UserControl Test Container
- UserControl class [Windows Forms], run-time behavior
ms.assetid: 4e4d5c49-1346-40ac-9d96-40211b573583
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 1be79d52be3b5b84938d8548a8f101e965fa9dbb
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015769"
---
# <a name="how-to-test-the-run-time-behavior-of-a-usercontrol"></a>如何：测试 UserControl 的运行时行为

开发<xref:System.Windows.Forms.UserControl>时, 需要测试其运行时行为。 您可以创建一个单独的基于 Windows 的应用程序项目, 并将您的控件置于测试窗体上, 但此过程是不方便的。 更快、更简单的方法是使用 Visual Studio 提供的**UserControl 测试容器**。 此测试容器直接从 Windows 控件库项目启动。

> [!IMPORTANT]
> 对于用于加载<xref:System.Windows.Forms.UserControl>的测试容器, 控件必须至少有一个公共构造函数。

> [!NOTE]
> 无法使用C++ **UserControl 测试容器**测试视觉对象控件。

## <a name="test-the-run-time-behavior-of-a-usercontrol"></a>测试 UserControl 的运行时行为

1. 在 Visual Studio 中, 创建一个 Windows 控件库项目, 并将其命名为**TestContainerExample**。

2. 在**Windows 窗体设计器**中, 将<xref:System.Windows.Forms.Label>控件从 "**工具箱**" 拖动到控件的设计图面上。

3. 按**F5**生成项目, 并运行 " **UserControl 测试容器**"。 测试容器显示<xref:System.Windows.Forms.UserControl>在**预览**窗格中。

4. 选择显示<xref:System.Windows.Forms.Control.BackColor%2A> <xref:System.Windows.Forms.PropertyGrid>在 "**预览**" 窗格右侧的控件中的属性。 将其值更改为**ControlDark**。 观察控件更改为较暗的颜色。 尝试更改其他属性值并观察控件上的效果。

5. 单击 "**预览**" 窗格下的 "**停靠填充用户控件**" 复选框。 请注意, 控件调整大小以填充窗格。 调整测试容器的大小, 并观察控件是否随窗格一起调整大小。

6. 关闭测试容器。

7. 向**TestContainerExample**项目添加另一个用户控件。

8. 在**Windows 窗体设计器**中, 将<xref:System.Windows.Forms.Button>控件从 "**工具箱**" 拖动到控件的设计图面上。

9. 按**F5**生成项目并运行测试容器。

10. 单击 "**选择用户控件**<xref:System.Windows.Forms.ComboBox> " 以在两个用户控件之间切换。

## <a name="test-user-controls-from-another-project"></a>测试其他项目中的用户控件

可以在当前项目的测试容器中测试其他项目中的用户控件。

1. 在 Visual Studio 中, 创建一个 Windows 控件库项目, 并将其命名为**TestContainerExample2**。

2. 在**Windows 窗体设计器**中, 将<xref:System.Windows.Forms.RadioButton>控件从 "**工具箱**" 拖动到控件的设计图面上。

3. 按**F5**生成项目并运行测试容器。 测试容器显示<xref:System.Windows.Forms.UserControl>在**预览**窗格中。

4. 单击 "**加载**" 按钮。

5. 在 "**打开**" 对话框中, 导航到在前面的过程中生成的 " **TestContainerExample**"。 选择**TestContainerExample**并单击 "**打开**" 按钮以加载用户控件

6. 使用 "**选择用户" 控件**<xref:System.Windows.Forms.ComboBox>可以从**TestContainerExample**项目中的两个用户控件之间切换。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.UserControl>
- [如何：创作复合控件](how-to-author-composite-controls.md)
- [演练：创作复合控件](walkthrough-authoring-a-composite-control-with-visual-csharp.md)
- [用户控件设计器](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/183c3hth(v=vs.100))
