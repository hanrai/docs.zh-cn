---
title: <faultPropagationQuery>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 4fb5c2b1-3dad-4eca-9c7f-3efb51899813
ms.openlocfilehash: f77a613f4eb0456a0085096aa478d37c78122217
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69946304"
---
# <a name="faultpropagationquery"></a>\<faultPropagationQuery>

表示一个用于跟踪在活动中发生的错误的处理的查询。  每次 FaultHandler 处理错误时，都会发生此事件。 应使用此类查询来跟踪对在活动中出现的错误进行的处理。 跟踪参与者需要用此查询来订阅错误传播记录。

 有关跟踪配置文件查询的详细信息, 请参阅[跟踪配置文件](../../../windows-workflow-foundation/tracking-profiles.md)。

\<system.serviceModel>\
\<跟踪 > \
\<trackingProfile>\
\<工作流 > \
\<faultPropagationQueries>\
\<faultPropagationQuery>

## <a name="syntax"></a>语法

```xml
<tracking>
  <trackingProfile name="Name">
    <workflow>
      <faultPropagationQueries>
        <faultPropagationQuery activityName="String"
                               faultHandlerActivityName="String" />
      </faultPropagationQueries>
    </workflow>
  </trackingProfile>
</tracking>
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|activityName|一个字符串, 指定传播错误的错误处理程序活动的名称。 默认值为 *，指示为所有活动返回错误传播记录。|
|faultHandlerActivityName|一个字符串，指定导致错误的活动的名称。|

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[\<faultPropagationQueries>](faultpropagationqueries.md)|表示一个配置元素列表，这些元素用于跟踪某个活动中发生的错误的处理。  每次 FaultHandler 处理错误时，都会发生此事件。|

## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Activities.Tracking.Configuration.FaultPropagationQueryElement?displayProperty=nameWithType>
- <xref:System.Activities.Tracking.FaultPropagationQuery?displayProperty=nameWithType>
- [工作流跟踪](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [跟踪配置文件](../../../windows-workflow-foundation/tracking-profiles.md)
