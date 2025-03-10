---
title: 缺少运行时间项目异常类 (.NET Native)
ms.date: 03/30/2017
ms.assetid: d5b3d13e-689f-4584-8ba6-44f5167a8590
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: caa929225701a62c0abb3b335bfd7fb6a129e9e3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69941628"
---
# <a name="missingruntimeartifactexception-class-net-native"></a>缺少运行时间项目异常类 (.NET Native)
**适用于 Windows 10 的 .NET for Windows apps, 仅 .NET Native**  
  
 当一个类型或类型成员的元数据可用但其实现已遭到删除时会引发此异常。  
  
 **命名空间：** System.Reflection  
  
> [!IMPORTANT]
> `MissingRuntimeArtifactException`类仅供 .NET Native 工具链内部使用。 它不用于在第三方代码中使用，也不应用它处理应用程序代码中的异常。 相反，你可以通过将条目添加到[运行时指令文件](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)来消除异常。 有关详细信息，请参阅“备注”部分。  
  
## <a name="syntax"></a>语法  
 [!code-csharp[ProjectN#22](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missingruntimeartifactexception_syntax1.cs#22)]  
  
 请注意，`MissingRuntimeArtifactException` 类派生自 <xref:System.MemberAccessException>。  
  
 `MissingRuntimeArtifactException` 类包含以下成员：  
  
## <a name="constructors"></a>构造函数  
  
|构造函数|描述|  
|-----------------|-----------------|  
|`public MissingRuntimeArtifactException()`|通过使用一个系统提供的、描述该错误的消息，来初始化 `MissingRuntimeArtifactException` 类的一个实例。<br /><br /> 此构造函数仅供 .NET Native 工具链内部使用。|  
|`public MissingRuntimeArtifactException(String message)`|用指定的错误消息初始化 `MissingRuntimeArtifactException` 类的新实例。<br /><br /> 此构造函数仅供 .NET Native 工具链内部使用。|  
  
## <a name="properties"></a>属性  
  
|属性|描述|  
|--------------|-----------------|  
|`public IDictionary Data { get; }`|获取提供有关异常的其他用户定义信息的键/值对集合。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`public string HelpLink { get; set; }`|获取或设置指向与此异常关联的帮助文件链接。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`public int HResult { get; protected set; }`|获取/设置 `HRESULT`，即分配给一个特定异常的编码数值。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`public Exception InnerException { get; }`|获取导致当前异常的异常。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`public string Message { get; }`|获取描述当前异常的消息。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`public string Source { get; set; }`|获取或设置导致错误的应用程序名称或对象。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`public string StackTrace { get; }`|获取调用堆栈上的即时框架字符串表示形式。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`public MethodBase TargetSite { get; }`|获取引发当前异常的方法。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|`public bool Equals(Object obj)`|确定指定的对象是否等于当前对象。  （从 <xref:System.Object> 继承。）|  
|`protected void Finalize()`|在垃圾回收将某一对象回收前允许该对象尝试释放资源并执行其他清理操作。 （从 <xref:System.Object> 继承。）|  
|`public Exception GetBaseException()`|返回是一个或多个后续异常的根源的异常。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`public int GetHashCode()`|为 `MissingRuntimeArtifactException` 实例返回一个哈希代码。   （从 <xref:System.Object> 继承。）|  
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|设置一个包含有关异常信息的 <xref:System.Runtime.Serialization.SerializationInfo> 对象。  （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`public Type GetType()`|获取当前实例的运行时类型。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
|`protected Object MemberwiseClone()`|创建当前对象的卷影副本。 （从 <xref:System.Object> 继承。）|  
|`public string ToString()`|返回当前异常的字符串表示形式。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
  
## <a name="events"></a>事件  
  
|Event|描述|  
|-----------|-----------------|  
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|当异常被序列化用来创建包含有关该异常的徐列出数据的异常状态对象时会出现该问题。 （从 <xref:System.Exception?displayProperty=nameWithType> 继承。）|  
  
## <a name="usage-details"></a>使用详情  
 当试图实例化一个类型或调用一个类型成员，并且尽管类型或成员的元数据存在但其实现已遭到删除的情况下，会引发 `MissingRuntimeArtifactException` 异常。  
  
 应用程序在运行时是否可以使用元数据和实现代码来动态执行方法是由运行时指令 (XML 配置) 文件 ( \*web.config) 定义的。 为防止应用引发此异常，必须修改 \*.rd.xml，确保一个类型或类型成员需要的元数据在运行时存在。 有关 \*.rd.xml 文件的格式信息，请参阅[运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)。  
  
> [!IMPORTANT]
> 由于此异常表示应用程序需要的实现代码在运行时间不可用，你不必在 `try`/`catch` 块中处理此异常。 相反，你应该诊断引起此异常的原因并通过使用运行时指令文件删除它。 通常, 可以通过在运行时指令文件 ( `Activate` \*.xml `Dynamic`文件) 中为程序元素指定合适的或策略来消除此异常。 若要获取可以添加到可消除异常的运行时指令文件的项，有两个疑难解答程序可供使用：  
>   
> - 类型的 [MissingMetadataException 故障排除程序](https://dotnet.github.io/native/troubleshooter/type.html) 。  
> - 方法的 [MissingMetadataException 故障排除程序](https://dotnet.github.io/native/troubleshooter/method.html) 。  
  
 `MissingRuntimeArtifactException` 类不包括独有成员；它的所有成员都是从其基类即 <xref:System.MemberAccessException> 继承的。  
  
## <a name="see-also"></a>请参阅

- [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)
- [运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)
