---
title: 如何：使用通道工厂以异步方式调用操作
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cc17dd47-b9ad-451c-a362-e36e0aac7ba0
ms.openlocfilehash: 3080514d06119a2f1b621cff16056ac7577c30b3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966807"
---
# <a name="how-to-call-operations-asynchronously-using-a-channel-factory"></a>如何：使用通道工厂以异步方式调用操作
本主题介绍客户端如何在使用基于 <xref:System.ServiceModel.ChannelFactory%601> 的客户端应用程序时以异步方式访问服务操作。 （当使用 <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType> 对象调用服务时，可以使用事件驱动的异步调用模型。 有关详细信息，请参阅[如何：异步](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)调用服务操作。 有关基于事件的异步调用模型的详细信息, 请参阅[基于事件的异步模式 (EAP)](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)。)  
  
 本主题中的服务可实现 `ICalculator` 接口。 客户端可以在此接口上以异步方式调用操作，这意味着像 `Add` 这样的操作将拆分为两个方法：`BeginAdd` 和 `EndAdd`。前一个方法启动调用，而后一个方法在操作完成时检索结果。 有关演示如何在服务中异步实现操作的示例, 请参阅[如何:实现异步服务操作](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md)。 有关同步和异步操作的详细信息, 请参阅[同步和异步操作](../../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)。  
  
## <a name="procedure"></a>过程  
  
#### <a name="to-call-wcf-service-operations-asynchronously"></a>以异步方式调用 WCF 服务操作  
  
1. 运行带`/async`选项的[svcutil.exe 元数据实用工具 ()](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)工具, 如以下命令所示。  
  
    ```  
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a  
    ```  
  
     这将生成该操作的服务协定的异步客户端版本。  
  
2. 创建一个异步操作完成时将要调用的回调函数，如下面的示例代码所示。  
  
     [!code-csharp[C_How_To_CF_Async#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#2)]
     [!code-vb[C_How_To_CF_Async#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#2)]  
  
3. 若要以异步方式访问服务操作，请创建客户端、调用 `Begin[Operation]`（例如 `BeginAdd`），并指定一个回调函数，如下面的示例代码所示。  
  
     [!code-csharp[C_How_To_CF_Async#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/client.cs#3)]
     [!code-vb[C_How_To_CF_Async#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/client.vb#3)]  
  
     执行该回调函数时，客户端将调用 `End<operation>`（例如 `EndAdd`）以检索结果。  
  
## <a name="example"></a>示例  
 上面过程中的客户端代码使用的服务可实现 `ICalculator` 接口，如下面的代码所示。 在服务端, 协定的`Add`和`Subtract`操作由 Windows Communication Foundation (WCF) 运行时同步调用, 即使前面的客户端步骤是在客户端上异步调用的。 在服务端，`Multiply` 和 `Divide` 操作用于在服务端以异步方式调用服务，即使客户端以同步方式调用这两个操作也是如此。 此示例将 <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> 属性设置为 `true`。 此属性设置与 .NET Framework 异步模式的实现相结合, 告诉运行时异步调用操作。  
  
 [!code-csharp[C_How_To_CF_Async#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_how_to_cf_async/cs/service.cs#4)]
 [!code-vb[C_How_To_CF_Async#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_how_to_cf_async/vb/service.vb#4)]  
