---
title: 推断关系
ms.date: 03/30/2017
ms.assetid: 8fa86a9d-6545-4a9d-b1f5-58d9742179c7
ms.openlocfilehash: 92a4953dc7f5119ffbf171ff2a7bf5b58e896638
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70204767"
---
# <a name="inferring-relationships"></a>推断关系
如果被推断为表的元素具有一个同样被推断为表的子元素，则将在这两个表之间创建 <xref:System.Data.DataRelation>。 名称为**ParentTableName_Id**的新列将添加到为父元素创建的表和为子元素创建的表中。 此标识列的**ColumnMapping**属性将设置为**mappingtype.attribute**。 列将是父表的自动递增主键, 并将用于这两个表之间的**DataRelation** 。 添加的标识列的数据类型将为 system.exception, 这与所有其他推断列的数据类型不同, 后者为**system.string**。 还<xref:System.Data.ForeignKeyConstraint>将使用父表和子表中的新列来创建具有**DeleteRule** = **级联**的。  
  
 例如，考虑以下 XML：  
  
```xml  
<DocumentElement>  
  <Element1>  
    <ChildElement1 attr1="value1" attr2="value2"/>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 推理过程将生成两个表：**Element1**和**ChildElement1**。  
  
 **Element1**表包含两列:**Element1_Id**和**ChildElement2**。 **Element1_Id**列的**ColumnMapping**属性将设置为**mappingtype.attribute**。 **ChildElement2**列的**ColumnMapping**属性将设置为**mappingtype.attribute**。 **Element1_Id**列将设置为**Element1**表的主键。  
  
 **ChildElement1**表包含三列: **attr1**、 **attr2**和**Element1_Id**。 **Attr1**和**Attr2**列的**ColumnMapping**属性将设置为**mappingtype.attribute**。 **Element1_Id**列的**ColumnMapping**属性将设置为**mappingtype.attribute**。  
  
 将使用两个表中的**Element1_Id**列创建**DataRelation**和**ForeignKeyConstraint** 。  
  
 **集会**DocumentElement  
  
 **数据表**Element1  
  
|Element1_Id|ChildElement2|  
|------------------|-------------------|  
|0|Text2|  
  
 **数据表**ChildElement1  
  
|attr1|attr2|Element1_Id|  
|-----------|-----------|------------------|  
|value1|value2|0|  
  
 **DataRelation**Element1_ChildElement1  
  
 **ParentTable**Element1  
  
 **ParentColumn**Element1_Id  
  
 **ChildTable**ChildElement1  
  
 **ChildColumn**Element1_Id  
  
 **嵌**True  
  
 **ForeignKeyConstraint**Element1_ChildElement1  
  
 **该列**Element1_Id  
  
 **ParentTable**Element1  
  
 **ChildTable**ChildElement1  
  
 **DeleteRule**Cascade  
  
 **AcceptRejectRule**无  
  
## <a name="see-also"></a>请参阅

- [从 XML 推断数据集关系结构](inferring-dataset-relational-structure-from-xml.md)
- [从 XML 加载数据集](loading-a-dataset-from-xml.md)
- [从 XML 加载数据集构架信息](loading-dataset-schema-information-from-xml.md)
- [嵌套 DataRelation](nesting-datarelations.md)
- [在数据集中使用 XML](using-xml-in-a-dataset.md)
- [数据集、数据表和数据视图](index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
