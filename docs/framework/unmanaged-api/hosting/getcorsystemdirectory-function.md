---
title: GetCORSystemDirectory 函数
ms.date: 03/30/2017
api_name:
- GetCORSystemDirectory
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetCORSystemDirectory
helpviewer_keywords:
- GetCORSystemDirectory function [.NET Framework hosting]
ms.assetid: 3dcd16a7-dafc-4ca8-b5cd-20ffb37db91d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d30384ea8b9ff4eee41abd43ae39486f770039e7
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70041428"
---
# <a name="getcorsystemdirectory-function"></a>GetCORSystemDirectory 函数
返回加载到进程中的公共语言运行时 (CLR) 的安装目录。 安装目录是完全限定的, 例如 "c:\windows\microsoft.net\framework\v1.0.3705"。  
  
 此函数已弃用。 它被 .NET Framework 4 中提供的[ICLRRuntimeInfo:: GetRuntimeDirectory](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getruntimedirectory-method.md)方法取代。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetCORSystemDirectory (   
    [out] LPWSTR  pbuffer,     
    [in]  DWORD   cchBuffer,   
    [out] DWORD*  dwlength  
);   
```  
  
## <a name="parameters"></a>参数  
 `pbuffer`  
 弄一个缓冲区, 其中运行时返回一个字符串, 其中包含加载到进程中的运行时的安装目录的完全限定名称。 如果运行时尚未加载到进程中, 则该函数将为计算机上安装的最新版本的运行时返回相应的目录信息。  
  
 `cchBuffer`  
 中的`pbuffer`大小 (以字节为单位)。  
  
 `dwLength`  
 弄中`pbuffer`返回的字符数。  
  
## <a name="remarks"></a>备注  
  
> [!CAUTION]
> 不要在运行 CLR 版本4的进程中使用此函数。 如果计算机上安装了 CLR 的早期版本, 则此函数将返回该版本的安装目录。  
  
## <a name="requirements"></a>要求  
 **适用**请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** MSCorEE.h  
  
 **类库**MSCorEE.dll  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [弃用的 CLR 承载函数](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
