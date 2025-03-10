---
title: 演练：使用 Microsoft Expression Blend 创建按钮
ms.date: 03/30/2017
helpviewer_keywords:
- buttons [WPF]
- converting [WPF], shape to button
- Expression Blend [WPF Designer]
ms.assetid: ff5037c2-bba7-4cae-8abb-6475b686c48e
ms.openlocfilehash: 1b4c775ea0680dcd8252a98c722dfe8f7e62548f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69942507"
---
# <a name="walkthrough-create-a-button-by-using-microsoft-expression-blend"></a>演练：使用 Microsoft Expression Blend 创建按钮
本演练将指导你完成使用 Microsoft Expression Blend [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]创建自定义按钮的过程。  
  
> [!IMPORTANT]
> Microsoft Expression Blend 的工作方式[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]是生成, 然后将其编译为生成可执行程序。 如果你希望直接使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] , 则有另一个演练使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] Visual Studio (而不是 Blend) 创建与此应用程序相同的应用程序。 有关详细信息, 请参阅[使用 XAML 创建按钮](walkthrough-create-a-button-by-using-xaml.md)。  
  
 下图显示了您将创建的自定义按钮。  
  
 ![你将创建的自定义按钮](./media/custom-button-blend-intro.jpg "custom_button_blend_Intro")  
  
## <a name="convert-a-shape-to-a-button"></a>将形状转换为按钮  
 在本演练的第一部分中, 你将创建自定义按钮的自定义外观。 为此, 首先要将矩形转换为按钮。 然后, 将其他形状添加到按钮的模板中, 从而创建一个更复杂的 "按钮" 按钮。 为什么不使用常规按钮启动并对其进行自定义？ 因为按钮具有不需要的内置功能,对于自定义按钮, 从矩形开始更容易。  
  
#### <a name="to-create-a-new-project-in-expression-blend"></a>在 Expression Blend 中创建新项目  
  
1. 开始 Expression Blend。 (单击 "**开始**", 指向 "**所有程序**", 指向 " **microsoft expression**", 然后单击 " **microsoft expression Blend**"。)  
  
2. 如果需要, 最大化应用程序。  
  
3. 在“文件”菜单上，单击“新建项目”。  
  
4. 选择**标准应用程序 (.exe)** 。  
  
5. 为项目`CustomButton`命名并按 **"确定"** 。  
  
 此时, 您有一个空[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]项目。 可以按 F5 运行该应用程序。 正如您所料, 应用程序只包含一个空白窗口。 接下来, 创建一个圆角矩形, 并将其转换为按钮。  
  
#### <a name="to-convert-a-rectangle-to-a-button"></a>将矩形转换为按钮  
  
1. **将窗口背景属性设置为黑色:** 选择窗口, 单击 "**属性" 选项卡**, 然后将<xref:System.Windows.Controls.Control.Background%2A>属性设置`Black`为。  
  
     ![如何将按钮背景设置为黑色](./media/custom-button-blend-changebackground.png "custom_button_blend_ChangeBackground")  
  
2. **在窗口上的按钮大小约绘制一个矩形:** 选择左侧工具面板上的 "矩形" 工具, 然后将该矩形拖到窗口上。  
  
     ![如何绘制矩形](./media/custom-button-blend-drawrect.png "custom_button_blend_DrawRect")  
  
3. **将矩形的角取整:** 拖动矩形的控制点或直接设置<xref:System.Windows.Shapes.Rectangle.RadiusX%2A>和<xref:System.Windows.Shapes.Rectangle.RadiusY%2A>属性。 将<xref:System.Windows.Shapes.Rectangle.RadiusX%2A> 和<xref:System.Windows.Shapes.Rectangle.RadiusY%2A>的值设置为20。  
  
     ![如何使矩形的角变圆](./media/custom-button-blend-roundcorners.png "custom_button_blend_RoundCorners")  
  
4. **将矩形更改为按钮:** 选择该矩形。 单击 "**工具**" 菜单上的 "**生成" 按钮**。  
  
     ![如何将形状转换为按钮](./media/custom-button-blend-makebutton.png "custom_button_blend_MakeButton")  
  
5. **指定样式/模板的作用域:** 将显示如下所示的对话框。  
  
     !["创建样式资源" 对话框](./media/custom-button-blend-makebutton2.gif "custom_button_blend_MakeButton2")  
  
     对于**资源名称 (Key)** , 请选择 "**应用到所有**"。  这会使生成的样式和按钮模板应用于所有作为按钮的对象。 对于**中**的 "定义", 选择 "**应用程序**"。 这会使生成的样式和按钮模板在整个应用程序中的作用域。 在这两个框中设置值时, 按钮样式和模板应用于整个应用程序中的所有按钮, 并且在应用程序中创建的任何按钮默认情况下都使用此模板。  
  
## <a name="edit-the-button-template"></a>编辑按钮模板  
 现在, 你已有一个已更改为按钮的矩形。 在本部分中, 您将修改该按钮的模板, 并进一步自定义其外观。  
  
#### <a name="to-edit-the-button-template-to-change-the-button-appearance"></a>编辑按钮模板以更改按钮外观  
  
1. **进入编辑模板视图:** 若要进一步自定义按钮的外观, 需要编辑按钮模板。 此模板是在将矩形转换为按钮时创建的。 若要编辑按钮模板, 请右键单击该按钮, 然后选择 "**编辑控件部件 (模板)** ", 然后单击 "**编辑模板**"。  
  
     ![如何编辑模板](./media/custom-button-blend-edittemplate.jpg "custom_button_blend_EditTemplate")  
  
     请注意, 在模板编辑器中, 按钮现在分隔为<xref:System.Windows.Shapes.Rectangle> <xref:System.Windows.Controls.ContentPresenter>和。 <xref:System.Windows.Controls.ContentPresenter>用于显示按钮中的内容 (例如, 字符串 "按钮")。 矩形和<xref:System.Windows.Controls.ContentPresenter>都在内<xref:System.Windows.Controls.Grid>进行布局。  
  
     ![表示矩形的组件](./media/custom-button-blend-templatepanel.png "custom_button_blend_TemplatePanel")  
  
2. **更改模板组件的名称:** 右键单击模板清单中的矩形, 将<xref:System.Windows.Shapes.Rectangle>名称从 "[rectangle]" 更改为 "outerRectangle", 并将 "[system.windows.controls.contentpresenter>]" 更改为 "myContentPresenter"。  
  
     ![如何重命名模板的组件](./media/custom-button-blend-renamecomponents.png "custom_button_blend_RenameComponents")  
  
3. **更改矩形, 使其在内部 (如环形) 为空:** 选择**outerRectangle**并将<xref:System.Windows.Shapes.Shape.Fill%2A>设置为 "透明" <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> , 并设置为5。  
  
     ![如何使矩形为空](./media/custom-button-blend-changerectproperties.png "custom_button_blend_ChangeRectProperties")  
  
     然后, 将<xref:System.Windows.Shapes.Shape.Stroke%2A>设置为模板的任何颜色。 为此, 请单击 "**笔划**" 旁边的小白色框, 选择 " **CustomExpression**", 然后在对话框中键入 "{TemplateBinding Background}"。  
  
     ![如何设置使用模板的颜色](./media/custom-button-blend-templatestroke.png "custom_button_blend_TemplateStroke")  
  
4. **创建内部矩形:** 现在, 创建另一个矩形 (将其命名为 "innerRectangle"), 并在**outerRectangle**内将其对称放置。 对于这种类型的工作, 你可能想要进行缩放以使编辑区域中的按钮变大。  
  
    > [!NOTE]
    > 您的矩形看起来可能与图中的不同 (例如, 它可能具有圆角)。  
  
     ![如何在另一个矩形内创建矩形](./media/custom-button-blend-innerrectangleproperties.png "custom_button_blend_innerRectangleProperties")  
  
5. **将 System.windows.controls.contentpresenter> 移到顶部:** 此时, 可能不会再看到文本 "Button"。 如果是这样, 则这是因为**innerRectangle**位于**myContentPresenter**的顶层。 若要解决此问题, 请将**myContentPresenter**拖到下面的**innerRectangle**。 重定位矩形和**myContentPresenter** , 使其看起来类似于下面的内容。  
  
    > [!NOTE]
    > 此外, 还可以通过右键单击**myContentPresenter**并按 "**发送前**" 将其定位在顶部。  
  
     ![如何将一个按钮移动到另一个按钮之上](./media/custom-button-blend-innerrectangle2.png "custom_button_blend_innerRectangle2")  
  
6. **更改 innerRectangle 的外观:** <xref:System.Windows.Shapes.Rectangle.RadiusX%2A>将、 <xref:System.Windows.Shapes.Rectangle.RadiusY%2A>和值设置为20。<xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 此外, 使用自定义<xref:System.Windows.Shapes.Shape.Fill%2A>表达式 "{TemplateBinding background}" 将设置为模板的背景, 并将设置<xref:System.Windows.Shapes.Shape.Stroke%2A>为 "透明"。 <xref:System.Windows.Shapes.Shape.Fill%2A>请注意, <xref:System.Windows.Shapes.Shape.Stroke%2A>和的**innerRectangle**的设置与**outerRectangle**的设置相反。  
  
     ![如何更改矩形的外观](./media/custom-button-blend-glassrectangleproperties1.png "custom_button_blend_glassRectangleProperties1")  
  
7. **在顶部添加玻璃层:** 自定义按钮外观的最后一项是在顶部添加玻璃层。 此玻璃层包含第三个矩形。 由于玻璃将覆盖整个按钮, 因此, 玻璃矩形在维度中类似于**outerRectangle**。 因此, 只需制作一份**outerRectangle**副本就能创建该矩形。 突出显示**outerRectangle** , 并使用 Ctrl + C 和 Ctrl + V 制作副本。 将此新矩形命名为 "glassCube"。  
  
8. **如有必要, 重定位 glassCube:** 如果**glassCube**尚未定位, 使其覆盖整个按钮, 请将其拖动到位置。  
  
9. **为 glassCube 指定一个与 outerRectangle 略有不同的形状:** 更改**glassCube**的属性。 首先将<xref:System.Windows.Shapes.Rectangle.RadiusX%2A>和<xref:System.Windows.Shapes.Rectangle.RadiusY%2A>属性更改为 10, 将<xref:System.Windows.Shapes.Shape.StrokeThickness%2A>更改为2。  
  
     ![GlassCube 的外观设置](./media/custom-button-blend-glasscubeappearance.gif "custom_button_blend_GlassCubeAppearance")  
  
10. **使 glassCube 看起来像玻璃:** 通过使用线性渐变 (75% 不透明) 将设置为glassy外观,在大约均匀间隔的时间段内,在白色和透明之间交替变化。<xref:System.Windows.Shapes.Shape.Fill%2A> 这是将梯度停止点设置为:  
  
    - 梯度停止点 1:白色, Alpha 值为 75%  
  
    - 梯度停止点 2:透明  
  
    - 梯度停止点 3:白色, Alpha 值为 75%  
  
    - 梯度停止点 4:透明  
  
    - 梯度停止点 5:白色, Alpha 值为 75%  
  
    - 梯度停止点 6:透明  
  
     这会创建一个 "波浪形" 玻璃外观。  
  
     ![看起来像玻璃的矩形](./media/custom-button-blend-glassrectangleproperties2.png "custom_button_blend_glassRectangleProperties2")  
  
11. **隐藏玻璃层:** 现在, 你已经了解了 glassy 层的外观, 接下来请进入 "**属性" 面板**的 "**外观" 窗格**, 并将不透明度设置为 0% 以隐藏它。 在前面的部分中, 我们将使用属性触发器和事件来显示和操作玻璃层。  
  
     ![如何隐藏玻璃矩形](./media/custom-button-glassrectangleproperties3.gif "custom_button_glassRectangleProperties3")  
  
## <a name="customize-the-button-behavior"></a>自定义按钮行为  
 此时, 您已通过编辑模板的模板对该按钮的显示进行了自定义, 但该按钮不会响应用户操作, 这是典型的按钮 (例如, 在鼠标悬停、接收焦点和单击时更改外观)。接下来的两个过程演示如何将这类行为生成为自定义按钮。 我们将从简单的属性触发器开始, 然后添加事件触发器和动画。  
  
#### <a name="to-set-property-triggers"></a>设置属性触发器  
  
1. **创建新的属性触发器:** 选择**glassCube**后, 在 "**触发器**" 面板中单击 " **+ 属性**" (请参阅下一步后面的图)。 这将创建一个具有默认属性触发器的属性触发器。  
  
2. **将 System.windows.uielement.ismouseover 用作触发器使用的属性:** 将属性更改为<xref:System.Windows.UIElement.IsMouseOver%2A>。 当<xref:System.Windows.UIElement.IsMouseOver%2A>属性为`true`时 (当用户用鼠标指向按钮时), 这会使属性触发器激活。  
  
     ![如何对属性设置触发器](./media/custom-button-blend-ismousedoverpropertytrigger.png "custom_button_blend_IsMousedOverPropertyTrigger")  
  
3. **System.windows.uielement.ismouseover 触发 glassCube 的 100% 的不透明度:** 请注意,**触发器记录已打开**(请参阅上图)。 这意味着, 在记录时对**glassCube**属性值所做的任何更改都将成为在为<xref:System.Windows.UIElement.IsMouseOver%2A> `true`时进行的操作。 录制时, 将<xref:System.Windows.UIElement.Opacity%2A> **glassCube**的更改为 100%。  
  
     ![如何设置按钮的不透明度](./media/custom-button-blend-ismousedoverpropertytrigger2.gif "custom_button_blend_IsMousedOverPropertyTrigger2")  
  
     现在, 您已创建了第一个属性触发器。 请注意, 编辑器的 "**触发器" 面板**已<xref:System.Windows.UIElement.Opacity%2A>将更改为 100%。  
  
     ![“触发器”面板](./media/custom-button-blend-propertytriggerinfo.png "custom_button_blend_PropertyTriggerInfo")  
  
     按 F5 运行应用程序, 并将鼠标指针移到按钮的上方和下方。 当鼠标悬停在按钮上并在指针离开时消失时, 应会看到玻璃层。  
  
4. **System.windows.uielement.ismouseover 触发器笔划值更改:** 让我们将其他一些操作与<xref:System.Windows.UIElement.IsMouseOver%2A>触发器相关联。 录制继续时, 请将所选内容从**glassCube**切换到**outerRectangle**。 然后, 将<xref:System.Windows.Shapes.Shape.Stroke%2A> **outerRectangle**的设置为自定义表达式 "{DynamicResource {x:Static SystemColors. HighlightBrushKey}}"。 这会将<xref:System.Windows.Shapes.Shape.Stroke%2A>设置为按钮所使用的典型突出显示颜色。 当鼠标悬停在按钮上时, 请按 F5 查看效果。  
  
     ![如何将笔划设置为突出显示颜色](./media/custom-button-blend-ismousedoverpropertytrigger3.png "custom_button_blend_IsMousedOverPropertyTrigger3")  
  
5. **System.windows.uielement.ismouseover 触发模糊文本:** 让我们将另一个操作与<xref:System.Windows.UIElement.IsMouseOver%2A>属性触发器关联起来。 当玻璃出现在屏幕上时, 使该按钮的内容看起来很模糊。 为此, 我们可以将模糊<xref:System.Windows.Media.Effects.BitmapEffect>应用<xref:System.Windows.Controls.ContentPresenter>到 (**myContentPresenter**)。  
  
     ![如何对按钮内容进行模糊](./media/custom-button-blend-propertytriggerwithbitmapeffect.png "custom_button_blend_PropertyTriggerWithBitMapEffect")  
  
    > [!NOTE]
    > 若要在执行<xref:System.Windows.Media.Effects.BitmapEffect>搜索之前返回 "**属性" 面板**, 请清除**搜索框**中的文本。  
  
     此时, 我们使用了具有多个相关操作的属性触发器来创建鼠标指针进入和离开按钮区域时的突出显示行为。 按钮的另一种典型行为是在焦点突出显示时突出显示。 可以通过为<xref:System.Windows.UIElement.IsFocused%2A>属性添加另一个属性触发器来添加此类行为。  
  
6. **为 IsFocused 创建属性触发器:** 使用与相同的<xref:System.Windows.UIElement.IsMouseOver%2A>过程 (请参阅本部分的第一步), 为<xref:System.Windows.UIElement.IsFocused%2A>属性创建另一个属性触发器。 当**触发器记录为 on**时, 将以下操作添加到触发器:  
  
    - **glassCube**获取<xref:System.Windows.UIElement.Opacity%2A> 100% 的。  
  
    - **outerRectangle**获取<xref:System.Windows.Shapes.Shape.Stroke%2A>自定义表达式值 "{DynamicResource {x:Static SystemColors. HighlightBrushKey}}"。  
  
 作为本演练的最后一步, 我们将向按钮添加动画。 这些动画将由事件 (具体而言<xref:System.Windows.UIElement.MouseEnter>是和<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件) 触发。  
  
#### <a name="to-use-event-triggers-and-animations-to-add-interactivity"></a>使用事件触发器和动画添加交互性  
  
1. **创建 MouseEnter 事件触发器:** 添加新的事件触发器, 并<xref:System.Windows.UIElement.MouseEnter>选择作为要在触发器中使用的事件。  
  
     ![如何创建 MouseEnter 事件触发器](./media/custom-button-blend-mouseovereventtrigger.png "custom_button_blend_MouseOverEventTrigger")  
  
2. **创建动画时间线:** 接下来, 将动画时间线与<xref:System.Windows.UIElement.MouseEnter>事件关联。  
  
     ![如何向事件添加动画时间线](./media/custom-button-blend-mouseovereventtrigger2.png "custom_button_blend_MouseOverEventTrigger2")  
  
     按 **"确定"** 创建新的时间线后, "**时间线" 面板**将显示并在设计面板中显示 "时间线录制已打开"。 这意味着我们可以在时间线中开始记录属性更改 (对属性更改进行动画处理)。  
  
    > [!NOTE]
    > 可能需要调整窗口和/或面板的大小以查看显示。  
  
     ![时间线面板](./media/custom-button-blend-mouseovereventtrigger3.png "custom_button_blend_MouseOverEventTrigger3")  
  
3. **创建关键帧:** 若要创建动画, 请选择要进行动画处理的对象, 在时间线上创建两个或更多关键帧, 并为这些关键帧设置要在其中插入动画的属性值。 下图指导您创建关键帧。  
  
     ![如何创建关键帧](./media/custom-button-blend-mouseovereventtrigger4.png "custom_button_blend_MouseOverEventTrigger4")  
  
4. **收缩此关键帧中的 glassCube:** 选择第二个关键帧后, 使用**大小转换**将**glassCube**的大小缩小到其完整大小的 90%。  
  
     ![如何缩小按钮的大小](./media/custom-button-blend-sizetransform.png "custom_button_blend_SizeTransform")  
  
     按 F5 运行该应用程序。 将鼠标指针移到按钮上。 请注意, 玻璃层会在按钮上缩小。  
  
5. **创建另一个事件触发器并将不同的动画与之关联:** 让我们再添加一个动画。 使用类似的过程来创建上一个事件触发器动画:  
  
    1. 使用<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件创建新的事件触发器。  
  
    2. 将新时间线与<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件关联。  
  
     ![如何创建新的时间线](./media/custom-button-blend-clickeventtrigger1.png "custom_button_blend_ClickEventTrigger1")  
  
    1. 对于此时间线, 请创建两个关键帧, 一个为0.0 秒, 第二个关键帧0.3 秒。  
  
    2. 突出显示处于0.3 秒的关键帧后, 将**旋转变换角度**设置为360度。  
  
     ![如何创建旋转变换](./media/custom-button-blend-rotatetransform.gif "custom_button_blend_RotateTransform")  
  
    1. 按 F5 运行该应用程序。 单击按钮。 请注意, 玻璃层会旋转。  
  
## <a name="conclusion"></a>结束语  
 已完成自定义按钮。 使用应用于应用程序中所有按钮的按钮模板执行此操作。 如果你退出模板编辑模式 (请参阅下图) 并创建更多按钮, 你将看到它们的外观和行为类似于自定义按钮, 而不像 "默认" 按钮。  
  
 ![自定义按钮模板](./media/custom-button-blend-scopeup.gif "custom_button_blend_ScopeUp")  
  
 ![使用相同模板的多个按钮](./media/custom-button-blend-createmultiplebuttons.png "custom_button_blend_CreateMultipleButtons")  
  
 按 F5 运行该应用程序。 单击按钮, 并注意它们的行为方式如何。  
  
 请记住, 在自定义模板时, 可以将<xref:System.Windows.Shapes.Shape.Fill%2A> <xref:System.Windows.Shapes.Shape.Stroke%2A> **innerRectangle**的属性和**outerRectangle**属性设置为模板背景 ({TemplateBinding background})。 因此, 在设置各个按钮的背景色时, 设置的背景将用于各自的属性。 立即尝试更改背景。 在下图中, 使用了不同的渐变。 因此, 尽管模板对控件 (如按钮) 的整体自定义很有用, 但仍可以修改具有模板的控件, 使其看起来彼此不同。  
  
 ![具有相同模板的按钮外观](./media/custom-button-blend-blendconclusion.jpg "custom_button_blend_BlendConclusion")  
  
 总之, 在自定义按钮模板的过程中, 已了解如何在 Microsoft Expression Blend 中执行以下操作:  
  
- 自定义控件的外观。  
  
- 设置属性触发器。 属性触发器非常有用, 因为它们可在大多数对象 (而不仅仅是控件) 上使用。  
  
- 设置事件触发器。 事件触发器非常有用, 因为它们可在大多数对象 (而不仅仅是控件) 上使用。  
  
- 创建动画。  
  
- 其他: 创建渐变、添加 BitmapEffects、使用转换, 并设置对象的基本属性。  
  
## <a name="see-also"></a>请参阅

- [使用 XAML 创建按钮](walkthrough-create-a-button-by-using-xaml.md)
- [样式设置和模板化](styling-and-templating.md)
- [动画概述](../graphics-multimedia/animation-overview.md)
- [使用纯色和渐变进行绘制概述](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
- [位图效果概述](../graphics-multimedia/bitmap-effects-overview.md)
