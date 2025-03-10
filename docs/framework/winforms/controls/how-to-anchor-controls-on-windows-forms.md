---
title: 如何：在 Windows 窗体上锚定控件
ms.date: 03/30/2017
helpviewer_keywords:
- Anchor property [Windows Forms], enabling resizable forms
- Windows Forms controls, screen resolutions
- resizing forms [Windows Forms]
- Windows Forms controls, size
- screen resolution and control display
- controls [Windows Forms], anchoring
- forms [Windows Forms], resizing
- Windows Forms, resizing
- controls [Windows Forms], positioning
ms.assetid: 59ea914f-fbd3-427a-80fe-decd02f7ae6d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 94fa6fe90e5583a3bfecf376af59d53f6d8528af
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987493"
---
# <a name="how-to-anchor-controls-on-windows-forms"></a>如何：Windows 窗体上的定位控件

如果要设计一个窗体, 用户可以在运行时调整其大小, 则窗体上的控件应正确调整大小和重新定位。 若要使用窗体动态调整控件大小, 可以使用<xref:System.Windows.Forms.Control.Anchor%2A> Windows 窗体控件的属性。 <xref:System.Windows.Forms.Control.Anchor%2A>属性定义控件的定位点位置。 当控件锚定到窗体并且调整了窗体的大小时, 控件将保持控件和定位点之间的距离。 例如, 如果您有一个<xref:System.Windows.Forms.TextBox>控件, 该控件锚定到窗体的左边缘、右边缘和下边缘, 则当调整窗体大小时<xref:System.Windows.Forms.TextBox> , 控件会水平调整大小, 以便与窗体的右侧和左侧保持相同的距离。 此外, 控件将对其自身定位, 使其位置与窗体下边缘的距离始终相同。 如果控件未定位并且调整了窗体的大小, 则相对于窗体边缘的控件位置会发生更改。

<xref:System.Windows.Forms.Control.Anchor%2A> 属性<xref:System.Windows.Forms.Control.AutoSize%2A>与属性交互。 有关详细信息, 请参阅[AutoSize 属性概述](autosize-property-overview.md)。

## <a name="anchor-a-control-on-a-form"></a>在窗体上定位控件

1. 在 Visual Studio 中, 选择要定位的控件。

    > [!NOTE]
    > 您可以通过按 CTRL 键, 单击每个控件以选择它, 然后按照此过程的其余部分, 来同时定位多个控件。

2. 在 "**属性**" 窗口中, 单击<xref:System.Windows.Forms.Control.Anchor%2A>属性右侧的箭头。

     将显示一个编辑器, 其中显示交叉。

3. 若要设置定位点, 请单击交叉的上、左、右或下部分。

     控件默认锚定到顶部和左侧。

4. 若要清除已锚定的控件侧, 请单击交叉的该侧。

5. 若要关闭<xref:System.Windows.Forms.Control.Anchor%2A> "属性编辑器", <xref:System.Windows.Forms.Control.Anchor%2A>请再次单击属性名称。

当在运行时显示窗体时, 控件调整大小以保持与窗体边缘的距离相同。 与定位边缘的距离始终与控件定位在 Windows 窗体设计器时所定义的距离相同。

> [!NOTE]
> 某些控件<xref:System.Windows.Forms.ComboBox> (如控件) 的高度限制为。 将控件定位到窗体或容器的底部不能强制控件超出其高度限制。

继承的控件必须`Protected`是能够锚定的。 若要更改控件的访问级别, 请在 " `Modifiers` **属性**" 窗口中设置其属性。

## <a name="see-also"></a>请参阅

- [Windows 窗体控件](index.md)
- [AutoSize 属性概述](autosize-property-overview.md)
- [如何：在 Windows 窗体上停靠控件](how-to-dock-controls-on-windows-forms.md)
- [演练：使用 FlowLayoutPanel 排列 Windows 窗体上的控件](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)
- [演练：使用 TableLayoutPanel 排列 Windows 窗体上的控件](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [演练：通过填充、边距和 AutoSize 属性排放 Windows 窗体控件](windows-forms-controls-padding-autosize.md)
