---
title: Web 和套接字权限
ms.date: 03/30/2017
helpviewer_keywords:
- Networking
- positions [.NET Framework], accepting
- sockets, permissions
- network, permissions
- Internet, permissions
- Network Resources
- SocketPermission class, about SocketPermission class
- positions [.NET Framework], connecting
- WebPermission class, about WebPermission class
- permissions [.NET Framework], sockets
- security [.NET Framework], Internet
- positions [.NET Framework], granting
ms.assetid: d51ad8cb-03ae-4a51-bfcd-cfcf6b98afa9
ms.openlocfilehash: fbb4e5d7171c50c06f55706df90240ffa205ee73
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967623"
---
# <a name="web-and-socket-permissions"></a>Web 和套接字权限
<xref:System.Net.WebPermission> 和 <xref:System.Net.SocketPermission> 类为使用 <xref:System.Net> 命名空间的应用程序提供网络安全性。 WebPermission 类控制应用程序从 URI 请求数据或向 Internet 提供 URI 的权限。  SocketPermission 类控制应用程序使用 <xref:System.Net.Sockets.Socket> 在本地端口接受数据或使用传输协议连接其他地址的远程设备的权限（基于主机、端口号和套接字的传输协议）。   
  
 权限类的选择取决于应用程序的类型。 使用 <xref:System.Net.WebRequest> 的应用程序及其子代应使用 WebPermission 类来管理权限。  使用套接字级别访问权限的应用程序及其子代应使用 SocketPermission 类来管理权限。   
  
 WebPermission 和 SocketPermission 定义两种权限：接受和连接。   “接受”授予应用程序应答来自其他参与方的传入连接的权限。 “连接”授予应用程序向其他参与方发起连接的权限。  
  
 对于 SocketPermission 实例，“接受”意味着应用程序可以在本地传输地址上接受传入的连接；“连接”意味着应用程序可以连接到某个远程（或本地）传输地址。   
  
 对于 WebPermission 实例，“接受”意味着应用程序可以将 WebPermission 控制的 URI 导出到外界；“连接”意味着应用程序可以访问该 URI（无论它是远程还是本地的）。    
  
## <a name="see-also"></a>请参阅

- [安全性](../../standard/security/index.md)
- [网络编程中的安全性](../../../docs/framework/network-programming/security-in-network-programming.md)
