---
title: <states>WCF,<workflowInstanceQuery>
ms.date: 03/30/2017
ms.assetid: d17f7525-8035-4e9e-85a0-4cddae59f85d
ms.openlocfilehash: ef4ce4b6fa6e60ead10b196b10a7c1489e15ac25
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69938981"
---
# <a name="states-of-wcf-workflowinstancequery"></a>\<WCF、 \<workflowInstanceQuery > 的状态 >

表示创建跟踪记录时已跟踪工作流实例中已订阅状态的集合。  
  
有关跟踪配置文件查询的详细信息, 请参阅[跟踪配置文件](../../../windows-workflow-foundation/tracking-profiles.md)  
  
\<system.serviceModel> \<tracking>  
\<配置文件 >  
\<trackingProfile>  
\<工作流 >  
\<workflowInstanceQueries>  
\<workflowInstanceQuery>  
\<状态 >  
  
## <a name="syntax"></a>语法  
  
```xml  
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <workflowInstanceQueries>
          <workflowInstanceQuery>
            <states>
              <state name="Name" />
            </states>
          </workflowInstanceQuery>
        </workflowInstanceQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>
```  
  
## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  

无。  
  
### <a name="child-elements"></a>子元素
  
|元素|描述|  
|-------------|-----------------|  
|[\<states>](state-of-wcf-workflowinstancequery.md)|创建跟踪记录时已跟踪工作流实例中的一个已订阅状态。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<workflowInstanceQuery>](../windows-workflow-foundation/workflowinstancequery.md)|一个查询，该查询跟踪工作流实例生命周期的更改，例如已开始或已完成的事件。|  
  
## <a name="remarks"></a>备注

返回的记录由此集合中的状态进行筛选。  
  
下表中列出了可能的状态值。  
  
|状态|描述|  
|-----------|-----------------|  
|Aborted|工作流实例已中止。|  
|已完成|工作流实例已完成。|  
|Deleted|工作流实例已删除。|  
|Idle|工作流实例处于空闲状态。|  
|Persisted|工作流实例已保留。|  
|Resumed|工作流实例已恢复。|  
|已开始|工作流实例已启动。|  
|UnhandledException|工作流实例遇到了未经处理的异常。|  
|已卸载|工作流实例已卸载。|  
|Canceled|工作流实例已取消。|  
|挂起的|工作流实例处于挂起状态。|  
|Terminated|工作流实例已终止。|  
|Unsuspended|工作流实例已取消挂起。|  
  
## <a name="example"></a>示例

下面的配置使用此查询订阅 `Started` 实例状态的工作流实例级跟踪记录。  
  
```xml  
<workflowInstanceQueries>
  <workflowInstanceQuery>
    <states>
      <state name="Started" />
    </states>
  </workflowInstanceQuery>
</workflowInstanceQueries>
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Activities.Tracking.Configuration.WorkflowInstanceQueryElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Activities.Tracking.Configuration.StateElementCollection?displayProperty=nameWithType>
- <xref:System.Activities.Tracking.WorkflowInstanceQuery?displayProperty=nameWithType>
- [工作流跟踪](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [跟踪配置文件](../../../windows-workflow-foundation/tracking-profiles.md)
