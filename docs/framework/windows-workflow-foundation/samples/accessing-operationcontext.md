---
title: 访问 OperationContext
ms.date: 03/30/2017
ms.assetid: 4e92efe8-7e79-41f3-b50e-bdc38b9f41f8
ms.openlocfilehash: 8d1c8543180a282a1b196393e5823dc3686aa16e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038409"
---
# <a name="accessing-operationcontext"></a>访问 OperationContext
此示例演示如何将消息传递活动<xref:System.ServiceModel.Activities.Receive> ( <xref:System.ServiceModel.Activities.Send>和) 与自定义作用域活动一起使用, <xref:System.ServiceModel.OperationContext.Current%2A>以便在传出消息或传入消息中访问和附加或检索自定义消息标头。  
  
## <a name="demonstrates"></a>演示  
 消息传递活动、<xref:System.ServiceModel.Activities.ISendMessageCallback>、<xref:System.ServiceModel.Activities.IReceiveMessageCallback>。  
  
## <a name="discussion"></a>讨论  
 此示例演示如何使用消息传递活动中的扩展性点（<xref:System.ServiceModel.Activities.ISendMessageCallback> 和 <xref:System.ServiceModel.Activities.IReceiveMessageCallback>）来访问 <xref:System.ServiceModel.OperationContext.Current%2A>。 在工作流运行时中，将回调注册为由消息传递活动在执行后选取的 <xref:System.Activities.IExecutionProperty> 的实现。 与该 <xref:System.Activities.IExecutionProperty> 实现处于同一范围内的任何消息传递活动都会受到影响。 特别是，此示例使用自定义范围活动来强制实施回调行为。 在客户端工作流中使用 <xref:System.ServiceModel.Activities.ISendMessageCallback> 可将工作流的 <xref:System.Activities.WorkflowApplication.Id%2A> 作为传出 <xref:System.ServiceModel.Channels.MessageHeader> 包含。 然后，在使用 <xref:System.ServiceModel.Activities.IReceiveMessageCallback> 的服务中选择此标头，并将此标头的值输出到控制台。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>设置、生成和运行示例  
  
1. 此示例使用 HTTP 终结点公开一个工作流服务。 若要运行此示例, 必须添加正确的 URL Acl (有关详细信息, 请参阅[配置 HTTP 和 HTTPS](https://go.microsoft.com/fwlink/?LinkId=70353) ), 方法是以管理员身份运行 Visual Studio, 或在提升的提示符下执行以下命令来添加相应的 acl。 确保替换了域和用户名。  
  
    ```  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2. 在添加 URL ACL 后，请使用下列步骤。  
  
    1. 生成解决方案。  
  
    2. 通过右键单击解决方案并选择 "**设置启动项目**" 来设置多个启动项目。  
  
    3. 将**服务**和**客户端**(按此顺序) 添加为多个启动项目。  
  
    4. 运行该应用程序。 客户端控制台显示运行两次的工作流，而服务窗口显示这些工作流的实例 ID。  
  
> [!IMPORTANT]
> 您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 如果此目录不存在, 请参阅[.NET Framework 4 的 Windows Communication Foundation (wcf) 和 Windows Workflow Foundation (WF) 示例](https://go.microsoft.com/fwlink/?LinkId=150780)以下载所有 Windows Communication Foundation (wcf) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]示例。 此示例位于以下目录：  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\Accessing Operation Context`
