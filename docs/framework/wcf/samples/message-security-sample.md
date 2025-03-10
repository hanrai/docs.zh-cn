---
title: 消息安全示例
ms.date: 03/30/2017
ms.assetid: 82444166-6288-493a-85d4-85f43f134d19
ms.openlocfilehash: 1e57e82dc9394f34ab97da751a5d11c6099d353c
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044864"
---
# <a name="message-security-sample"></a>消息安全示例
此示例演示如何实现使用 `basicHttpBinding` 和消息安全性的应用程序。 此示例基于实现计算器服务的[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)。  
  
> [!NOTE]
> 本主题的最后介绍了此示例的设置过程和生成说明。  
  
 `basicHttpBinding` 的安全模式可以设置为下列值：`Message`、`Transport`、`TransportWithMessageCredential`、`TransportCredentialOnly` 和 `None`。 在下面的示例服务 App.config 文件中，终结点定义将指定 `basicHttpBinding` 并引用名为 `Binding1` 的绑定配置，如下面的示例配置中所示：  
  
```xml  
<system.serviceModel>  
  <services>  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
     <!-- This endpoint is exposed at the base address provided by -->  
     <!-- host: http://localhost:8000/ServiceModelSamples/service.-->  
     <endpoint address=""  
               binding="basicHttpBinding"  
               bindingConfiguration="Binding1"   
               contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </service>  
  </services>  
  ...  
</system.serviceModel>  
```  
  
 `mode`绑定配置将[ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md) `Message` 安全>`Certificate`的属性[设置\<](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-basichttpbinding.md)为, 并将消息的属性>设置为,如下所示`clientCredentialType`示例配置:  
  
```xml  
<bindings>  
  <basicHttpBinding>  
    <!--   
        This configuration defines the SecurityMode as Message and   
        the clientCredentialType as Certificate.  
        -->  
    <binding name="Binding1" >  
      <security mode = "Message">  
        <message clientCredentialType="Certificate"/>  
      </security>  
    </binding>  
  </basicHttpBinding>  
</bindings>  
```  
  
 服务用于向客户端验证自己身份的证书是在配置文件的 behaviors 节中 `serviceCredentials` 元素的下面设置的。 应用于证书（客户端使用该证书向服务验证自己的身份）的验证模式也是在 behaviors 节中 `clientCertificate` 元素的下面设置的。  
  
```xml  
<!--For debugging purposes, set the includeExceptionDetailInFaults attribute to true.-->  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
      <!--The serviceCredentials behavior allows one to define a -->  
      <!--service certificate. A service certificate is used by a -->  
      <!--client to authenticate the service and provide message -->  
      <!-- protection. This configuration references the "localhost"-->  
      <!--certificate installed during the setup instructions. -->  
      <serviceCredentials>  
        <serviceCertificate findValue="localhost"  
               storeLocation="LocalMachine"   
               storeName="My" x509FindType="FindBySubjectName" />  
        <clientCertificate>  
          <!-- Setting the certificateValidationMode to -->  
          <!-- PeerOrChainTrust means that if the certificate -->  
          <!--is in the user's Trusted People store, then it is -->  
          <!-- trusted without performing a validation of the -->  
          <!-- certificate's issuer chain. This setting is used -->  
          <!-- here for convenience so that the sample can be run -->  
          <!-- without having to have certificates issued by a -->  
          <!-- certification authority (CA). -->  
          <!-- This setting is less secure than the default, -->  
          <!-- ChainTrust. The security implications of this -->  
          <!-- setting should be carefully considered before using -->  
          <!-- PeerOrChainTrust in production code. -->  
          <authentication   
                       certificateValidationMode="PeerOrChainTrust" />  
        </clientCertificate>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 在客户端配置文件中指定同样的绑定和安全详细信息。  
  
 通过使用下面的代码，可以使调用方的标识显示在服务控制台窗口中：  

```csharp
Console.WriteLine("Called by {0}", ServiceSecurityContext.Current.PrimaryIdentity.Name);  
```

 运行示例时，操作请求和响应将显示在客户端控制台窗口中。 在客户端窗口中按 Enter 可以关闭客户端。  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-and-build-the-sample"></a>设置和生成示例  
  
1. 确保已对[Windows Communication Foundation 示例执行了一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要生成 C# 或 Visual Basic .NET 版本的解决方案，请按照 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
### <a name="to-run-the-sample-on-the-same-machine"></a>在同一计算机上运行示例  
  
1. 运行示例安装文件夹中的 Setup.bat。 这将安装运行示例所需的所有证书。  
  
    > [!NOTE]
    > Setup.bat 批处理文件设计为通过 Windows SDK 命令提示运行。 这要求 MSSDK 环境变量指向 SDK 的安装目录。 将在 Windows SDK 命令提示中自动设置此环境变量。  
  
2. 从 \service\bin 运行服务应用程序。  
  
3. 从 \client\bin 运行客户端应用程序。 客户端活动将显示在客户端控制台应用程序上。  
  
4. 如果客户端和服务无法进行通信, 请参阅[WCF 示例的故障排除提示](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
5. 在运行完该示例后运行 Cleanup.bat 移除证书。 其他安全示例使用相同的证书。  
  
### <a name="to-run-the-sample-across-machines"></a>跨计算机运行示例  
  
1. 在服务计算机上为服务二进制文件创建一个目录。  
  
2. 将服务程序文件复制到服务器上的服务目录中。 另外，将 Setup.bat、Cleanup.bat 和 ImportClientCert.bat 文件复制到服务器上。  
  
3. 在客户端计算机上为这些客户端二进制文件创建一个目录。  
  
4. 将客户端程序文件复制到客户端计算机上的客户端目录中。 另外，将 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 文件复制到客户端上。  
  
5. 在服务器上运行 `setup.bat service`。 使用`setup.bat`参数运行将使用计算机的完全限定的域名创建一个服务证书, 并将服务证书导出到名为 .cer 的文件中。 `service`  
  
6. 编辑`findValue` [serviceCertificate 以反映新的证书名称 (在 > 元素中的属性中), 该名称与计算机的完全限定域名相同。 \<](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 还要更改基址的值以指定一个完全限定的计算机名（而不是 localhost）。`.`  
  
7. 将服务目录中的 Service.cer 文件复制到客户端计算机上的客户端目录中。  
  
8. 在客户端上，运行 `setup.bat client`。 如果使用 `setup.bat` 自变量运行 `client`，则会创建一个名为 client.com 的客户端证书，并将此客户端证书导出到名为 Client.cer 的文件中。  
  
9. 在客户端计算机上的 Client.exe.config 文件中，更改终结点的地址值，使其与服务的新地址相匹配。 通过使用服务器的完全限定域名替换 localhost 来执行此操作。 另外, 将`findValue` [ \<defaultCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/defaultcertificate-element.md)的属性更改为新的服务证书名称, 该名称是服务器的完全限定域名。  
  
10. 将客户端目录中的 Client.cer 文件复制到服务器上的服务目录中。  
  
11. 在客户端上，运行 ImportServiceCert.bat。 这会将 Service.cer 文件中的服务证书导入 CurrentUser – TrustedPeople 存储区。  
  
12. 在服务器上，运行 ImportClientCert.bat，这会将 Client.cer 文件中的客户端证书导入 LocalMachine - TrustedPeople 存储区。  
  
13. 在服务计算机上，在命令提示符下运行 Service.exe。  
  
14. 在客户端计算机上，从命令提示符窗口中启动 Client.exe。  
  
    1. 如果客户端和服务无法进行通信, 请参阅[WCF 示例的故障排除提示](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-clean-up-after-the-sample"></a>运行示例后进行清理  
  
- 运行完示例后运行示例文件夹中的 Cleanup.bat。  
  
    > [!NOTE]
    > 此脚本不会在跨计算机运行此示例时移除客户端上的服务证书。 如果你已运行跨计算机使用证书的 Windows Communication Foundation (WCF) 示例, 请确保清除已安装在 CurrentUser-TrustedPeople 存储中的服务证书。 为此, 请使用以下命令:`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` 例如： `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`  
  
> [!IMPORTANT]
> 您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 如果此目录不存在, 请参阅[.NET Framework 4 的 Windows Communication Foundation (wcf) 和 Windows Workflow Foundation (WF) 示例](https://go.microsoft.com/fwlink/?LinkId=150780)以下载所有 Windows Communication Foundation (wcf) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]示例。 此示例位于以下目录：  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Basic\MessageSecurity`  
