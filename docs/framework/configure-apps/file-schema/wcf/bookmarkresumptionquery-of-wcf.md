---
title: <bookmarkResumptionQuery>WCF 的
ms.date: 03/30/2017
ms.assetid: 755a34f0-87c9-4a1e-ae4d-0fb8a6fbdc0e
ms.openlocfilehash: ee8457645a0b54e21ef27c2891ebea97d6cc547b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69926354"
---
# <a name="bookmarkresumptionquery-of-wcf"></a>\<WCF 的 y >

表示一个查询，该查询用于跟踪工作流实例中的书签恢复。 跟踪参与者需要用此查询来订阅书签恢复记录。  
  
有关跟踪配置文件查询的详细信息, 请参阅[跟踪配置文件](../../../windows-workflow-foundation/tracking-profiles.md)
  
\<system.serviceModel>  
\<跟踪 >  
\<配置文件 >  
\<trackingProfile>  
\<工作流 >  
\<bookmarkResumptionQueries>  
\<bookmarkResumptionQuery>  
  
## <a name="syntax"></a>语法  
  
```xml  
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <bookmarkResumptionQueries>
          <bookmarkResumptionQuery name="String" />
        </bookmarkResumptionQueries>
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
|`name`|一个字符串，指定要订阅的书签记录的名称。|  
  
### <a name="child-elements"></a>子元素

无。
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<bookmarkResumptionQueries>](bookmarkresumptionqueries-of-wcf.md)|表示一个查询集合，这些查询用于跟踪工作流实例中的书签恢复。|  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Activities.Tracking.Configuration.BookmarkResumptionQueryElementCollection?displayProperty=nameWithType>
- <xref:System.Activities.Tracking.BookmarkResumptionQuery?displayProperty=nameWithType>
- [工作流跟踪](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [跟踪配置文件](../../../windows-workflow-foundation/tracking-profiles.md)
