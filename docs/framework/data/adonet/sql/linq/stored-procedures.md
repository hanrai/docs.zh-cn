---
title: 存储过程
ms.date: 03/30/2017
ms.assetid: 4d23dd7a-a85f-44ff-a717-af7d0950c0fc
ms.openlocfilehash: b06dc19aa8b767da6a1c6b00bd5b465465db6060
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67742845"
---
# <a name="stored-procedures"></a>存储过程
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 在您的对象模型中使用方法来表示数据库中的存储的过程。 您可以通过应用 <xref:System.Data.Linq.Mapping.FunctionAttribute> 属性和 <xref:System.Data.Linq.Mapping.ParameterAttribute> 属性（如果需要）将方法指定为存储过程。 有关详细信息，请参阅[LINQ to SQL 对象模型](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)。  
  
 使用 Visual Studio 的开发人员通常会使用对象关系设计器来映射存储的过程。 本节中的主题说明了在您自行编写代码的情况下，如何在您的应用程序中构建和调用这些方法。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：返回行集](../../../../../../docs/framework/data/adonet/sql/linq/how-to-return-rowsets.md)  
 介绍如何返回数据行并说明如何使用输入参数。  
  
 [如何：使用采用参数的存储的过程](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-stored-procedures-that-take-parameters.md)  
 介绍如何使用输入和输出参数。  
  
 [如何：使用针对多个结果形状映射的存储的过程](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-stored-procedures-mapped-for-multiple-result-shapes.md)  
 介绍如何实现在同一存储过程中返回多个形状。  
  
 [如何：使用针对顺序结果形状映射的存储的过程](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-stored-procedures-mapped-for-sequential-result-shapes.md)  
 介绍如何在返回顺序已知的情况下提供多个形状。  
  
 [通过使用存储过程自定义操作](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures.md)  
 介绍如何使用存储过程来实现插入、更新和删除操作。  
  
 [通过仅使用存储过程自定义操作](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures-exclusively.md)  
 介绍如何只使用存储过程来实现插入、更新和删除操作。  
  
## <a name="related-sections"></a>相关章节  
 [编程指南](../../../../../../docs/framework/data/adonet/sql/linq/programming-guide.md)  
 提供有关如何创建和使用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 对象模型的信息。  
  
 [演练：仅使用存储过程 (Visual Basic)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-using-only-stored-procedures-visual-basic.md)  
 包含了演示如何在 Visual Basic 中使用存储过程的步骤。  
  
 [演练：仅使用存储过程 (C#)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-using-only-stored-procedures-csharp.md)  
 包含了演示如何在 C# 中使用存储过程的步骤。
