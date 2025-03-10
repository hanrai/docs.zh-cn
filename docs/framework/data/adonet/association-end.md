---
title: 关联端
ms.date: 03/30/2017
ms.assetid: 2c345213-0296-4d90-ac6d-cef179798a75
ms.openlocfilehash: 575157cd1d125d3315e1859aad72cc8b08d8b4cf
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69932206"
---
# <a name="association-end"></a>关联端
*关联端*标识[关联](../../../../docs/framework/data/adonet/association-type.md)一端的[实体类型](../../../../docs/framework/data/adonet/entity-type.md)以及该关联端可以存在的实体类型实例的数量。 关联端定义为关联的一部分；关联必须正好有两个关联端。 [导航属性](../../../../docs/framework/data/adonet/navigation-property.md)允许从一个关联端导航到另一个关联端。  
  
 关联端定义包含以下信息：  
  
- 关联中涉及的实体类型之一。 （必需）  
  
    > [!NOTE]
    > 对于某个给定的关联，为每个关联端指定的实体类型可以是相同的。 这将创建一个自关联。  
  
- 一个[关联端多重性](../../../../docs/framework/data/adonet/association-end-multiplicity.md), 指示可以位于关联一端的实体类型实例的数量。 Association 端重数的值可以为一 (1)、零或一 (0 ..1) 或多 (\*)。  
  
- 关联端的名称。 （可选）  
  
- 有关在关联端上执行的操作的信息，例如级联删除。 （可选）  
  
## <a name="example"></a>示例  
 下图显示了一个具有两个关联的概念模型：`PublishedBy` 和 `WrittenBy`。 `PublishedBy` 关联的关联端是 `Book` 和 `Publisher` 实体类型。 `Publisher` End 的重数为一 (1), 而`Book`结尾的重数为多 (\*), 这表示发布者发布了许多书籍, 书籍发布了一个出版商。  
  
 ![具有三个实体类型的示例模型](./media/association-end/example-model-three-entity-types.gif)  
  
 ADO.NET 实体框架使用一种称为概念架构定义语言 ([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)) 的域特定语言 (DSL) 来定义概念模型。 下面的 CSDL 定义了上图中显示的 `PublishedBy` 关联。 请注意，每个关联端的类型、名称和重数由 XML 特性指定（分别是 `Type`、`Role` 和 `Multiplicity` 特性）。 有关在端上执行的操作的可选信息在 XML 元素（`OnDelete` 元素）中指定。 在本例中，如果删除出版商，将同时删除所有关联的书籍。  
  
 [!code-xml[EDM_Example_Model#AssociationEnd](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books3.edmx#associationend)]  
  
## <a name="see-also"></a>请参阅

- [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)
- [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)
