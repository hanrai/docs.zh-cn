---
title: <workflowControlEndpoint>
ms.date: 03/30/2017
ms.assetid: 6c89e76c-643b-4b6a-9b25-628f753d7027
ms.openlocfilehash: 2c9774217b835acdb9ebf7374b964d838497fc9f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69915334"
---
# <a name="workflowcontrolendpoint"></a>\<workflowControlEndpoint>
此配置元素定义用于控制工作流实例的执行（创建、运行、挂起、终止等）的标准终结点。  
  
\<system.ServiceModel>  
\<standardEndpoints>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
    <workflowControlEndpoint>
      <standardEndpoint name="String" />
    </workflowControlEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|NAME|一个字符串，指定标准终结点的配置的名称。 此名称在服务终结点的 `endpointConfiguration` 特性中用于将标准终结点链接到其配置。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<standardEndpoints>](standardendpoints.md)|具有一个或多个固定属性（地址、绑定和协定）的预定义终结点的标准终结点集合。|  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>
