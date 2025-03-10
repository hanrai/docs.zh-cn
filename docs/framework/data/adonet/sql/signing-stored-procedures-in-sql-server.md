---
title: 在 SQL Server 中对存储过程签名
ms.date: 01/05/2018
ms.assetid: eeed752c-0084-48e5-9dca-381353007a0d
ms.openlocfilehash: a30b5e28263c9f36e80c4e6b848033d5095b830b
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70043937"
---
# <a name="signing-stored-procedures-in-sql-server"></a>在 SQL Server 中对存储过程签名

数字签名是用签名人的私钥加密的数据摘要。 该私钥可确保数字签名对于其持有者或所有者是唯一的。 您可以对存储过程、函数 (内联表值函数除外)、触发器和程序集进行签名。

您可以使用证书或非对称密钥为存储过程签名。 此设计适用于无法通过所属权链继承权限或所属权链中断的方案，如动态 SQL。 然后, 你可以创建一个映射到该证书的用户, 并为该存储过程需要访问的对象授予证书用户权限。

您还可以创建一个映射到同一个证书的登录名, 然后向该登录名授予任何必需的服务器级权限, 或者将该登录名添加到一个或多个固定服务器角色中。 这是为了避免在需要更`TRUSTWORTHY`高级别权限的情况下启用数据库设置。

执行存储过程时, SQL Server 会将证书用户和/或登录的权限与调用方的权限进行组合。 `EXECUTE AS`与子句不同, 它不会更改过程的执行上下文。 返回登录名和用户名的内置函数会返回调用方的名称，而不是证书用户的名称。

## <a name="creating-certificates"></a>创建证书

使用证书或非对称密钥对存储过程进行签名时, 将使用私钥创建一个由存储过程代码的加密哈希和执行方式用户组成的数据摘要。 在运行时，数据摘要将使用公钥解密并与存储过程的哈希值进行比较。 更改 execute as 用户会使哈希值失效, 使数字签名不再匹配。 修改存储过程将完全删除该签名, 这会阻止无权访问私钥的用户更改存储过程代码。 在这两种情况下, 每次更改代码或执行方式用户时, 都必须对过程进行重新签名。

对模块进行签名涉及两个必需步骤:

1. 使用 Transact-SQL `CREATE CERTIFICATE [certificateName]` 语句创建一个证书。 此语句具有多个用于设置开始日期、结束日期和密码的选项。 默认的到期日期为一年。

1. 使用 Transact-SQL `ADD SIGNATURE TO [procedureName] BY CERTIFICATE [certificateName]` 语句通过证书为过程签名。

模块签名后, 需要创建一个或多个主体, 以便保存应该与证书关联的附加权限。

如果模块需要其他数据库级别权限:

1. 使用 Transact-SQL `CREATE USER [userName] FROM CERTIFICATE [certificateName]` 语句创建与该证书关联的数据库用户。 此用户仅存在于数据库中, 并且不与登录名相关联, 除非还使用同一证书创建了登录名。

1. 向证书用户授予所需的数据库级别权限。

如果模块需要其他服务器级别权限:

1. 将证书复制到`master`数据库。

1. 使用 transact-sql `CREATE LOGIN [userName] FROM CERTIFICATE [certificateName]`语句创建与该证书关联的登录名。

1. 向证书登录名授予必需的服务器级权限。

> [!NOTE]
> 证书不能向用户授予已经使用 DENY 语句撤消的权限。 DENY 始终优先于 GRANT，以防止调用方继承授予给证书用户的权限。

## <a name="external-resources"></a>外部资源

有关更多信息，请参见以下资源。

|资源|描述|
|--------------|-----------------|
|[模块登录](https://go.microsoft.com/fwlink/?LinkId=98590)SQL Server 联机丛书|说明模块签名，提供示例方案和到相关 Transact-SQL 主题的链接。|
|在 SQL Server 联机丛书中[使用证书对存储过程进行签名](/sql/relational-databases/tutorial-signing-stored-procedures-with-a-certificate)|提供有关使用证书为存储过程签名的教程。|

## <a name="see-also"></a>请参阅

- [保证 ADO.NET 应用程序的安全](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)
- [SQL Server 安全性概述](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)
- [SQL Server 中的应用程序安全性方案](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)
- [在 SQL Server 中使用存储过程管理权限](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)
- [在 SQL Server 中编写安全的动态 SQL](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)
- [在 SQL Server 中使用模拟自定义权限](../../../../../docs/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server.md)
- [使用存储过程修改数据](../../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
