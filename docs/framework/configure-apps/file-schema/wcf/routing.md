---
title: <routing>
ms.date: 03/30/2017
ms.assetid: a210c209-3940-4288-9a8e-39b1e62606bc
ms.openlocfilehash: 3c7e9cb1284ab55c8dd199d9fb47a223698814f0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69934130"
---
# <a name="routing"></a>\<路由 >

表示用于定义一组路由筛选器的配置节, 这些筛选器确定计算传入消息时要<xref:System.ServiceModel.Dispatcher.MessageFilter>使用的 Windows Communication Foundation (WCF) 的类型, 以及用于定义目标终结点的路由表。当筛选器匹配时向发送消息。

[ **\<system.serviceModel>** ](system-servicemodel.md)   
&nbsp;&nbsp; **\<routing>**
  
## <a name="syntax"></a>语法  
  
```xml  
<system.serviceModel>
  <routing>
    <filters>
      <filter customType="String"
              filterData="String"
              filterType="Action/Address/AddressPrefix/And/Custom/Endpoint/MatchAll/XPath"
              name="String" />
    </filters>
    <routingTables>
      <table name="String">
        <entries>
          <add endpoint="String"
               filterName="String"
               priority="Integer" />
        </entries>
      </table>
    </routingTables>
  </routing>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

无

### <a name="child-elements"></a>子元素

|     | 描述 |
| --- | ----------- |
| [ **\<filters>** ](filters-of-routing.md) | 包含一组路由筛选器, 用于确定在计算传入消息时将使用的 Windows Communication Foundation (WCF) MessageFilter 的类型。 |
| [ **\<filterTables>** ](filtertables.md) | 包含路由筛选器和目标终结点之间的映射，以便指定在筛选器匹配时使用的终结点。 |

### <a name="parent-elements"></a>父元素

|     | 描述 |
| --- | ----------- |
| **\<system.ServiceModel>** | 所有 WCF 配置元素的根元素。 |

## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Routing.Configuration.RoutingSection?displayProperty=nameWithType>
