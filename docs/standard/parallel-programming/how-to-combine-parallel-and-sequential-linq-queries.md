---
title: 如何：合并并行和顺序 LINQ 查询
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel queries, combine parallel and sequential
ms.assetid: 1167cfe6-c8aa-4096-94ba-c66c3a4edf4c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 026c7d2be678c4b6aeed4e2e6f9eb43283cd04c1
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988466"
---
# <a name="how-to-combine-parallel-and-sequential-linq-queries"></a>如何：合并并行和顺序 LINQ 查询
此示例展示了如何使用 <xref:System.Linq.ParallelEnumerable.AsSequential%2A> 方法，指示 PLINQ 顺序处理查询中的所有后续运算符。 尽管顺序处理通常比并行处理慢，但有时却是生成正确结果的必要条件。  
  
> [!WARNING]
> 本示例旨在演示用法，运行速度可能不如等效的顺序 LINQ to Objects 查询快。 若要详细了解加速，请参阅[了解 PLINQ 中的加速](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)。  
  
## <a name="example"></a>示例  
 下面的示例展示了一种需要 <xref:System.Linq.ParallelEnumerable.AsSequential%2A> 的情况，即暂留在旧查询子句中建立的顺序。  
  
 [!code-csharp[PLINQ#24](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#24)]
 [!code-vb[PLINQ#24](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#24)]  
  
## <a name="compiling-the-code"></a>编译代码  
 若要编译并运行此代码，请将它粘贴到 [PLINQ 数据样本](../../../docs/standard/parallel-programming/plinq-data-sample.md)项目中，添加用于从 `Main` 调用方法的代码行，再按 F5。  
  
## <a name="see-also"></a>请参阅

- [并行 LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
