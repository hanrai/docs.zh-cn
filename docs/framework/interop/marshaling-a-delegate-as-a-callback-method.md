---
title: 将委托作为回调方法进行封送
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data marshaling, Callback sample
- marshaling, Callback sample
ms.assetid: 6ddd7866-9804-4571-84de-83f5cc017a5a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2697950a371d66f2e57731e0ff01ed531a07955e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69946397"
---
# <a name="marshaling-a-delegate-as-a-callback-method"></a>将委托作为回调方法进行封送
此示例演示如何将委托传递给需要函数指针的非托管函数。 委托是可以容纳方法引用的类，等效于类型安全函数指针或回调函数。

> [!NOTE]
> 在调用内使用委托时，公共语言运行时防止在该调用的持续时间内对委托执行垃圾回收。 但是，如果非托管函数存储了该委托，以便在调用完成后使用，则必须手动防止垃圾回收，直到非托管函数结束对该委托的使用为止。 有关详细信息，请参阅 [HandleRef 示例](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/hc662t8k(v=vs.100))和 [GCHandle 示例](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/44ey4b32(v=vs.100))。

回调示例使用以下非托管函数（与其原始函数声明一同显示）：

- `TestCallBack` 从 PinvokeLib.dll 导出。

    ```cpp
    void TestCallBack(FPTR pf, int value);
    ```

- `TestCallBack2` 从 PinvokeLib.dll 导出。

    ```cpp
    void TestCallBack2(FPTR2 pf2, char* value);
    ```

[PinvokeLib.dll](marshaling-data-with-platform-invoke.md#pinvokelibdll) 是一种自定义的非托管库，包含上述函数的实现。

在此示例中，`LibWrap` 类包含 `TestCallBack` 和 `TestCallBack2` 方法的托管原型。 这两种方法都作为参数将委托传递给回调函数。 委托的签名必须匹配它引用的方法的签名。 例如，`FPtr` 和 `FPtr2`委托的签名与 `DoSomething` 和 `DoSomething2` 方法相同。

## <a name="declaring-prototypes"></a>声明原型
[!code-cpp[Conceptual.Interop.Marshaling#37](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/callback.cpp#37)]
[!code-csharp[Conceptual.Interop.Marshaling#37](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/callback.cs#37)]
[!code-vb[Conceptual.Interop.Marshaling#37](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/callback.vb#37)]

## <a name="calling-functions"></a>调用函数
[!code-cpp[Conceptual.Interop.Marshaling#38](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/callback.cpp#38)]
[!code-csharp[Conceptual.Interop.Marshaling#38](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/callback.cs#38)]
[!code-vb[Conceptual.Interop.Marshaling#38](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/callback.vb#38)]

## <a name="see-also"></a>请参阅

- [其他封送处理示例](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ss9sb93t(v=vs.100))
- [平台调用数据类型](marshaling-data-with-platform-invoke.md#platform-invoke-data-types)
- [在托管代码中创建原型](creating-prototypes-in-managed-code.md)
