---
title: 如何：将服务名字对象用于 WSDL 协定
ms.date: 03/30/2017
ms.assetid: a88d9650-bb50-4f48-8c85-12f5ce98a83a
ms.openlocfilehash: 80b0d034b92123862d0500106f81d4a566cac467
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968783"
---
# <a name="how-to-use-a-service-moniker-with-wsdl-contracts"></a>如何：将服务名字对象用于 WSDL 协定
在某些情况下，您可能希望具有完全自包含的 COM 互操作客户端。 您要调用的服务可能不会公开 MEX 终结点，而 WCF 客户端 DLL 可能不会为 COM 互操作注册。 在这些情况下，您可以创建用于描述该服务的 WSDL 文件，并将该文件传递到 WCF 服务标记中。 本主题描述如何使用 WCF WSDL 标记调用 WCF 入门示例。  
  
### <a name="using-the-wsdl-service-moniker"></a>使用 WSDL 服务标记  
  
1. 打开并生成 GettingStarted 示例解决方案。  
  
2. 打开 Internet Explorer 并浏览到`http://localhost/ServiceModelSamples/Service.svc` , 确保该服务正在运行。  
  
3. 在 Service.cs 文件中，将下面的属性添加到 CalculatorService 类中：  
  
     [!code-csharp[S_WSDL_Client#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wsdl_client/cs/service.cs#0)]  
  
4. 将绑定命名空间添加到服务 App.config 中：  

5. 为要读取的应用程序创建 WSDL 文件。 由于命名空间是在步骤3和步骤4中添加的, 因此可以使用 IE 通过浏览到来`http://localhost/ServiceModelSamples/Service.svc?wsdl`查询服务的整个 WSDL 说明。 然后，将文件从 Internet Explorer 另存为 serviceWSDL.xml。 如果未在步骤 3 和 4 中指定命名空间，则从查询上述 URL 返回的 WSDL 文档将不是完整的 WSDL。 返回的 WSDL 文档将包括导入其他 WSDL 文档的多条导入语句。 您必须完成每条导入语句并生成完整的 WSDL 文档，从而将从服务返回的 WSDL 与导入的 WSDL 合并在一起。  
  
6. 打开 Visual Basic 6.0 并创建一个新的 Standard .exe 文件。 在窗体中添加一个按钮并双击该按钮，以将以下代码添加到 Click 处理程序中：  
  
    ```  
    ' Open the WSDL contract file and read it all into the wsdlContract string.  
    Const ForReading = 1  
    Set objFSO = CreateObject("Scripting.FileSystemObject")  
    Set objFile = objFSO.OpenTextFile("c:\serviceWsdl.xml", ForReading)  
    wsdlContract = objFile.ReadAll  
    objFile.Close  
  
    ' Create a string for the service moniker including the content of the WSDL contract file.  
    wsdlMonikerString = "service4:address='http://localhost/ServiceModelSamples/service.svc'"  
    wsdlMonikerString = wsdlMonikerString + ", wsdl='" & wsdlContract & "'"  
    wsdlMonikerString = wsdlMonikerString + ", binding=WSHttpBinding_ICalculator, bindingNamespace='http://Microsoft.ServiceModel.Samples'"  
    wsdlMonikerString = wsdlMonikerString + ", contract=ICalculator, contractNamespace='http://Microsoft.ServiceModel.Samples'"  
  
    ' Create the service moniker object.  
    Set wsdlServiceMoniker = GetObject(wsdlMonikerString)  
  
    ' Call the service operations using the moniker object.  
    MsgBox "WSDL service moniker: 145 - 76.54 = " & wsdlServiceMoniker.Subtract(145, 76.54)  
    ```  
  
    > [!NOTE]
    > 如果标记的格式不正确，或者服务不可用，则对 `GetObject` 的调用将返回一个错误，指示“无效的语法”。  如果您收到此错误，请确保所使用的标记正确无误且服务可用。  
  
7. 运行 Visual Basic 应用程序。 将显示一个消息框，其中列出调用 Subtract(145, 76.54) 的结果。  
  
## <a name="see-also"></a>请参阅

- [入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)
- [与 COM 应用程序集成的概述](../../../../docs/framework/wcf/feature-details/integrating-with-com-applications-overview.md)
