---
title: <httpDigest> 元素
ms.date: 03/30/2017
ms.assetid: 3da4f276-dfd9-4247-8c07-01d83618727c
ms.openlocfilehash: 2ceefdd7fab82025e89ad08d8423d57524c2e4d8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925565"
---
# <a name="httpdigest-element"></a>\<httpDigest > 元素
指定一个在向服务证明客户端身份时使用的摘要类型凭据。  
  
 \<system.ServiceModel>  
\<行为 >  
\<endpointBehaviors>  
\<行为 >  
\<clientCredentials>  
\<httpDigest>  
  
## <a name="syntax"></a>语法  
  
```xml  
<digest impersonationLevel="Identification/Impersonation/Delegation/Anonymous/None" />
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`impersonationLevel`|设置客户端用于与服务器进行通信的模拟首选项。 服务器上不强制使用客户端所选择的模拟模式。 包括以下有效值：<br /><br /> 标识服务器可以获取客户端的标识和特权, 但不能模拟客户端。<br />模仿服务器可以在本地系统上模拟客户端的安全上下文。<br />委托服务器可以模拟客户端在远程系统上的安全上下文。<br />匿名服务器无法模拟或标识客户端。<br />内容未分配模拟级别。<br /><br /> 默认值为 Identification。 此属性的类型为 <xref:System.Security.Principal.TokenImpersonationLevel>。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|指定用于向服务验证客户端身份的凭据。|  
  
## <a name="remarks"></a>备注  
 摘要是使用算法和一组输入确定的哈希。 身份验证器和被验证方一致同意某种算法并交换用作输入的数据。 客户端可以计算哈希并将其发送给服务。 服务也可以计算哈希并比较值。 如果匹配，则客户端将通过验证。  
  
 必须使用 Windows 上的 Active Directory 和 Internet 信息服务 (IIS) 启用此功能。 有关详细信息, 请参阅[IIS 6.0 中的摘要式身份验证](https://go.microsoft.com/fwlink/?LinkId=88443)。  
  
## <a name="see-also"></a>请参阅

- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.HttpDigest%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.HttpDigest%2A>
- <xref:System.ServiceModel.Configuration.HttpDigestClientElement>
- <xref:System.ServiceModel.Security.HttpDigestClientCredential>
- [安全行为](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [保护客户端](../../../wcf/securing-clients.md)
- [使用证书](../../../wcf/feature-details/working-with-certificates.md)
- [保护服务和客户端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
