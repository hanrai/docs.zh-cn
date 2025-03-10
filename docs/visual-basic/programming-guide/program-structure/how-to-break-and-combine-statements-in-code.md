---
title: 如何：在代码中中断和组合语句 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb._
helpviewer_keywords:
- colons (:)
- line continuation
- _ line-continuation character
- ': line separator character'
- Visual Basic code, line breaks in
- Visual Basic code, line breaks
- Visual Basic code, line continuation
- long lines of code
- line terminator
- line-continuation sequence
- underscores [Visual Basic], in code
- statements [Visual Basic], line continuation in
- line breaks [Visual Basic], in code
- line-continuation character [Visual Basic]
- Visual Basic code, line continuation in
- statements [Visual Basic], line breaks in
ms.assetid: dea01dad-a8ac-484a-bb3a-8c45a1b1eccc
ms.openlocfilehash: 745974523bd747dd23f3cfaf7cb70bb6cd4513f0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69946204"
---
# <a name="how-to-break-and-combine-statements-in-code-visual-basic"></a>如何：在代码中中断和组合语句 (Visual Basic)
编写代码时, 有时可能会创建需要在代码编辑器中水平滚动的冗长语句。 尽管这不会影响你的代码的运行方式, 但当你或其他人在监视器上显示的代码时, 这会很难。 在这种情况下, 应考虑将单个长语句分解为多行。  
  
### <a name="to-break-a-single-statement-into-multiple-lines"></a>将单个语句分解为多行  
  
- 在您希望行中断的位置使用以下划线 (`_`) 开头的行继续符。 该下划线必须紧跟在空格后，并且在它后面紧跟行终止符（回车）。  
  
    > [!NOTE]
    > 在某些情况下, 如果省略行继续符, 则 Visual Basic 编译器将在下一行代码中隐式地继续执行该语句。 有关可以省略行继续符的语法元素的列表, 请参阅[语句](../../../visual-basic/programming-guide/language-features/statements.md)中的 "隐式行继续符"。  
  
     在下面的示例中, 语句分为四行, 其中的行继续符用于终止除最后一行以外的所有行。  
  
     [!code-vb[VbVbcnConventions#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#20)]  
  
     使用此序列可以使代码更易于阅读, 无论是联机还是打印。  
  
     行继续符必须是行中的最后一个字符。 你不能在同一行上将它与其他任何内容一起跟随。  
  
     存在一些限制, 以使你可以使用行继续符;例如, 不能在参数名中间使用。 您可以使用行继续符来破坏参数列表, 但参数的各个名称必须保持不变。  
  
     不能使用行继续符继续注释。 编译器不会检查注释中的字符是否有特殊意义。 对于多行注释, 请在每行上重复注释`'`符号 ()。  
  
 尽管建议方法将每个语句置于单独的行上, 但 Visual Basic 也允许在同一行上放置多个语句。  
  
### <a name="to-place-multiple-statements-on-the-same-line"></a>在同一行上放置多个语句  
  
- 用冒号 (`:`) 分隔语句, 如以下示例中所示。  
  
     [!code-vb[VbVbcnConventions#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#10)]  
  
## <a name="see-also"></a>请参阅

- [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
- [语句](../../../visual-basic/programming-guide/language-features/statements.md)
