---
title: ICorDebugThread 接口
ms.date: 03/30/2017
api_name:
- ICorDebugThread
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread
helpviewer_keywords:
- ICorDebugThread interface [.NET Framework debugging]
ms.assetid: 3930fd9b-2bc3-4b72-80a0-b6eeb94d60c6
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1517d686c50923f5599e33436e0ad6126e8be140
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923146"
---
# <a name="icordebugthread-interface"></a>ICorDebugThread 接口
表示进程中的线程。 `ICorDebugThread` 实例的生存期与它表示的线程的生存期相同。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[ClearCurrentException 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-clearcurrentexception-method.md)|未实现此方法。 请勿使用。|  
|[CreateEval 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-createeval-method.md)|创建一个对此`ICorDebugThread`运行的 ICorDebugEval 对象。|  
|[CreateStepper 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-createstepper-method.md)|创建一个 ICorDebugStepper 对象, 该对象允许单步执行此`ICorDebugThread`中的活动框架。|  
|[EnumerateChains 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-enumeratechains-method.md)|获取一个接口指针, 该指针指向包含此`ICorDebugThread`中所有堆栈链的 ICorDebugChainEnum 枚举器。|  
|[GetActiveChain 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getactivechain-method.md)|获取此`ICorDebugThread`上的活动 ICorDebugChain 的接口指针。|  
|[GetActiveFrame 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getactiveframe-method.md)|获取此`ICorDebugThread`上的活动 ICorDebugFrame 的接口指针。|  
|[GetAppDomain 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getappdomain-method.md)|获取一个接口指针, 该指针指向此`ICorDebugThread`当前正在执行的应用程序域。|  
|[GetCurrentException 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getcurrentexception-method.md)|获取一个指向 ICorDebugValue 对象的接口指针, 该对象表示当前由托管代码引发的异常。|  
|[GetDebugState 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getdebugstate-method.md)|获取描述此`ICorDebugThread`的当前调试状态的 CorDebugThreadState 值。|  
|[GetHandle 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-gethandle-method.md)|获取此`ICorDebugThread`的活动部分的当前句柄。|  
|[GetID 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getid-method.md)|获取此`ICorDebugThread`的活动部分的当前操作系统标识符。|  
|[GetObject 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getobject-method.md)|获取公共语言运行时 (CLR) 线程的接口指针。|  
|[GetProcess 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getprocess-method.md)|获取一个接口指针, 该指针指向此`ICorDebugThread`构成部分的进程。|  
|[GetRegisterSet 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getregisterset-method.md)|获取一个接口指针, 该指针指向与此`ICorDebugThread`关联的寄存器集。|  
|[GetUserState 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-getuserstate-method.md)|获取描述此`ICorDebugThread`的当前状态的 CorDebugUserState 值的按位组合。|  
|[SetDebugState 方法](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-setdebugstate-method.md)|设置描述此`ICorDebugThread`的调试`CorDebugThreadState`状态的值的按位组合。|  
  
## <a name="remarks"></a>备注  
  
> [!NOTE]
> 此接口不支持跨计算机或跨进程远程调用。  
  
## <a name="requirements"></a>要求  
 **适用**请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cordebug.idl, Cordebug.idl  
  
 **类库**CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [调试接口](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
