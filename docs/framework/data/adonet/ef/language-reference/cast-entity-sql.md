---
title: CAST (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 07b6d750-dfd4-48a9-b86c-3badcbba6f70
ms.openlocfilehash: 253dcf092deadd1049d0556af4ea0630602110d0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69935817"
---
# <a name="cast-entity-sql"></a>CAST (Entity SQL)
将一种数据类型的表达式转换为另一种数据类型的表达式。  
  
## <a name="syntax"></a>语法  
  
```  
CAST ( expression AS data_type )  
```  
  
## <a name="arguments"></a>自变量  
 `expression`  
 任何可转换为 `data_type`的有效表达式。  
  
 `data_type`  
 系统提供的目标数据类型。 该类型必须为基元（标量）类型。 使用的 `data_type` 取决于查询空间。 如果使用 <xref:System.Data.EntityClient.EntityCommand>执行查询，则数据类型为概念模型中定义的类型。 有关详细信息，请参阅 [CSDL Specification](../../../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)。 如果使用 <xref:System.Data.Objects.ObjectQuery%601>执行查询，则数据类型为公共语言运行库 (CLR) 类型。  
  
## <a name="return-value"></a>返回值  
 返回与 `data_type`相同的值。  
  
## <a name="remarks"></a>备注  
 强制转换表达式的语义类似于 Transact-sql 转换表达式。 强制转换表达式用于将一种类型的值转换为另一种类型的值。  
  
```  
CAST( e as T )  
```  
  
 如果 e 具有某种类型 S，且 S 可转换为 T，则上面的表达式是有效的强制转换表达式。 T 必须为基元（标量）类型。  
  
 精度和标量方面的值可以选择在强制转换为 `Edm.Decimal`时提供。 如果未显式提供，则精度和标量的默认值分别为 18 和 0。 具体而言， `Decimal`支持以下重载：  
  
- `CAST( d as Edm.Decimal );`  
  
- `CAST( d as Edm.Decimal(precision) );`  
  
- `CAST( d as Edm.Decimal(precision, scale) );`  
  
 使用强制转换表达式视为显式转换。 显式转换可能截断数据或丧失精度。  
  
> [!NOTE]
> 仅对基元类型和枚举成员类型支持 CAST。  
  
## <a name="example"></a>示例  
 下面的 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查询使用 CAST 运算符将一种数据类型的表达式强制转换为另一种数据类型的表达式。 此查询基于 AdventureWorks 销售模型。 若要编译并运行此查询，请执行下列步骤：  
  
1. [按照如何:执行返回 PrimitiveType 结果](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md)的查询。  
  
2. 将以下查询作为参数传递给 `ExecutePrimitiveTypeQuery` 方法：  
  
 [!code-csharp[DP EntityServices Concepts 2#CAST](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#cast)]  
  
## <a name="see-also"></a>请参阅

- [实体 SQL 引用](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
