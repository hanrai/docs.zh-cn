---
title: 演练：在设计时在 Windows 窗体上分配 WPF 内容
ms.date: 03/30/2017
helpviewer_keywords:
- WPF content [Windows Forms], assigning at design time
- ElementHost control [Windows Forms], assigning WPF content at design time
- interoperability [WPF]
- Windows Forms, content assignments
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: b3e9ef93-7e0f-4a2f-8f1e-3437609a1eb7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bc5f5e2d8808c0a60df721bf2c0ed76b45ef49a0
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666251"
---
# <a name="walkthrough-assign-wpf-content-on-windows-forms-at-design-time"></a>演练：在设计时 Windows 窗体上分配 WPF 内容

本文介绍如何选择要在窗体上显示的 Windows Presentation Foundation (WPF) 控件类型。 可选择项目中包含的任何 WPF 控件类型。

## <a name="prerequisites"></a>系统必备

若要完成本演练，必须具有 Visual Studio。

## <a name="create-the-project"></a>创建项目

打开 Visual Studio, 并在 Visual Basic 或视觉对象C#中创建一个名为`SelectingWpfContent`的新 Windows 窗体应用程序项目。

> [!NOTE]
> 承载 WPF 内容时，仅支持 C# 和 Visual Basic 项目。

## <a name="create-the-wpf-control-types"></a>创建 WPF 控件类型

将 WPF 控件类型添加到项目后，可将其托管到不同的 <xref:System.Windows.Forms.Integration.ElementHost> 控件。

1. 将新的 WPF <xref:System.Windows.Controls.UserControl> 项目添加到解决方案。 使用控件类型的默认名称，`UserControl1.xaml`。 有关详细信息，请参见[演练：在设计时](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)在 Windows 窗体上创建新的 WPF 内容。

2. 在设计视图中，请确保已选中 `UserControl1`。

3. 在 "**属性**" 窗口中, 将<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>属性的值设置为**200**。

4. 向添加<xref:System.Windows.Controls.TextBox?displayProperty=nameWithType>一个控件, <xref:System.Windows.Controls.UserControl>并将该<xref:System.Windows.Controls.TextBox.Text%2A>属性的值设置为 "**托管内容**"。

5. 将第二个 WPF <xref:System.Windows.Controls.UserControl> 添加到项目。 使用控件类型的默认名称，`UserControl2.xaml`。

6. 在 "**属性**" 窗口中, 将<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>属性的值设置为**200**。

7. 向添加<xref:System.Windows.Controls.TextBox?displayProperty=nameWithType>一个控件, <xref:System.Windows.Controls.UserControl>并将该<xref:System.Windows.Controls.TextBox.Text%2A>属性的值设置为 "**托管内容 2**"。

   > [!NOTE]
   > 一般情况下，你应承载更复杂的 WPF 内容。 此处，<xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> 控件仅为了便于说明。

8. 生成项目。

## <a name="select-wpf-controls"></a>选择 WPF 控件

可将不同的 WPF 内容分配到 <xref:System.Windows.Forms.Integration.ElementHost> 控件，该控件现已承载内容。

1. 在 Windows 窗体设计器中打开 `Form1`。

2. 在 "**工具箱**" 中, 双击`UserControl1`在窗体上创建`UserControl1`的实例。

   `UserControl1` 的实例托管在名为 `elementHost1` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。

3. 在的智能标记面板`elementHost1`中, 打开 "**选择承载的内容**" 下拉列表。

4. 从下拉列表框中选择 " **UserControl2** "。

   `elementHost1` 控件现承载 `UserControl2` 类型的实例。

5. 在 "**属性**" 窗口中, 确认<xref:System.Windows.Forms.Integration.ElementHost.Child%2A> "属性" 设置为 " **UserControl2**"。

6. 从 "**工具箱**" 的 " **WPF 互操作性**" 组<xref:System.Windows.Forms.Integration.ElementHost>中, 将控件拖到窗体上。

   新控件的默认名称是 `elementHost2`。

7. 在的智能标记面板`elementHost2`中, 打开 "**选择承载的内容**" 下拉列表。

8. 从下拉列表中选择 " **UserControl1** "。

9. `elementHost2` 控件现承载 `UserControl1` 类型的实例。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [迁移和互操作性](../../wpf/advanced/migration-and-interoperability.md)
- [使用 WPF 控件](using-wpf-controls.md)
- [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)
