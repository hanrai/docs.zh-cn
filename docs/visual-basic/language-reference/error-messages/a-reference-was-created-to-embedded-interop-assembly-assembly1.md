---
title: 创建了对嵌入的互操作程序集“<assembly1>”的引用，因为程序集“<assembly2>”间接引用了该程序集
ms.date: 07/20/2015
f1_keywords:
- vbc40059
- bc40059
helpviewer_keywords:
- VBC40059
- BC40059
ms.assetid: 520e39cb-8ab6-46f5-aa00-08afd51b4b7c
ms.openlocfilehash: 0f7a136abb0e63e4b139b87c8f18ae3fcb99dbf9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69947753"
---
# <a name="a-reference-was-created-to-embedded-interop-assembly-assembly1-because-of-an-indirect-reference-to-that-assembly-from-assembly-assembly2"></a>已创建对嵌入的互操作程序集\<"assembly1 >" 的引用, 因为程序集 "\<assembly2 >" 间接引用了该程序集
创建了对嵌入的互操作程序集“\<assembly1>”的引用，因为程序集“\<assembly2>”间接引用了该程序集。 请考虑更改任一程序集上的“Embed Interop Types”属性。  
  
 已添加对 `Embed Interop Types` 属性设置为 `True` 的程序集 (assembly1) 的引用。 这指示编译器嵌入来自该程序集的互操作类型信息。 但是，编译器不能嵌入来自该程序集的互操作类型信息，因为引用的另一个程序集 (assembly2) 也引用该程序集 (assembly1)，并将 `Embed Interop Types` 属性设置为 `False`。  
  
> [!NOTE]
> 将程序集引用的 `Embed Interop Types` 属性设置为 `True`，其效果等同于使用命令行编译器的 `/link` 选项引用该程序集。  
  
 **错误 ID:** BC40059  
  
### <a name="to-address-this-warning"></a>解决此警告  
  
- 要嵌入这两个程序集的互操作类型信息，请将对 assembly1 的所有引用的 `Embed Interop Types` 属性设置为 `True`。  
  
- 若要删除警告，可以将 assembly1 的 `Embed Interop Types` 属性设置为 `False`。 在这种情况下, 互操作类型信息由主互操作程序集 (PIA) 提供。  
  
## <a name="see-also"></a>请参阅

- [/link (Visual Basic)](../../../visual-basic/reference/command-line-compiler/link.md)
- [与非托管代码交互操作](../../../framework/interop/index.md)
