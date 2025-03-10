---
title: <activityStateQuery>WCF 的
ms.date: 03/30/2017
ms.assetid: d6cdc04b-6f3a-4097-a623-ee4a1be3b5c4
ms.openlocfilehash: ce7505896b9c5bb605bb0f67d735cb324f4fd493
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69926899"
---
# <a name="activitystatequery-of-wcf"></a>\<WCF 的 activityStateQuery >

表示一个查询，该查询用于跟踪构成工作流实例的活动的生命周期更改。 例如, 你可能想要跟踪每次在工作流实例中完成 "发送电子邮件" 活动的时间。 跟踪参与者需要用此查询来订阅活动状态记录对象。 在 ActivityStates 中指定了要订阅的可用状态。  
  
有关跟踪配置文件查询的详细信息, 请参阅[跟踪配置文件](../../../windows-workflow-foundation/tracking-profiles.md)。

\<system.serviceModel> \<tracking>  
\<profiles> \<trackingProfile>  
\<工作流 >  
\<activityStateQueries>  
\<activityStateQuery>  
  
## <a name="syntax"></a>语法  
  
```xml  
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <activityStateQueries>
          <activityStateQuery activityName="String">
            <arguments>
              <argument name="String" />
            </arguments>
            <states>
              <state name="String" />
            </states>
            <variables>
              <variable name="String" />
            </variables>
          </activityStateQuery>
        </activityStateQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  

下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|activityName|一个字符串，指定要对其筛选 <xref:System.Activities.Tracking.ActivityStateRecord> 实例的活动的名称。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<参数 >](../windows-workflow-foundation/arguments.md)|与此活动查询关联的自变量的集合。|  
|[\<states>](../windows-workflow-foundation/states.md)|一个配置元素集合，这些元素包含应为其发出跟踪记录的已订阅活动的状态。|  
|[\<states>](../windows-workflow-foundation/states.md)|与此活动查询关联的变量的集合。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<faultPropagationQuery>](../windows-workflow-foundation/faultpropagationquery.md)|表示一个配置元素列表，这些元素用于跟踪父活动取消子活动的请求。 跟踪参与者需要用此查询来订阅取消请求记录对象。|  
  
## <a name="remarks"></a>备注

ActivityStateQuery 的一项独特功能是能够在跟踪工作流的执行时提取数据。 这在访问跟踪记录后续执行时可提供其他上下文。 您可以使用[ \<参数 >](../windows-workflow-foundation/arguments.md)、 [ \<状态 >](../windows-workflow-foundation/states.md)和[ \<状态 >](../windows-workflow-foundation/states.md)元素从工作流中的任何活动提取任何变量或参数。下面的示例演示在发出活动的`Closed`跟踪记录时提取变量和参数的活动状态查询。 变量和参数只能通过 ActivityStateRecord 提取, 因此使用[ \<activityStateQuery >](../windows-workflow-foundation/activitystatequery.md)在跟踪配置文件内进行订阅。  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">
  <states>
    <state name="Closed" />
  </states>
  <variables>
    <variable name="FromAddress" />
  </variables>
  <arguments>
    <argument name="Result" />
  </arguments>
</activityStateQuery>
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Activities.Tracking.Configuration.ActivityStateQueryElement>
- <xref:System.Activities.Tracking.ActivityStateQuery>
- [工作流跟踪](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [跟踪配置文件](../../../windows-workflow-foundation/tracking-profiles.md)
