---
title: 托管线程中的异常
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- unhandled exceptions,in managed threads
- threading [.NET Framework],unhandled exceptions
- threading [.NET Framework],exceptions in managed threads
- managed threading
ms.assetid: 11294769-2e89-43cb-890e-ad4ad79cfbee
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 689ee44980a4a41b6d46ed9b68306c1b08c49586
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960061"
---
# <a name="exceptions-in-managed-threads"></a>托管线程中的异常
从 .NET Framework 2.0 版开始，公共语言运行时允许线程中的多数未经处理的异常正常继续。 在多数情况下，这意味着未经处理的异常会导致应用程序终止。  
  
> [!NOTE]
> 这是对 .NET Framework 1.0 和 1.1 版的重要更改，这两个版本对许多未经处理的异常（例如，线程池线程中未经处理的异常）提供支持。 请参阅本主题后面的[对先前版本的更改](#ChangeFromPreviousVersions)。  
  
 公共语言运行时为用于控制程序流的某些未经处理的异常提供支持：  
  
- 由于 <xref:System.Threading.Thread.Abort%2A> 得到调用，因此 <xref:System.Threading.ThreadAbortException> 在线程中抛出。  
  
- 由于线程执行时所在的应用域正在卸载，因此 <xref:System.AppDomainUnloadedException> 在线程中抛出。  
  
- 公共语言运行时或主机进程通过引发内部异常来终止线程。  
  
 如果公共语言运行时所创建的线程中未处理这些异常中的任何一个，则异常会终止线程，但公共语言运行时不允许该异常继续下去。  
  
 如果在主线程或从非托管代码进入运行时的线程中未处理这些异常，则它们会正常继续，并导致应用程序终止。  
  
> [!NOTE]
> 运行时有可能在任何托管代码有机会安装异常处理程序之前，引发一个未经处理的异常。 即使托管代码没有机会处理此类异常，仍允许异常正常继续。  
  
## <a name="exposing-threading-problems-during-development"></a>在开发过程中暴露线程处理问题  
 如果允许线程不给出任何提示就失败（不终止应用程序），则可能无法检测出重大的编程问题。 对于长时间运行的服务和其他应用程序，此问题尤为严重。 当线程失败时，程序状态会逐渐损坏。 应用程序性能可能会降低，应用程序也可能无响应。  
  
 如果允许线程中未经处理的异常正常继续，直到操作系统终止程序为止，将会在开发和测试过程中暴露此类问题。 程序终止的错误报告支持调试。  
  
<a name="ChangeFromPreviousVersions"></a>   
## <a name="change-from-previous-versions"></a>对先前版本的更改  
 最重要的更改发生在托管线程上。 在 .NET Framework 1.0 和 1.1 版中，公共语言运行时在下列情况下为未经处理的异常提供支持：  
  
- 在线程池线程中，没有诸如未经处理的异常这样的内容。 当某个任务引发了它无法处理的异常时，运行时会将异常堆栈跟踪打印至控制台，然后将线程返回至线程池。  
  
- 在使用 <xref:System.Threading.Thread> 类的 <xref:System.Threading.Thread.Start%2A> 方法创建的线程中，不存在未经处理的异常等现象。 当在此类线程中运行的代码引发它无法处理的异常时，运行时会将异常堆栈跟踪打印至控制台，然后正常终止线程。  
  
- 在终结器线程中，没有诸如未经处理的异常这样的内容。 当终结器引发它无法处理的异常时，运行时会将异常堆栈跟踪打印至控制台，然后允许终结器线程继续运行终结器。  
  
 托管线程的前台或后台状态不会影响此行为。  
  
 对于发自非托管代码的线程中的未经处理的异常，差别更加细微。 运行时 JIT 附加对话会抢占已通过本机代码的线程中的托管异常或本机异常的操作系统对话。 无论什么情况，进程都会终止。  
  
### <a name="migrating-code"></a>迁移代码  
 通常，更改将暴露以前无法识别的编程问题，以便修复这些问题。 但在某些情况下，程序员可能已经利用了运行时支持，例如用于终止线程。 根据具体情况，他们应考虑以下迁移策略之一：  
  
- 重构代码，以便接收到信号时线程能够正常退出。  
  
- 使用 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 方法中止线程。  
  
- 如果线程必须停止才能使进程终止，请将该线程设置为后台线程，这样它就会在进程退出时自动终止。  
  
 在所有情况下，迁移策略均应遵循异常设计准则。 请参阅[异常设计准则](../../../docs/standard/design-guidelines/exceptions.md)。  
  
### <a name="application-compatibility-flag"></a>应用程序兼容性标志  
 作为临时的兼容性措施，管理员可以将兼容性标志放在应用程序配置文件的 `<runtime>` 节中。 这会导致公共语言运行时回到 1.0 和 1.1 版的行为。  
  
```xml  
<legacyUnhandledExceptionPolicy enabled="1"/>  
```  
  
## <a name="host-override"></a>主机重写  
 在 .NET Framework 2.0 版中，非托管主机可以使用宿主 API 中的 [ICLRPolicyManager](../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md) 接口来重写公共语言运行时的默认未经处理的异常。 [ICLRPolicyManager::SetUnhandledExceptionPolicy](../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setunhandledexceptionpolicy-method.md) 函数用于设置未经处理的异常的策略。  
  
## <a name="see-also"></a>请参阅

- [托管线程处理基本知识](../../../docs/standard/threading/managed-threading-basics.md)
