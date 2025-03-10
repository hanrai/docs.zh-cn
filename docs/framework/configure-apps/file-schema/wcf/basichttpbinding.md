---
title: <basicHttpBinding>
ms.date: 03/30/2017
helpviewer_keywords:
- basicHttpBinding Element
ms.assetid: 85cf1a4f-26c2-48c7-bda6-6c960d5d3fb3
ms.openlocfilehash: 2ae8a9d2ad7bf3607394e65570b8961fd2d58606
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69919887"
---
# <a name="basichttpbinding"></a>\<basicHttpBinding>
表示 Windows Communication Foundation (WCF)服务可用来配置和公开终结点的绑定，这些终结点将能够与基于 ASMX 的 Web 服务和客户端以及其他符合 WS-I Basic Profile 1.1 的服务进行通信。  
  
 \<system.ServiceModel>  
\<bindings>  
\<basicHttpBinding>  
  
## <a name="syntax"></a>语法  
  
```xml  
<basicHttpBinding>
  <binding allowCookies="Boolean"
           bypassProxyOnLocal="Boolean"
           closeTimeout="TimeSpan"
           envelopeVersion="None/Soap11/Soap12"
           hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"
           maxBufferPoolSize="Integer"
           maxBufferSize="Integer"
           maxReceivedMessageSize="Integer"
           messageEncoding="Text/Mtom"
           name="String"
           openTimeout="TimeSpan"
           proxyAddress="URI"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding"
           transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
           useDefaultWebProxy="Boolean">
    <security mode="None/Transport/Message/TransportWithMessageCredential/TransportCredentialOnly">
      <transport clientCredentialType="None/Basic/Digest/Ntlm/Windows/Certificate"
                 proxyCredentialType="None/Basic/Digest/Ntlm/Windows"
                 realm="String" />
      <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
               clientCredentialType="UserName/Certificate" />
    </security>
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</basicHttpBinding>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`allowCookies`|一个布尔值，指示客户端是否接受 Cookie 并在今后的请求中传播这些 Cookie。 默认值为 `false`。<br /><br /> 在与使用 Cookie 的 ASMX Web 服务进行交互时，可以使用此属性。 通过这种方式，可以确保从服务器返回的 Cookie 自动复制到客户端今后对该服务的所有请求。|  
|`bypassProxyOnLocal`|一个布尔值，指示是否对本地地址不使用代理服务器。 默认值为 `false`。<br /><br /> 如果 Internet 资源具有本地地址，则该资源是本地资源。 本地地址是指位于同一台计算机、 本地 LAN 或 intranet 上和标识，语法上通过省略句点 （.） 如 Uri " http://webserver/ " 和 " http://localhost/ "。<br /><br /> 通过设置此属性，可以确定在访问本地资源时，采用 BasicHttpBinding 配置的终结点是否使用代理服务器。 如果此属性为 `true`，则对本地 Internet 资源的请求不使用代理服务器。 当此属性设置为 `true` 时，如果希望客户端在与同一台计算机上的服务通话时使用代理，请使用主机名称（而非 localhost）。<br /><br /> 当此属性为 `false` 时，所有 Internet 请求都通过代理服务器发出。|  
|`closeTimeout`|一个 <xref:System.TimeSpan> 值，指定为完成关闭操作提供的时间间隔。 此值应大于或等于 <xref:System.TimeSpan.Zero>。 默认值为 00:01:00。|  
|`envelopeVersion`|指定用于通过此绑定处理的消息的 SOAP 版本。 只有 Soap11 是有效值。|  
|`hostNameComparisonMode`|指定用于分析 URI 的 HTTP 主机名比较模式。 此属性的类型为 <xref:System.ServiceModel.HostNameComparisonMode>，指示在对 URI 进行匹配时，是否使用主机名来访问服务。 默认值为 <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>，表示忽略匹配项中的主机名。|  
|`maxBufferPoolSize`|一个整数值，指定为从通道接收消息的消息缓冲区管理器分配并供其使用的最大内存量。 默认值为 524288 (0x80000) 字节。<br /><br /> 通过使用缓冲池，缓冲区管理器可将使用缓冲区的开销降到最低。 当消息离开通道时，服务需要使用缓冲区来处理这些消息。 如果缓冲池中的内存不够用来处理消息负载，则缓冲区管理器必须从 CLR 堆分配更多内存，而这会增加垃圾回收的系统开销。 从 CLR 垃圾堆进行大量分配表明缓冲池太小，可以通过提高此属性指定的限制来实现更大的内存分配，从而提高性能。|  
|`maxBufferSize`|一个整数值，指定为采用此绑定配置的终结点处理消息时存储消息的缓冲区的最大大小（字节）。 默认值为 65,536 字节。|  
|`maxReceivedMessageSize`|一个正整数，定义在采用此绑定配置的通道上可以接收的消息的最大消息大小（字节），包括消息头。 如果消息对于接收方而言太大，则发送方将收到 SOAP 错误。 接收方将删除该消息，并在跟踪日志中创建事件项。 默认值为 65,536 字节。|  
|`messageEncoding`|定义用于对 SOAP 消息进行编码的编码器。 包括以下有效值：<br /><br /> 全文使用文本消息编码器。<br />Mtom使用消息传输组织机制 1.0 (MTOM) 编码器。<br /><br /> 默认值为 Text。 此属性的类型为 <xref:System.ServiceModel.WSMessageEncoding>。|  
|`name`|一个包含绑定的配置名称的字符串。 因为此值用作绑定的标识，所以它应该是唯一的。 每个绑定都具有 `name` 和 `namespace` 属性，它们共同在服务的元数据中唯一标识每个绑定。 此外，在同一类型的绑定中，此名称是唯一的。 从 [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)] 开始，不要求绑定和行为具有名称。 有关默认配置和无值绑定和行为的详细信息, 请参阅[WCF 服务的](../../../wcf/samples/simplified-configuration-for-wcf-services.md)[简化配置](../../../wcf/simplified-configuration.md)和简化配置。|  
|`namespace`|指定绑定的 XML 命名空间。 默认值为 “http://tempuri.org/Bindings” 。 每个绑定都具有 `name` 和 `namespace` 属性，它们共同在服务的元数据中唯一标识每个绑定。|  
|`openTimeout`|一个 <xref:System.TimeSpan> 值，指定为完成打开操作提供的时间间隔。 此值应大于或等于 <xref:System.TimeSpan.Zero>。 默认值为 00:01:00。|  
|`proxyAddress`|一个包含 HTTP 代理地址的 URI。 如果 `useSystemWebProxy` 设置为 `true`，则此设置必须为 `null`。 默认值为 `null`。|  
|`receiveTimeout`|一个 <xref:System.TimeSpan> 值，指定为完成接收操作提供的时间间隔。 此值应大于或等于 <xref:System.TimeSpan.Zero>。 默认值为 00:10:00。|  
|`sendTimeout`|一个 <xref:System.TimeSpan> 值，指定为完成发送操作提供的时间间隔。 此值应大于或等于 <xref:System.TimeSpan.Zero>。 默认值为 00:01:00。|  
|`textEncoding`|设置要用来在绑定上发出消息的字符集编码。 包括以下有效值：<br /><br /> BigEndianUnicodeUnicode BigEndian 编码。<br />Unicode16位编码。<br />UTF88位编码<br /><br /> 默认值为 UTF8。 此属性的类型为 <xref:System.Text.Encoding>。|  
|`transferMode`|一个有效的 <xref:System.ServiceModel.TransferMode> 值，指定为请求或响应对消息进行缓冲处理还是流式处理。|  
|`useDefaultWebProxy`|一个布尔值，指定是否应在可用时使用系统的自动配置 HTTP 代理。 默认值为 `true`。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<security>](security-of-basichttpbinding.md)|定义绑定的安全设置。 此元素的类型为 <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement>。|  
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|定义可由采用此绑定配置的终结点进行处理的 SOAP 消息的复杂性约束。 此元素的类型为 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<bindings>](bindings.md)|此元素包含标准绑定和自定义绑定的集合。|  
  
## <a name="remarks"></a>备注  
 BasicHttpBinding 使用 HTTP 作为传输协议来发送 SOAP 1.1 消息。 服务可以使用此绑定来公开符合 WS-I BP 1.1 标准的终结点，例如 ASMX 客户端使用的终结点。 同样，客户端可以使用 BasicHttpBinding 与公开符合 WS-I BP 1.1 标准的终结点的服务（如 ASMX Web 服务或采用 BasicHttpBinding 配置的服务）进行通信。  
  
 默认情况下, 安全设置处于关闭状态, 但可以将[ \<security >](security-of-basichttpbinding.md)子元素的 mode 属性设置为以外`None`的值。 默认情况下，它使用“Text”消息编码和 UTF-8 文本编码。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 <xref:System.ServiceModel.BasicHttpBinding> 提供 HTTP 通信以及与第一代和第二代 Web 服务的最大互操作性。 绑定是在客户端和服务的配置文件中指定的。 绑定类型是使用 `binding` 元素的 `<endpoint>` 属性指定的。 如果要配置基本绑定并更改它的某些设置，则必须定义一个绑定配置。 终结点必须使用 `bindingConfiguration` 元素的 `<endpoint>` 属性按名称引用绑定配置，如以下服务配置代码所示。  
  
```xml  
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="basicHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
  </services>
  <bindings>
    <basicHttpBinding>
      <binding name="Binding1"
               hostNameComparisonMode="StrongWildcard"
               receiveTimeout="00:10:00"
               sendTimeout="00:10:00"
               openTimeout="00:10:00"
               closeTimeout="00:10:00"
               maxReceivedMessageSize="65536"
               maxBufferSize="65536"
               maxBufferPoolSize="524288"
               transferMode="Buffered"
               messageEncoding="Text"
               textEncoding="utf-8"
               bypassProxyOnLocal="false"
               useDefaultWebProxy="true">
        <security mode="None" />
      </binding>
    </basicHttpBinding>
  </bindings>
</system.serviceModel>
```  
  
## <a name="example"></a>示例  
 从 [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)] 开始，不要求绑定和行为具有名称。 可以通过从终结点地址和绑定的名称中删除 bindingConfiguration 来完成上一示例中的功能。  
  
```xml  
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="basicHttpBinding"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
  </services>
  <bindings>
    <basicHttpBinding>
      <binding hostNameComparisonMode="StrongWildcard"
               receiveTimeout="00:10:00"
               sendTimeout="00:10:00"
               openTimeout="00:10:00"
               closeTimeout="00:10:00"
               maxReceivedMessageSize="65536"
               maxBufferSize="65536"
               maxBufferPoolSize="524288"
               transferMode="Buffered"
               messageEncoding="Text"
               textEncoding="utf-8"
               bypassProxyOnLocal="false"
               useDefaultWebProxy="true">
        <security mode="None" />
      </binding>
    </basicHttpBinding>
  </bindings>
</system.serviceModel>
```  
  
 有关默认配置和无值绑定和行为的详细信息, 请参阅[WCF 服务的](../../../wcf/samples/simplified-configuration-for-wcf-services.md)[简化配置](../../../wcf/simplified-configuration.md)和简化配置。  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Channels.Binding>
- <xref:System.ServiceModel.Channels.BindingElement>
- <xref:System.ServiceModel.BasicHttpBinding>
- <xref:System.ServiceModel.Configuration.BasicHttpBindingElement>
- [绑定](../../../wcf/bindings.md)
- [配置系统提供的绑定](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [使用绑定配置服务和客户端](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
