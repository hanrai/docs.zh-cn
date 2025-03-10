---
title: 缓解：WCF 服务和证书身份验证
ms.date: 03/30/2017
ms.assetid: ef19c91a-b9df-4bf0-a28e-eb1e99c4bc95
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b6ad11d4295be3a5bfd590d9cef1926f6676f2b1
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70043228"
---
# <a name="mitigation-wcf-services-and-certificate-authentication"></a>缓解：WCF 服务和证书身份验证

.NET Framework 4.6 向 WCF SSL 协议默认列表添加了 TLS 1.1 和 TLS 1.2。 客户端和服务器计算机都安装了 .NET Framework 4.6 或更高版本时，TLS 1.2 用于协商。

## <a name="impact"></a>影响

TLS 1.2 不支持 MD5 证书身份验证。 因此，如果客户使用的 SSL 证书对哈希算法使用 MD5，WCF 客户端就无法连接 WCF 服务。 有关详细信息，请参阅[缓解：WCF 服务和证书身份验证](../../../docs/framework/migration-guide/mitigation-wcf-services-and-certificate-authentication.md)。

## <a name="mitigation"></a>缓解

可以通过执行下列任一操作来解决此问题，以便 WCF 客户端可以连接 WCF 服务器：

- 将证书更新为不使用 MD5 算法。 建议采用此解决方案。

- 如果未在源代码中动态配置绑定，将应用程序的配置文件更新为使用 TLS 1.1 或更低版本的协议。 这样便可以继续将证书和 MD5 哈希算法结合使用。

  > [!CAUTION]
  > 不建议采用此解决方法，因为使用 MD5 哈希算法的证书被视为不安全。

  下面的配置文件就采用了此解决方法：

  ```xml
  <configuration>
      <system.serviceModel>
          <bindings>
              <netTcpBinding>
                  <binding>
                      <security mode= "None|Transport|Message|TransportWithMessageCredential" >
                          <transport clientCredentialType="None|Windows|Certificate"
                                              protectionLevel="None|Sign|EncryptAndSign"
                                              sslProtocols="Ssl3|Tls1|Tls11">
                          </transport>
                      </security>
                  </binding>
              </netTcpBinding>
          </bindings>
      </system.ServiceModel>
  </configuration>
  ```

- 如果在源代码中动态配置了绑定，将 <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=nameWithType> 属性更新为使用 TLS 1.1 (<xref:System.Security.Authentication.SslProtocols.Tls11?displayProperty=nameWithType>) 或源代码中的早期版本协议。

  > [!CAUTION]
  > 不建议采用此解决方法，因为使用 MD5 哈希算法的证书被视为不安全。

## <a name="see-also"></a>请参阅

- [运行时更改](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6.md)
