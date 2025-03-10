---
title: CoEEShutDownCOM 函数
ms.date: 03/30/2017
api_name:
- CoEEShutDownCOM
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoEEShutDownCOM
helpviewer_keywords:
- CoEEShutDownCOM function [.NET Framework hosting]
ms.assetid: b634cae2-632f-4737-9be4-92d0652844d7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 164384f043a1722ace6e5c4098cb31c4327cba1e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044059"
---
# <a name="coeeshutdowncom-function"></a>CoEEShutDownCOM 函数
强制公共语言运行时 (CLR) 释放它在运行时可调用包装 (RCW) 内包含的所有接口指针。 这就产生了释放所有 RCW 缓存的效果。 此全局函数在 .NET Framework 4 中已弃用。 相反, 请使用特定运行时的入口点。  
  
## <a name="syntax"></a>语法  
  
```cpp  
void CoEEShutDownCOM ();  
```  
  
## <a name="remarks"></a>备注  
 `CoEEShutDownCOM`函数首先释放所有上下文和所有缓存中的所有 rcw, 然后删除安装程序中的任何现有的弹出通知。 不发生 DLL 卸载。  
  
> [!CAUTION]
> 此函数影响加载到进程中的所有运行时。  
  
 从 .NET Framework 4 开始, 在你想要影响的特定运行时上调用此函数的入口点。 若要获取入口点, 请调用[ICLRRuntimeInfo:: GetProcAddress](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getprocaddress-method.md)方法, 并指定 "CoEEShutDownCOM"。  
  
## <a name="requirements"></a>要求  
 **适用**请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor  
  
 **类库**作为资源包括在 Mscoree.dll 中  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [元数据全局静态函数](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
