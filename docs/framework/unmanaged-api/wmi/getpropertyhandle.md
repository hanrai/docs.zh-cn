---
title: GetPropertyHandle 函数 (非托管 API 参考)
description: GetPropertyHandle 函数返回标识属性的唯一句柄。
ms.date: 11/06/2017
api_name:
- GetPropertyHandle
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetPropertyHandle
helpviewer_keywords:
- GetPropertyHandle function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d6dc2792b572aae30e9989c81967b86f340d7b83
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69038263"
---
# <a name="getpropertyhandle-function"></a>GetPropertyHandle 函数

返回标识属性的唯一句柄。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>语法

```cpp
HRESULT GetPropertyHandle (
   [in] int                  vFunc,
   [in] IWbemObjectAccess*   ptr,
   [in] LPCWSTR              wszPropertyName,
   [out] CIMTYPE*            pType,
   [out] long*               pHandle
);
```

## <a name="parameters"></a>参数

`vFunc`\
中此参数未使用。

`ptr`\
中指向[IWbemObjectAccess](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess)实例的指针。

`wszPropertyName`\
中以 null 结尾的 UTF16 编码字符的字符串, 其中包含属性名称。

`pType`\
弄一个指针, 指向[`CIMTYPE`](/windows/win32/api/wbemcli/ne-wbemcli-cimtype_enumeration)表示属性的 CIM 类型的枚举成员。

`pHandle`\
弄指向包含属性句柄的整数的指针。

## <a name="return-value"></a>返回值

此函数返回的以下值是在*WbemCli*头文件中定义的, 也可以在代码中将它们定义为常量:

|返回的常量  |值  |描述  |
|---------|---------|---------|
|`WBEM_E_NOT_FOUND` | 0x80041002 | 找不到指定的属性名。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 参数无效。 |
|`WBEM_E_NOT_SUPPORTED` | 0x8004100c | 请求的属性的类型`CIM_OBJECT`为或。 `CIM_ARRAY` |
|`WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |

## <a name="remarks"></a>备注

此函数包装对[IWbemClassObject:: GetPropertyHandle](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemobjectaccess-getpropertyhandle)方法的调用。

使用[IWbemObjectAccess](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess)方法读取或写入属性值时, 可以使用此句柄来确定属性。

对于除`CIM_OBJECT`和`CIM_ARRAY`之外的所有数据类型的属性, 可以检索句柄。 返回的句柄在类的所有实例中工作。

## <a name="requirements"></a>要求

**适用**请参阅[系统需求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** WMINet_Utils.idl

**.NET Framework 版本：** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>请参阅

- [WMI 和性能计数器 (非托管 API 参考)](index.md)
