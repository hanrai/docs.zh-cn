---
title: 查看消息日志
ms.date: 03/30/2017
ms.assetid: 3012fa13-f650-45fb-aaea-c5cca8c7d372
ms.openlocfilehash: c926833a48331f191b6dcc3323f0dfda329b7014
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968671"
---
# <a name="viewing-message-logs"></a>查看消息日志
本主题描述如何查看消息日志。  
  
## <a name="viewing-message-logs-in-the-service-trace-viewer"></a>在服务跟踪查看器中查看消息日志  
 消息将在 WCF 处理时进行转换。 因此，记录的消息只反映记录时的消息内容，而不是网络上的内容。  
  
 由于消息日志记录的输出与消息的传输格式无关，因此，消息日志记录始终输出已解码的消息。 如果已正确配置消息日志记录，则记录的所有消息都应采用纯文本格式。 例如，使用二进制消息编码器不会影响已记录消息的格式（纯文本）。  
  
 XmlWriterTraceListener 的输出是一个包含一系列 XML 片段的文件。 请注意，该文件并不是有效的 XML 文件。 建议使用[服务跟踪查看器工具 (svctraceviewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)来查看消息日志文件。 有关如何使用此工具的详细信息, 请参阅[使用服务跟踪查看器查看相关跟踪和故障排除](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)。  
  
 在服务跟踪查看器中, 消息在 "**消息**" 选项卡中列出。导致处理错误或与处理错误相关的消息会以黄色（警告级别）或以红色（错误级别）突出显示，具体取决于错误的严重性。 双击消息会显示处理请求上下文中的消息跟踪。  
  
> [!NOTE]
> 如果消息没有标头，则不记录 `<header/>` 标记。  
  
## <a name="viewing-messages-logged-by-a-client-a-relay-and-a-service"></a>查看由客户端、中继和服务记录的消息  
 您的环境可能包含客户端，它将消息发送给中继，中继随后将消息转发给服务。 当在所有三个位置上启用消息日志记录, 并且在[服务跟踪查看器工具 (svctraceviewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)中同时查看所有三个消息日志时, 将错误地呈现消息日志交换。 这是因为消息头中的 `CorrelationId` 和 `ActivityId` 对于每个发送-接收对并不是唯一的。  
  
 您可以使用以下方法之一解决此问题。  
  
- 随时仅查看[服务跟踪查看器工具 (svctraceviewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)中三个消息日志中的两个。  
  
- 如果必须同时查看[服务跟踪查看器工具 (svctraceviewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)中的所有三个日志, 可以通过创建一个新<xref:System.ServiceModel.Channels.Message>实例来修改中继服务。 此实例应该是传入消息正文以及除 `ActivityId` 和 `Action` 标头以外所有标头的副本。 下面的示例代码演示如何执行该操作。  
  
```csharp
Message outgoingMessage = Message.CreateMessage(incomingMessage.Version, incomingMessage.Headers.Action, incomingMessage.GetReaderAtBodyContents());  
  
for (int i = 0; i < incomingMessage.Headers.Count; i++)  
{  
   if (incomingMessage.Headers[i].Name.Equals("ActivityId", StringComparison.InvariantCultureIgnoreCase) ||  
incomingMessage.Headers[i].Name.Equals("Action", StringComparison.InvariantCultureIgnoreCase))  
   {  
      continue;  
    }  
    outgoingMessage.Headers.CopyHeaderFrom(incomingMessage, i);  
}  
```  
  
## <a name="exceptional-cases-for-inaccurate-message-logging-content"></a>不准确消息日志记录内容的异常情况  
 在以下条件下，记录的消息可能不是网络上存在的八进制流的准确表示形式。  
  
- 对于 BasicHttpBinding，在 /addressing/none 命名空间中记录传入消息的信封标头。  
  
- 空格可能不匹配。  
  
- 对于传入消息，可能用不同形式表示空元素。 例如, \<标记 >\</tag > 而不是\<标记/>  
  
- 默认情况下或通过显式设置 enableLoggingKnownPii="true" 已禁用已知 PII 日志记录。  
  
- 已启用编码以转换到 UTF-8。  
  
## <a name="see-also"></a>请参阅

- [服务跟踪查看器工具 (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)
- [使用服务跟踪查看器查看相关跟踪和进行故障排除](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)
- [消息日志记录](../../../../docs/framework/wcf/diagnostics/message-logging.md)
