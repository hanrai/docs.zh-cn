---
title: 如何：使用采用参数的存储过程
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b935fd84-cb9c-4205-8c48-658d5db2ec93
ms.openlocfilehash: 17ae74a430df4d4a4670c2390ce7b2ee25b67c7a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69938703"
---
# <a name="how-to-use-stored-procedures-that-take-parameters"></a>如何：使用采用参数的存储过程
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 将输出参数映射到引用参数，并且对于值类型，它将参数声明为可以为 null。  
  
 有关如何在返回行集的查询中使用输入参数的示例, 请参阅[如何:返回行](../../../../../../docs/framework/data/adonet/sql/linq/how-to-return-rowsets.md)集。  
  
## <a name="example"></a>示例  
 下面的示例带有单个输入参数（客户 ID）并返回一个输出参数（该客户的总销售额）。  
  
```  
CREATE PROCEDURE [dbo].[CustOrderTotal]   
@CustomerID nchar(5),  
@TotalSales money OUTPUT  
AS  
SELECT @TotalSales = SUM(OD.UNITPRICE*(1-OD.DISCOUNT) * OD.QUANTITY)  
FROM ORDERS O, "ORDER DETAILS" OD  
where O.CUSTOMERID = @CustomerID AND O.ORDERID = OD.ORDERID  
```  
  
 [!code-csharp[DLinqSprox#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#2)]
 [!code-vb[DLinqSprox#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#2)]  
  
## <a name="example"></a>示例  
 您将按如下方式调用此存储过程：  
  
 [!code-csharp[DLinqSprox#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/Program.cs#3)]
 [!code-vb[DLinqSprox#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/Module1.vb#3)]  
  
## <a name="see-also"></a>请参阅

- [存储过程](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)
- [下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)
- [使用可以为 null 的类型](../../../../../csharp/programming-guide/nullable-types/using-nullable-types.md)
- [可以为 null 的值类型](../../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
