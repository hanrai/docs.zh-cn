---
title: 如何：折叠和隐藏代码段 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic, code collapsing
- Visual Basic, code hiding
- Visual Basic code, collapsing and hiding
ms.assetid: b770e8f5-e07d-491a-ab4b-a977980f9ba2
ms.openlocfilehash: db396adf24c12542f720d3b235068aea2329288d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69949735"
---
# <a name="how-to-collapse-and-hide-sections-of-code-visual-basic"></a>如何：折叠和隐藏代码段 (Visual Basic)
`#Region`指令使你可以折叠和隐藏 Visual Basic 文件中的代码段。 使用`#Region`指令, 可以指定在使用 Visual Studio code 编辑器时可展开或折叠的代码块。 可以有选择地隐藏代码, 使文件更易于管理且更易于阅读。 有关详细信息，请参阅[大纲显示](/visualstudio/ide/outlining)。  
  
 `#Region`指令支持代码块语义, `#If...#End If`如。 这意味着它们不能以一个块开始, 并在另一个块中结束;开始和结束必须在同一个块中。 `#Region`函数内不支持指令。  
  
### <a name="to-collapse-and-hide-a-section-of-code"></a>折叠和隐藏代码段  
  
- 将代码段放置在`#Region`和`#End Region`语句之间, 如以下示例中所示:  
  
     [!code-vb[VbVbalrConditionalComp#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#6)]  
  
     `#Region`块可以在一个代码文件中多次使用; 因此, 用户可以定义自己的过程和类块, 进而可以进行折叠。 `#Region`块还可以嵌套在其他`#Region`块内。  
  
    > [!NOTE]
    > 隐藏代码不会阻止编译代码, 也不会影响`#If...#End If`语句。  
  
## <a name="see-also"></a>请参阅

- [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
- [#Region 指令](../../../visual-basic/language-reference/directives/region-directive.md)
- [#If...Then...#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
- [大纲显示](/visualstudio/ide/outlining)
