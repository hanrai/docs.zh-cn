---
title: 在数据集中使用 XML
ms.date: 03/30/2017
ms.assetid: 35138159-e199-49ec-baf7-1ec6777e171e
ms.openlocfilehash: ba68f0fbe84a9877596ddfefd56f71a5889cf8de
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70203137"
---
# <a name="using-xml-in-a-dataset"></a>在数据集中使用 XML
通过 ADO.NET，您可以从 XML 流或文档填充 <xref:System.Data.DataSet>。 可以使用 XML 流或文档向 <xref:System.Data.DataSet> 提供数据和/或架构信息。 从 XML 流或文档中提供的信息可以与已存在于 <xref:System.Data.DataSet> 中的现有数据或架构信息进行组合。  
  
 为了通过 HTTP 将 <xref:System.Data.DataSet> 传输给其他应用程序或启用了 XML 的平台来使用，ADO.NET 还允许您创建 <xref:System.Data.DataSet> 的 XML 表示形式（包含或不包含架构）。 在 <xref:System.Data.DataSet> 的 XML 表示形式中，数据以 XML 形式编写，而架构若以内联形式包含在该表示形式中时，则使用 XML 架构定义语言 (XSD) 来编写。 XML 和 XML 架构提供一种方便的格式与远程客户端之间来回传输 <xref:System.Data.DataSet> 的内容。  
  
## <a name="in-this-section"></a>本节内容  
 [DiffGrams](diffgrams.md)  
 提供有关 DiffGram 的详细信息，DiffGram 是一种用于读写 <xref:System.Data.DataSet> 内容的 XML 格式。  
  
 [从 XML 加载数据集](loading-a-dataset-from-xml.md)  
 讨论在从 XML 文档中加载 <xref:System.Data.DataSet> 内容时需考虑的不同选项。  
  
 [以 XML 数据的形式编写数据集内容](writing-dataset-contents-as-xml-data.md)  
 讨论如何以 XML 数据的形式生成 <xref:System.Data.DataSet> 的内容以及可使用的不同 XML 格式选项。  
  
 [从 XML 加载数据集构架信息](loading-dataset-schema-information-from-xml.md)  
 讨论用于从 XML 中加载 <xref:System.Data.DataSet> 架构的 <xref:System.Data.DataSet> 方法。  
  
 [以 XSD 的形式写入数据集构架信息](writing-dataset-schema-information-as-xsd.md)  
 讨论 XML 架构的用途以及如何从 <xref:System.Data.DataSet> 生成 XML 架构。  
  
 [数据集和 XmlDataDocument 同步](dataset-and-xmldatadocument-synchronization.md)  
 讨论 .NET Framework 中提供的同步访问单个数据集的关系和分层视图的功能，并解释如何在 <xref:System.Data.DataSet> 和 <xref:System.Xml.XmlDataDocument> 之间创建同步关系。  
  
 [嵌套 DataRelation](nesting-datarelations.md)  
 讨论嵌套 <xref:System.Data.DataRelation> 对象在以 XML 数据形式表示 <xref:System.Data.DataSet> 内容时的重要性，并描述如何创建这些对象。  
  
 [从 XML 架构派生数据集关系结构 (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 描述从 XML 架构创建的 <xref:System.Data.DataSet> 的关系结果（即架构）。  
  
 [从 XML 推断数据集关系结构](inferring-dataset-relational-structure-from-xml.md)  
 描述在从 XML 元素进行推断时所创建的 <xref:System.Data.DataSet> 的结果关系结构（即架构）。  
  
## <a name="related-sections"></a>相关章节  
 [ADO.NET 概述](../ado-net-overview.md)  
 描述 ADO.NET 结构和组件，并说明如何使用它们来访问现有的数据源和管理应用程序数据。  
  
## <a name="see-also"></a>请参阅

- [数据集、数据表和数据视图](index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
