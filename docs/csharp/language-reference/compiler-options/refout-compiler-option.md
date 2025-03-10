---
title: -refout（C# 编译器选项）
ms.date: 08/08/2017
f1_keywords:
- /refout
helpviewer_keywords:
- refout compiler option [C#]
- /refout compiler option [C#]
- -refout compiler option [C#]
ms.openlocfilehash: 97cbf540527d0449387b71bb1d97df95b6a4aba4
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69602507"
---
# <a name="-refout-c-compiler-options"></a>-refout（C# 编译器选项）

-refout 选项指定应输出引用程序集的文件路径  。 这在 Emit API 中转换为 `metadataPeStream`。 此选项对应于 MSBuild 的 [ProduceReferenceAssembly](/visualstudio/msbuild/common-msbuild-project-properties) 项目属性。

## <a name="syntax"></a>语法

```console
-refout:filepath
```

## <a name="arguments"></a>自变量

 `filepath` - 引用程序集的文件路径。 通常情况下，应与主程序集的路径匹配。 推荐约定（MSBuild 采用）是，将引用程序集放入与主程序集相关的“ref/”子文件夹中。

## <a name="remarks"></a>备注

仅包含元数据的程序集会将方法主体替换为一个 `throw null` 主体，但包括除匿名类型以外的所有成员。 使用 `throw null` 主体（而非不使用主体）的原因在于，这样做可以运行和传递 PEVerify（从而验证元数据的完整性）。

引用程序集包括程序集级 `ReferenceAssembly` 属性。 可以在源中指定此属性（之后编译器就不需要进行合成）。 由于有此属性，运行时会拒绝加载用于执行的引用程序集（但仍可在仅限反射的模式下加载）。 在程序集上反射的工具需要确保仅将引用程序集加载为反射模式，否则将生成运行时 typeload 错误。

引用程序集进一步从仅包含元数据的程序集中删除元数据（私有成员）：

- 引用程序集只包含在 API 外围应用中所需的引用。 实际程序集可能包含与特定实现相关的其他引用。 例如，`class C { private void M() { dynamic d = 1; ... } }` 的引用程序集不引用 `dynamic` 所需的任何类型。
- 删除私有函数成员（方法、属性和事件），前提是这不会对编译造成显著影响。 如果没有 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性，也请删除内部函数成员。
- 但保留引用程序集中的所有类型（包括私有或嵌套类型）。 保留所有属性（甚至是内部属性）。
- 保留所有虚拟方法。 保留显式接口实现。 保留显式实现的属性和事件，因为它们的访问器是虚拟的（因此予以保留）。
- 保留结构的所有字段。 （这是 post-C#-7.1 优化候选项）

`-refout` 和 [`-refonly`](refonly-compiler-option.md) 选项互斥。

## <a name="see-also"></a>请参阅

- [C# 编译器选项](./index.md)
- [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)
