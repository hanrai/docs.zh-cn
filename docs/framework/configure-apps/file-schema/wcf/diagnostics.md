---
title: <diagnostics>
ms.date: 03/30/2017
ms.assetid: 0c2f95c4-cc12-4fb5-a70c-7fc6fa95db58
ms.openlocfilehash: 170cae5b328c86073c1d8e7710bb19e98ab5688c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925877"
---
# <a name="diagnostics"></a>\<diagnostics>
`diagnostics` 元素定义管理员可以用来进行运行时检查和控制的设置。  
  
 \<system.ServiceModel>  
\<diagnostics>  
  
## <a name="syntax"></a>语法  
  
```xml  
<system.serviceModel>
  <diagnostics etwProviderId="String"
               performanceCounters="Off/ServiceOnly/All/Default"
               wmiProviderEnabled="Boolean">
    <endToEndTracing activityTracing="Boolean"
                     messageFlowTracing="Boolean"
                     propagateActivity="Boolean" />
    <messageLogging logEntireMessage="Boolean"
                    logMalformedMessages="Boolean"
                    logMessagesAtServiceLevel="Boolean"
                    logMessagesAtTransportLevel="Boolean"
                    maxMessagesToLog="Integer"
                    maxSizeOfMessageToLog="Integer">
      <filters>
        <clear />
      </filters>
    </messageLogging>
  </diagnostics>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|etwProviderId|一个字符串，指定将事件写入到 ETW 会话的事件跟踪提供程序的标识符。|  
|performanceCounters|指定是否启用程序集的性能计数器。 有效值为<br /><br /> 非性能计数器被禁用。<br />ServiceOnly只启用与此服务相关的性能计数器。<br />一切可以在运行时查看性能计数器。<br />缺省值创建单个性能计数器实例 _WCF_Admin。 此实例用于启用基础结构所使用的 SQM 数据的集合。 此实例的计数器值均未进行更新，因此将保持为零。 这是在 WCF 没有配置的情况下的默认值。|  
|wmiProviderEnabled|一个布尔值，指定是否启用程序集的 WMI 提供程序。 用户要获得在运行时访问 Windows Communication Foundation (WCF) 的检查和控制功能的权限，需要使用 WMI 提供程序。 默认值为 `false`。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<endToEndTracing>](endtoendtracing.md)|一个配置元素，用于启用和禁用服务应用程序运行过程中端对端跟踪的不同方面。|  
|[\<messageLogging>](messagelogging.md)|描述 WCF 消息日志记录的设置。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|serviceModel|所有 WCF 配置元素的根元素。|  
  
## <a name="remarks"></a>备注  
 `diagnostics` 节定义了位于程序集中的所有服务的诊断设置。 无法在服务级别定义单独的诊断设置，除非程序集中只有一个服务。 将根据本节的需求来设置属性。  
  
## <a name="example"></a>示例  
  
```xml  
<diagnostics wmiProviderEnabled="false"
             performanceCounters="all">
  <messageLogging logEntireMessage="true"
                  logMalformedMessages="true"
                  logMessagesAtServiceLevel="true"
                  logMessagesAtTransportLevel="true"
                  maxMessagesToLog="42"
                  maxSizeOfMessageToLog="42">
    <filters>
      <clear />
    </filters>
  </messageLogging>
</diagnostics>
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Configuration.DiagnosticSection>
- <xref:System.ServiceModel.Diagnostics>
