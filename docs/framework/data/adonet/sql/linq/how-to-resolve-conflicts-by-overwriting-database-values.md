---
title: 如何：通过重写数据库值解决冲突
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fd6db0b8-c29c-48ff-b768-31d28e7a148c
ms.openlocfilehash: f6721234d2d3920343bc72889c7683fb6ee662a0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69928756"
---
# <a name="how-to-resolve-conflicts-by-overwriting-database-values"></a>如何：通过重写数据库值解决冲突
若要先协调预期数据库值与实际数据库值之间的差异，再尝试重新提交更改，则可以使用 <xref:System.Data.Linq.RefreshMode.KeepCurrentValues> 覆盖数据库值。 有关详细信息, 请[参阅乐观并发:概述](../../../../../../docs/framework/data/adonet/sql/linq/optimistic-concurrency-overview.md)。  
  
> [!NOTE]
> 在所有情况下，都会先通过从数据库中检索更新后的数据来刷新客户端上的记录。 此操作确保了下一次更新尝试将通过相同的并发检查。  
  
## <a name="example"></a>示例  
 在本方案中，当 User1 尝试提交更改时将引发 <xref:System.Data.Linq.ChangeConflictException> 异常，原因是 User2 同时已更改了 Assistant 和 Department 列。 下表说明了这种情况。  
  
||经理|Assistant|Department|  
|------|-------------|---------------|----------------|  
|原始数据库在被 User1 和 User2 查询时的状态。|Alfreds|Maria|销售额|  
|User1 准备提交这些更改。|Alfred||“营销”|  
|User2 已经提交了这些更改。||Mary|服务|  
  
 User1 决定通过用当前客户端成员值覆盖数据库值来解决此冲突。  
  
 User1 通过使用 <xref:System.Data.Linq.RefreshMode.KeepCurrentValues> 解决了此冲突后，数据库中的结果将如下表中所示：  
  
||经理|Assistant|Department|  
|------|-------------|---------------|----------------|  
|解决冲突后的新状态。|Alfred<br /><br /> （来自 User1）|Maria<br /><br /> （原始）|“营销”<br /><br /> （来自 User1）|  
  
 下面的示例代码演示了如何用当前客户端成员值覆盖数据库值。 （未对各个成员冲突进行检查或自定义处理。）  
  
 [!code-csharp[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#2)]
 [!code-vb[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#2)]  
  
## <a name="see-also"></a>请参阅

- [如何：管理更改冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)
