---
title: 如何：标签语句 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- colons (:)
- statements [Visual Basic], labels
- ': separator character'
- Visual Basic code, labeling statements
ms.assetid: 38f1ff43-2054-42cb-963b-1998e60c6ed4
ms.openlocfilehash: 6b442b5a0ad731cfc490a7387c78ac9279dddaf0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69961325"
---
# <a name="how-to-label-statements-visual-basic"></a>如何：标签语句 (Visual Basic)
语句块由用冒号分隔的代码行组成。 以标识字符串或整数开头的代码行称为 "*标记*"。 语句标签用于标记代码行, 以将其标识为与等`On Error Goto`语句一起使用。  
  
 标签可以是有效 Visual Basic 标识符 (如标识编程元素的标识符), 也可以是整数文本。 标签必须出现在源代码行的开头, 并且必须后跟一个冒号, 而不考虑它是否后跟同一行中的语句。  
  
 编译器通过检查行首是否与任何已定义的标识符匹配来标识标签。 如果不是, 编译器将假定它是一个标签。  
  
 标签具有自己的声明空间, 不会干扰其他标识符。 标签的范围是方法的主体。 标签声明优先于任何不明确的情况。  
  
> [!NOTE]
> 标签只能用于方法中的可执行语句。  
  
### <a name="to-label-a-line-of-code"></a>为代码行添加标签  
  
- 在源代码行的开头放置一个标识符, 后跟一个冒号。  
  
     例如, 以下代码行分别标记有`Jump`和: `120`  
  
     [!code-vb[VbVbalrStatements#708](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#708)]  
  
## <a name="see-also"></a>请参阅

- [语句](../../../visual-basic/programming-guide/language-features/statements.md)
- [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
