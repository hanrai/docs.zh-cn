---
title: 自定义服务主机
ms.date: 03/30/2017
ms.assetid: fe16ff50-7156-4499-9c32-13d8a79dc100
ms.openlocfilehash: 5da6497eadc6f02210c7f9d35d2889c98dc34ce4
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70039961"
---
# <a name="custom-service-host"></a>自定义服务主机
本示例演示如何使用 <xref:System.ServiceModel.ServiceHost> 类的自定义派生来改变服务的运行时行为。 此方法为通过通用方式配置大量服务提供了一个可重用的替代方法。 此示例还演示如何使用 <xref:System.ServiceModel.Activation.ServiceHostFactory> 类在 Internet 信息服务 (IIS) 或 Windows 进程激活服务 (WAS) 承载环境中使用自定义 ServiceHost。  
  
> [!IMPORTANT]
> 您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 如果此目录不存在, 请参阅[.NET Framework 4 的 Windows Communication Foundation (wcf) 和 Windows Workflow Foundation (WF) 示例](https://go.microsoft.com/fwlink/?LinkId=150780)以下载所有 Windows Communication Foundation (wcf) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]示例。 此示例位于以下目录：  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Hosting\CustomServiceHost`  
  
## <a name="about-the-scenario"></a>关于方案  
 为了避免无意中泄漏可能敏感的服务元数据, Windows Communication Foundation (WCF) 服务的默认配置将禁用元数据发布。 默认情况下此行为是安全的，但也意味着你无法使用元数据导入工具（例如 Svcutil.exe）生成调用服务所需的客户端代码，除非在配置中显式启用服务的元数据发布行为。  
  
 对大量服务启用元数据发布需要向每个单独的服务添加相同的配置元素，这会生成实质上相同的大量配置信息。 作为分别配置每个服务的一种替代方法，可以编写命令性代码来启用一次元数据发布，然后在多个不同的服务中重复使用该代码。 这是通过创建一个从 <xref:System.ServiceModel.ServiceHost> 派生的新类并重写 `ApplyConfiguration`() 方法以便强制添加元数据发布行为来实现的。  
  
> [!IMPORTANT]
> 为清楚起见，本示例演示如何创建不安全的元数据发布终结点。 此类终结点或许可以供未通过身份验证的匿名使用者使用，因此在部署此类终结点之前，必须谨慎以确保适合公开透露服务元数据。  
  
## <a name="implementing-a-custom-servicehost"></a>实现自定义 ServiceHost  
 <xref:System.ServiceModel.ServiceHost> 类公开多个有用的虚拟方法，继承者可以重写这些方法以改变服务的运行时行为。 例如，`ApplyConfiguration`() 方法可从配置存储中读取服务配置信息并相应地改变主机的 <xref:System.ServiceModel.Description.ServiceDescription>。 默认实现可从应用程序的配置文件中读取配置。 自定义实现可以重写 `ApplyConfiguration`() 以便使用命令性代码进一步改变 <xref:System.ServiceModel.Description.ServiceDescription>，甚至完全替换默认配置存储。 例如，从数据库而不是应用程序的配置文件中读取服务的终结点配置。  
  
 在本示例中，我们要生成一个用于添加 ServiceMetadataBehavior（可启用元数据发布）的自定义 ServiceHost，即使服务的配置文件中未显式添加此行为。 为了实现此目的，我们要创建一个从 <xref:System.ServiceModel.ServiceHost> 继承的新类并重写 `ApplyConfiguration`()。  
  
```  
class SelfDescribingServiceHost : ServiceHost  
{  
    public SelfDescribingServiceHost(Type serviceType, params Uri[] baseAddresses)  
        : base(serviceType, baseAddresses) { }  
  
    //Overriding ApplyConfiguration() allows us to   
    //alter the ServiceDescription prior to opening  
    //the service host.   
    protected override void ApplyConfiguration()  
    {  
        //First, we call base.ApplyConfiguration()  
        //to read any configuration that was provided for  
        //the service we're hosting. After this call,  
        //this.Description describes the service  
        //as it was configured.  
        base.ApplyConfiguration();       
  
        //(rest of implementation elided for clarity)  
    }  
}  
```  
  
 由于我们不想忽略在应用程序的配置文件中已提供的任何配置，因此，重写 `ApplyConfiguration`() 的第一步是调用基实现。 完成此方法后，我们可以使用下面的命令性代码向说明中强制添加 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>。  
  
```  
ServiceMetadataBehavior mexBehavior = this.Description.Behaviors.Find<ServiceMetadataBehavior>();  
if (mexBehavior == null)  
{  
    mexBehavior = new ServiceMetadataBehavior();  
    this.Description.Behaviors.Add(mexBehavior);  
}  
else  
{  
    //Metadata behavior has already been configured,   
    //so we do not have any work to do.  
    return;  
}  
```  
  
 重写 `ApplyConfiguration`() 必须执行的最后一步是添加默认元数据终结点。 按照约定，为服务主机的 BaseAddresses 集合中的每个 URI 创建了一个元数据终结点。  
  
```  
//Add a metadata endpoint at each base address  
//using the "/mex" addressing convention  
foreach (Uri baseAddress in this.BaseAddresses)  
{  
    if (baseAddress.Scheme == Uri.UriSchemeHttp)  
    {  
        mexBehavior.HttpGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeHttps)  
    {  
        mexBehavior.HttpsGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpsBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetPipe)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexNamedPipeBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetTcp)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexTcpBinding(),  
                                "mex");  
    }  
}  
```  
  
## <a name="using-a-custom-servicehost-in-self-host"></a>在自承载方案中使用自定义 ServiceHost  
 由于已完成了自定义 ServiceHost 实现，因此可以使用它通过在 `SelfDescribingServiceHost` 的实例内承载任何服务向该服务添加元数据发布行为。 下面的代码演示如何在自承载方案中使用自定义 ServiceHost。  
  
```  
SelfDescribingServiceHost host =   
         new SelfDescribingServiceHost( typeof( Calculator ) );  
host.Open();  
```  
  
 自定义主机仍然从应用程序的配置文件中读取服务的终结点配置，就好象使用默认 <xref:System.ServiceModel.ServiceHost> 类承载服务一样。 但由于我们添加了在自定义主机内启用元数据发布的逻辑，因此不再需要在配置中显式启用元数据发布行为。 如果要生成的应用程序包含多个服务并需要在每个服务上启用元数据发布，而不想反复编写同样的配置元素，则使用此方法具有明显的优势。  
  
## <a name="using-a-custom-servicehost-in-iis-or-was"></a>在 IIS 或 WAS 中使用自定义 ServiceHost  
 在自承载方案中使用自定义服务主机非常简单，因为最终负责创建和打开服务主机实例的是应用程序代码。 但在 IIS 或 WAS 宿主环境中, WCF 基础结构会动态地实例化服务的主机, 以响应传入消息。 自定义服务主机也可用于此承载环境，但它们需要一些 ServiceHostFactory 形式的附加代码。 下面的代码演示可返回自定义 <xref:System.ServiceModel.Activation.ServiceHostFactory> 的实例的 `SelfDescribingServiceHost` 的派生。  
  
```  
public class SelfDescribingServiceHostFactory : ServiceHostFactory  
{  
    protected override ServiceHost CreateServiceHost(Type serviceType,   
     Uri[] baseAddresses)  
    {  
        //All the custom factory does is return a new instance  
        //of our custom host class. The bulk of the custom logic should  
        //live in the custom host (as opposed to the factory)   
        //for maximum  
        //reuse value outside of the IIS/WAS hosting environment.  
        return new SelfDescribingServiceHost(serviceType,     
                                             baseAddresses);  
    }  
}  
```  
  
 您可以看到，实现自定义 ServiceHostFactory 非常简单。 所有自定义逻辑都位于 ServiceHost 实现的内部；工厂返回派生类的实例。  
  
 若要对服务实现使用自定义工厂，必须向服务的 .svc 文件添加一些附加元数据。  
  
```  
<%@ServiceHost Service="Microsoft.ServiceModel.Samples.CalculatorService"  
               Factory="Microsoft.ServiceModel.Samples.SelfDescribingServiceHostFactory"  
               language=c# Debug="true" %>  
```  
  
 在此我们向 `Factory` 指令添加了一个附加 `@ServiceHost` 属性，并作为该属性的值传递自定义工厂的 CLR 类型名称。 当 IIS 或 WAS 接收到此服务的消息时, WCF 托管基础结构首先会创建 ServiceHostFactory 的实例, 然后通过调用`ServiceHostFactory.CreateServiceHost()`实例化服务主机本身。  
  
## <a name="running-the-sample"></a>运行示例  
 虽然本示例提供功能完整的客户端和服务实现，但本示例的目的主要是演示如何通过自定义主机改变服务的运行时行为。请执行下面的步骤：  
  
#### <a name="to-observe-the-effect-of-the-custom-host"></a>观察自定义主机的效果  
  
1. 打开服务的 Web.config 文件并观察其中的配置是否未显式启用服务的元数据。  
  
2. 打开服务的 .svc 文件, 并观察它@ServiceHost的指令是否包含一个工厂属性, 该属性指定自定义 ServiceHostFactory 的名称。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>设置、生成和运行示例  
  
1. 确保已对[Windows Communication Foundation 示例执行了一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要生成解决方案, 请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3. 构建解决方案后, 请运行 ServiceModelSamples 以在 IIS 7.0 中设置该应用程序。 现在, ServiceModelSamples 目录应显示为 IIS 7.0 应用程序。  
  
4. 若要以单机配置或跨计算机配置来运行示例, 请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
5. 若要删除 IIS 7.0 应用程序, 请运行 "清理"。  
  
## <a name="see-also"></a>请参阅

- [如何：在 IIS 中承载 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)
