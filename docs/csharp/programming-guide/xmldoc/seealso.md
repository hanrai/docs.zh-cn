---
title: <seealso> - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- cref
- <seealso>
- seealso
helpviewer_keywords:
- cref [C#], see also
- seealso C# XML tag
- cref [C#]
- cross-references [C#], tags
- <seealso> C# XML tag
ms.assetid: 8e157f3f-f220-4fcf-9010-88905b080b18
ms.openlocfilehash: 3ddaa7efec2b4bf5ffa53971aa6f380a1be9bad8
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69587655"
---
# <a name="seealso-c-programming-guide"></a>\<seealso>（C# 编程指南）
## <a name="syntax"></a>语法  
  
```xml  
<seealso cref="member"/>  
```  
  
## <a name="parameters"></a>参数  
 cref = " `member`"  
 对可从当前编译环境调用的成员或字段的引用。 编译器检查是否存在给定的码位元素，并将 `member` 传递到输出 XML 中的元素名称。`member` 必须在双引号 (" ") 内。  
  
 有关如何创建对泛型类型的 cref 引用的信息，请参阅 [\<see>](./see.md)。  
  
## <a name="remarks"></a>备注  
 使用 \<seealso> 标记，可以指定想要在“另请参阅”部分中显示的文本。 使用 [\<see>](./see.md) 从文本内指定链接。  
  
 使用 [/doc](../../language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
## <a name="example"></a>示例  
 有关使用 \<seealso> 的示例，请参阅 [\<summary>](./summary.md)。  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../index.md)
- [建议的文档注释标记](./recommended-tags-for-documentation-comments.md)
