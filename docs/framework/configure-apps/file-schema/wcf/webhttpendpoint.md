---
title: <webHttpEndpoint>
ms.date: 03/30/2017
ms.assetid: ecaaeb6f-ebd0-411d-8b53-92477cd45347
ms.openlocfilehash: 866be522cb1c64142227a8d6a1a8f88551ca9105
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940473"
---
# <a name="webhttpendpoint"></a>\<webHttpEndpoint>
此配置元素定义一个标准终结点, 该终结点具有固定[ \<的 webHttpBinding >](webhttpbinding.md)绑定[ \<](webhttp.md) , 可自动添加 wcf-webhttp > 行为。 在编写 REST 服务时，请使用此终结点。  
  
\<system.ServiceModel>  
\<standardEndpoints>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
    <webHttpEndpoint>
      <standardEndpoint automaticFormatSelectionEnabled="String"
                        defaultOutgoingResponseFormat="Xml/Json"
                        helpEnabled="Boolean"
                        webEndpointType="String" />
    </webHttpEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|automaticFormatSelectionEnabled|一个布尔值，指示是否启用自动格式选择。<br /><br /> 如果启用了自动格式选择，基础结构将分析请求消息的 `Accept` 标头，并确定最适合的响应格式。 如果 `Accept` 标头未指定适合的响应格式，则基础结构将使用请求消息的 `Content-Type`，或使用操作的默认响应格式。|  
|defaultOutgoingResponseFormat|一个指定默认传出响应格式的特性。 此特性的类型为 <xref:System.ServiceModel.Web.WebMessageFormat>|  
|helpEnabled|一个布尔值，指示是否为终结点启用了 HTTP 帮助页。|  
|webEndpointType|一个字符串，指定终结点的类型。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<standardEndpoints>](standardendpoints.md)|具有一个或多个固定属性（地址、绑定和协定）的预定义终结点的标准终结点集合。|  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Description.WebHttpEndpoint>
- <xref:System.ServiceModel.Configuration.WebHttpEndpointElement>
