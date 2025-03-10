---
title: dotnet run 命令
description: dotnet run 命令可便于使用源代码运行应用程序。
ms.date: 05/29/2018
ms.openlocfilehash: 0a6c1303bc12c256dd0a8923f9468620835ddabc
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70202804"
---
# <a name="dotnet-run"></a>dotnet run

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet run` - 无需任何显式编译或启动命令即可运行源代码。

## <a name="synopsis"></a>摘要

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

```console
dotnet run [-c|--configuration] [-f|--framework] [--force] [--launch-profile] [--no-build] [--no-dependencies]
    [--no-launch-profile] [--no-restore] [-p|--project] [--runtime] [-v|--verbosity] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

```console
dotnet run [-c|--configuration] [-f|--framework] [--force] [--launch-profile] [--no-build] [--no-dependencies]
    [--no-launch-profile] [--no-restore] [-p|--project] [--runtime] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```console
dotnet run [-c|--configuration] [-f|--framework] [-p|--project] [[--] [application arguments]]
dotnet run [-h|--help]
```

---

## <a name="description"></a>说明

`dotnet run` 命令为从源代码使用一个命令运行应用程序提供了一个方便的选项。 这对从命令行中进行快速迭代开发很有帮助。 命令取决于生成代码的 [`dotnet build`](dotnet-build.md) 命令。 对于此生成的任何要求，例如项目必须首先还原，同样适用于 `dotnet run`。

输出文件会写入到默认位置，即 `bin/<configuration>/<target>`。 例如，如果具有 `netcoreapp2.1` 应用程序并且运行 `dotnet run`，则输出置于 `bin/Debug/netcoreapp2.1`。 将根据需要覆盖文件。 临时文件将置于 `obj` 目录。

如果该项目指定多个框架，在不使用 `-f|--framework <FRAMEWORK>` 选项指定框架时，执行 `dotnet run` 将导致错误。

在项目上下文，而不是生成程序集中使用 `dotnet run` 命令。 如果尝试改为运行依赖于框架的应用程序 DLL，则必须在不使用命令的情况下使用 [dotnet](dotnet.md)。 例如，若要运行 `myapp.dll`，请使用：

```console
dotnet myapp.dll
```

有关 `dotnet` 驱动程序的详细信息，请参阅 [.NET Core 命令行工具 (CLI)](index.md) 主题。

若要运行应用程序，`dotnet run` 命令需从 NuGet 缓存解析共享运行时之外的应用程序依赖项。 因为它使用缓存的依赖项，因此，不推荐在生产中使用 `dotnet run` 来运行应用程序。 相反，使用 [`dotnet publish`](dotnet-publish.md)[ 命令创建部署](../deploying/index.md)，并部署已发布的输出。

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="options"></a>选项

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`--`

将参数分隔到正在运行的应用程序的参数的 `dotnet run`。 在此分隔符后的所有参数均传递给已运行的应用程序。

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`。

`-f|--framework <FRAMEWORK>`

使用指定[框架](../../standard/frameworks.md)生成并运行应用。 框架必须在项目文件中进行指定。

`--force`

强制解析所有依赖项，即使上次还原已成功，也不例外。 指定此标记等同于删除 project.assets.json 文件  。

`-h|--help`

打印出有关命令的简短帮助。

`--launch-profile <NAME>`

启动应用程序时要使用的启动配置文件（若有）的名称。 启动配置文件在 launchSettings.json 文件中进行定义，通常称为 `Development`、`Staging` 和 `Production`  。 有关详细信息，请参阅[使用多个环境](/aspnet/core/fundamentals/environments)。

`--no-build`

运行前不生成项目。 还隐式设置 `--no-restore` 标记。

`--no-dependencies`

当使用项目到项目 (P2P) 引用还原项目时，还原根项目，不还原引用。

`--no-launch-profile`

不尝试使用 launchSettings.json 配置应用程序  。

`--no-restore`

运行此命令时不执行隐式还原。

`-p|--project <PATH>`

指定要运行的项目文件的路径（文件夹名称或完整路径）。 如果未指定，则默认为当前目录。

`--runtime <RUNTIME_IDENTIFIER>`

指定要为其还原包的目标运行时。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。

`-v|--verbosity <LEVEL>`

设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`--`

将参数分隔到正在运行的应用程序的参数的 `dotnet run`。 在此分隔符后的所有参数均传递给已运行的应用程序。

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`。

`-f|--framework <FRAMEWORK>`

使用指定[框架](../../standard/frameworks.md)生成并运行应用。 框架必须在项目文件中进行指定。

`--force`

强制解析所有依赖项，即使上次还原已成功，也不例外。 指定此标记等同于删除 project.assets.json 文件  。

`-h|--help`

打印出有关命令的简短帮助。

`--launch-profile <NAME>`

启动应用程序时要使用的启动配置文件（若有）的名称。 启动配置文件在 launchSettings.json 文件中进行定义，通常称为 `Development`、`Staging` 和 `Production`  。 有关详细信息，请参阅[使用多个环境](/aspnet/core/fundamentals/environments)。

`--no-build`

运行前不生成项目。 还隐式设置 `--no-restore` 标记。

`--no-dependencies`

当使用项目到项目 (P2P) 引用还原项目时，还原根项目，不还原引用。

`--no-launch-profile`

不尝试使用 launchSettings.json 配置应用程序  。

`--no-restore`

运行此命令时不执行隐式还原。

`-p|--project <PATH>`

指定要运行的项目文件的路径（文件夹名称或完整路径）。 如果未指定，则默认为当前目录。

`--runtime <RUNTIME_IDENTIFIER>`

指定要为其还原包的目标运行时。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--`

将参数分隔到正在运行的应用程序的参数的 `dotnet run`。 在此分隔符后的所有参数均传递给已运行的应用程序。

`-c|--configuration {Debug|Release}`

定义生成配置。 默认值为 `Debug`。

`-f|--framework <FRAMEWORK>`

使用指定[框架](../../standard/frameworks.md)生成并运行应用。 框架必须在项目文件中进行指定。

`-h|--help`

打印出有关命令的简短帮助。

`-p|--project <PATH/PROJECT.csproj>`

指定项目文件的路径和名称。 （请参阅备注。）如果未指定，则默认为当前目录。

> [!NOTE]
> 通过 `-p|--project` 选项使用项目文件的路径和名称。 CLI 中的回归可阻止使用 .NET Core SDK 1.x 提供文件夹路径。 若要详细了解此问题，请参阅 [dotnet run -p - 无法启动项目 (dotnet/cli #5992)](https://github.com/dotnet/cli/issues/5992)。

---

## <a name="examples"></a>示例

运行当前目录中的项目：

`dotnet run`

运行指定的项目：

`dotnet run --project ./projects/proj1/proj1.csproj`

运行当前目录中的项目（在本例中，`--help` 参数被传递到应用程序，因为使用了空白的 `--` 选项）：

`dotnet run --configuration Release -- --help`

在当前仅显示最小输出的目录中还原项目的依赖项和工具，然后运行项目（.NET Core SDK 2.0 及更高版本）：

`dotnet run --verbosity m`
