---
title: 演练：使用 DesignerSerializationVisibilityAttribute 序列化标准类型的集合
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- serialization [Windows Forms], collections
- standard types [Windows Forms], collections
- collections [Windows Forms], serializing
- collections [Windows Forms], standard types
ms.assetid: 020c9df4-fdc5-4dae-815a-963ecae5668c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2fbb0715d148b443b1eca8f400e4ad43eb51fa43
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015739"
---
# <a name="walkthrough-serialize-collections-of-standard-types"></a>演练：序列化标准类型的集合

自定义控件有时会将集合公开为属性。 本演练演示如何使用<xref:System.ComponentModel.DesignerSerializationVisibilityAttribute>类来控制在设计时如何序列化集合。 <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content>将值应用于集合属性可确保对属性进行序列化。

要将本主题中的代码作为单个列表进行复制，请参阅[如何：用 DesignerSerializationVisibilityAttribute](/previous-versions/visualstudio/visual-studio-2013/ms171833(v=vs.120))序列化标准类型的集合。

## <a name="prerequisites"></a>系统必备

若要完成本演练，必须具有 Visual Studio。

## <a name="create-a-control-with-a-serializable-collection"></a>使用可序列化集合创建控件

第一步是创建一个控件, 该控件将可序列化集合作为属性。 您可以使用 "**集合编辑器**" 编辑此集合的内容, 您可以从 "**属性**" 窗口访问此集合。

1. 在 Visual Studio 中, 创建一个 Windows 控件库项目, 并将其命名为**SerializationDemoControlLib**。

2. 重`UserControl1`命名`SerializationDemoControl`为。 有关详细信息, 请参阅[重命名代码符号重构](/visualstudio/ide/reference/rename)。

3. 在 "**属性**" 窗口中, 将<xref:System.Windows.Forms.Padding.All%2A?displayProperty=nameWithType>属性的值设置为**10**。

4. 将控件放置在中`SerializationDemoControl`。 <xref:System.Windows.Forms.TextBox>

5. 选择 <xref:System.Windows.Forms.TextBox> 控件。 在 "**属性**" 窗口中, 设置以下属性。

    |Property|更改为|
    |--------------|---------------|
    |**多行**|`true`|
    |**停靠**|<xref:System.Windows.Forms.DockStyle.Fill>|
    |**ScrollBars**|<xref:System.Windows.Forms.ScrollBars.Vertical>|
    |**ReadOnly**|`true`|

6. 在**代码编辑器**中, 声明中`stringsValue` `SerializationDemoControl`名为的字符串数组字段。

     [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#4)]
     [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#4)]
     [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#4)]

7. 定义上的`Strings`属性。 `SerializationDemoControl`

   > [!NOTE]
   > <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content>该值用于启用集合的序列化。

   [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#5)]
   [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#5)]
   [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#5)]

8. 按**F5**生成项目并在 " **UserControl 测试容器**" 中运行控件。

9. 查找**UserControl 测试容器**的中<xref:System.Windows.Forms.PropertyGrid>的**字符串**属性。 选择 "**字符串**" 属性, 然后在 "Visual![Studio](./media/visual-studio-ellipsis-button.png)属性窗口中选择省略号按钮 (...), 以打开"**字符串集合编辑器**"。

10. 在**字符串集合编辑器**中输入几个字符串。 通过在每个字符串的结尾按**enter**键来分隔它们。 输入完字符串后, 请单击 **"确定"** 。

   > [!NOTE]
   > 你键入的字符串将显示在<xref:System.Windows.Forms.TextBox> `SerializationDemoControl`的中。

## <a name="serialize-a-collection-property"></a>序列化集合属性

若要测试控件的序列化行为, 请将其放在窗体上, 并使用**集合编辑器**更改集合的内容。 可以通过查看**Windows 窗体设计器**向其发出代码的特定设计器文件来查看序列化的集合状态。

1. 向解决方案中添加一个 Windows 应用程序项目。 将项目命名为 `SerializationDemoControlTest`。

2. 在 "**工具箱**" 中, 找到名为 " **SerializationDemoControlLib 组件**" 的选项卡。 在此选项卡中, 你将`SerializationDemoControl`找到。 有关详细信息，请参见[演练：用自定义组件](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)自动填充工具箱。

3. 将放置`SerializationDemoControl`在窗体上。

4. 在 "**属性**" 窗口中找到属性。`Strings` 单击 " `Strings`属性", 然后单击 "Visual![Studio](./media/visual-studio-ellipsis-button.png)" 属性窗口中的省略号按钮 (...), 以打开 "**字符串集合编辑器**"。

5. 在**字符串集合编辑器**中键入多个字符串。 在每个字符串的末尾按**enter**分隔它们。 输入完字符串后, 请单击 **"确定"** 。

> [!NOTE]
> 你键入的字符串将显示在<xref:System.Windows.Forms.TextBox> `SerializationDemoControl`的中。

6. 在“解决方案资源管理器”中，单击“显示所有文件”按钮。

7. 打开 " **Form1** " 节点。 下面是一个名为**Form1.Designer.cs**或的文件。 这是**Windows 窗体设计器**发出代码的文件, 表示窗体的设计时状态及其子控件。 在“代码编辑器”中打开此文件。

8. 打开名为 " **Windows 窗体设计器生成的代码**" 的区域, 找到标记为 " **serializationDemoControl1**" 的部分。 此标签下面是表示控件的已序列化状态的代码。 在步骤5中键入的字符串将显示在对属性的`Strings`赋值中。 下面的代码示例在C#和 Visual Basic 中, 会显示类似于键入字符串 "red"、"橙色" 和 "黄色" 的代码。

    ```csharp
    this.serializationDemoControl1.Strings = new string[] {
            "red",
            "orange",
            "yellow"};
    ```

    ```vb
    Me.serializationDemoControl1.Strings = New String() {"red", "orange", "yellow"}
    ```

9. 在**代码编辑器**中, 将<xref:System.ComponentModel.DesignerSerializationVisibilityAttribute> `Strings`属性的值更改为<xref:System.ComponentModel.DesignerSerializationVisibility.Hidden>。

    ```csharp
    [DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)]
    ```

    ```vb
    <DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)> _
    ```

10. 重新生成解决方案, 并重复步骤3和4。

> [!NOTE]
> 在这种情况下, **Windows 窗体设计器**不发出对属性`Strings`的赋值。

## <a name="next-steps"></a>后续步骤

一旦知道如何序列化标准类型的集合, 请考虑将自定义控件更深入地集成到设计时环境中。 以下主题介绍如何增强自定义控件的设计时集成:

- [设计时体系结构](/previous-versions/visualstudio/visual-studio-2013/c5z9s1h4(v=vs.120))

- [Windows 窗体控件中的特性](attributes-in-windows-forms-controls.md)

- [设计器序列化概述](/previous-versions/visualstudio/visual-studio-2013/ms171834(v=vs.120))

- [演练：创建利用 Visual Studio 设计时功能的 Windows 窗体控件](creating-a-wf-control-design-time-features.md)

## <a name="see-also"></a>请参阅

- <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute>
- [演练：用自定义组件自动填充工具箱](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
