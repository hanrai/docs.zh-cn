---
title: <dataContractSerializer>
ms.date: 03/30/2017
helpviewer_keywords:
- dataContractSerializer element
- <dataContractSerializer> element
- DataContractSerializer
- KnownTypes
ms.assetid: f41fb4d5-24e7-4059-8010-286a30bfea93
ms.openlocfilehash: 7e440810fee1dddb7025d1385b1edb4838d98a39
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925914"
---
# <a name="datacontractserializer"></a>\<dataContractSerializer>
包含 <xref:System.Runtime.Serialization.DataContractSerializer> 的配置数据。 此元素出现在两个不同的层次结构中。 这两个层次结构分别在下面的“架构层次结构”一节和“备注”一节中列出。  
  
 \<system.ServiceModel>  
\<行为 >  
\<serviceBehaviors>  
\<行为 >  
\<dataContractSerializer>  
  
## <a name="syntax"></a>语法  
  
```xml  
<dataContractSerializer ignoreExtensionDataObject="Boolean"
                        maxItemsInObjectGraph="Integer" />
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|元素|描述|  
|-------------|-----------------|  
|ignoreExtensionDataObject|一个布尔值，指定在对终结点进行序列化或反序列化时，是否要忽略由该终结点提供的数据。 只可对 `<dataContractSerializer>` 元素下的 `<behavior>` 设置此属性。|  
|maxItemsInObjectGraph|一个整数，指定要序列化或反序列化的最大项数。 此属性为 65536。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-servicebehaviors.md)|服务行为的设置集合。|  
|[\<system.runtime.serialization>](system-runtime-serialization.md)|表示 <xref:System.Runtime.Serialization> 命名空间节的根元素，并包含 <xref:System.Runtime.Serialization.DataContractSerializer> 的设置选项的元素。|  
  
## <a name="remarks"></a>备注  
 如本主题中所述, 这是\<X509Extension > 元素的第二个层次结构。  
  
 [\<system.runtime.serialization>](system-runtime-serialization.md)  
  
 [\<dataContractSerializer>](datacontractserializer-element.md)  
  
 有关已知类型的更多信息，请参见 <xref:System.Runtime.Serialization.DataContractSerializer>。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>
- <xref:System.ServiceModel.Configuration.DataContractSerializerElement>
- [数据协定已知类型](../../../wcf/feature-details/data-contract-known-types.md)
- [数据传输和序列化](../../../wcf/feature-details/data-transfer-and-serialization.md)
