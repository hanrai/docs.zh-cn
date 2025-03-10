---
title: dotnet pack 命令
description: dotnet pack 命令可为 .NET Core 项目创建 NuGet 包。
ms.date: 12/04/2018
ms.openlocfilehash: c5c00f3bb06e5bc5579c0d3d6bdd39fbdf3db656
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2019
ms.locfileid: "70202840"
---
# <a name="dotnet-pack"></a>dotnet pack

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet pack` - 将代码打包到 NuGet 包。

## <a name="synopsis"></a>摘要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

```console
dotnet pack [<PROJECT>] [-c|--configuration] [--force] [--include-source] [--include-symbols] [--no-build] [--no-dependencies]
    [--no-restore] [-o|--output] [--runtime] [-s|--serviceable] [-v|--verbosity] [--version-suffix]
dotnet pack [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```console
dotnet pack [<PROJECT>] [-c|--configuration] [--include-source] [--include-symbols] [--no-build] [-o|--output]
    [-s|--serviceable] [-v|--verbosity] [--version-suffix]
dotnet pack [-h|--help]
```

---

## <a name="description"></a>说明

`dotnet pack` 命令生成项目并创建 NuGet 包。 该命令的结果是一个 NuGet 包。 如果 `--include-symbols` 选项存在，则创建包含调试符号的另一个包。

将被打包项目的 NuGet 依赖项添加到 *.nuspec* 文件，以便在安装包时可以进行正确解析。 项目到项目的引用不会打包到项目内。 目前，如果具有项目到项目的依赖项，则每个项目均必须包含一个包。

默认情况下，`dotnet pack` 先构建项目。 如果希望避免此行为，则传递 `--no-build` 选项。 此选项在持续集成 (CI) 生成方案中通常非常有用，你可以知道代码是之前生成的。

可向 `dotnet pack` 命令提供 MSBuild 属性，用于打包进程。 有关详细信息，请参阅 [NuGet 元数据属性](csproj.md#nuget-metadata-properties)和 [MSBuild 命令行引用](/visualstudio/msbuild/msbuild-command-line-reference)。 [示例](#examples)部分介绍了如何在不同的情况下使用 MSBuild -p 开关。

默认情况下，Web 项目不可打包。 若要覆盖默认行为，请将以下属性添加到 .csproj  文件中：

```xml
<PropertyGroup>
   <IsPackable>true</IsPackable>
</PropertyGroup>
```

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="arguments"></a>自变量

* **`PROJECT`**

  要打包的项目。 它可能是 [csproj 文件](csproj.md)或目录的路径。 如果未指定，则默认为当前目录。

## <a name="options"></a>选项

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

* **`-c|--configuration {Debug|Release}`**

  定义生成配置。 默认值为 `Debug`。

* **`--force`**

  强制解析所有依赖项，即使上次还原已成功，也不例外。 指定此标记等同于删除 project.assets.json 文件  。

* **`-h|--help`**

  打印出有关命令的简短帮助。

* **`--include-source`**

  将源文件包括在 NuGet 包中。 源文件包括在 `nupkg` 内的 `src` 文件夹中。

* **`--include-symbols`**

  生成符号 `nupkg`。

* **`--no-build`**

  打包前不生成项目。 还将隐式设置 `--no-restore` 标记。

* **`--no-dependencies`**

  忽略项目间引用，仅还原根项目。

* **`--no-restore`**

  运行此命令时不执行隐式还原。

* **`-o|--output <OUTPUT_DIRECTORY>`**

  将生成的包放置在指定目录。

* **`--runtime <RUNTIME_IDENTIFIER>`**

  指定要为其还原包的目标运行时。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。

* **`-s|--serviceable`**

  设置包中可用的标志。 有关详细信息，请参阅 [.NET 博客：.NET 4.5.1 支持 .NET NuGet 库的 Microsoft 安全更新](https://aka.ms/nupkgservicing)。

* **`--version-suffix <VERSION_SUFFIX>`**

  定义项目中 `$(VersionSuffix)` MSBuild 属性的值。

* **`-v|--verbosity <LEVEL>`**

  设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

* **`-c|--configuration {Debug|Release}`**

  定义生成配置。 默认值为 `Debug`。

* **`-h|--help`**

  打印出有关命令的简短帮助。

* **`--include-source`**

  将源文件包括在 NuGet 包中。 源文件包括在 `nupkg` 内的 `src` 文件夹中。

* **`--include-symbols`**

  生成符号 `nupkg`。

* **`--no-build`**

  打包前不生成项目。

* **`-o|--output <OUTPUT_DIRECTORY>`**

  将生成的包放置在指定目录。

* **`-s|--serviceable`**

  设置包中可用的标志。 有关详细信息，请参阅 [.NET 博客：.NET 4.5.1 支持 .NET NuGet 库的 Microsoft 安全更新](https://aka.ms/nupkgservicing)。

* **`--version-suffix <VERSION_SUFFIX>`**

  定义项目中 `$(VersionSuffix)` MSBuild 属性的值。

* **`-v|--verbosity <LEVEL>`**

  设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

---

## <a name="examples"></a>示例

* 打包当前目录中的项目：

  ```console
  dotnet pack
  ```

* 打包 `app1` 项目：

  ```console
  dotnet pack ~/projects/app1/project.csproj
  ```

* 打包当前目录中的项目并将生成的包放置到 `nupkgs` 文件夹：

  ```console
  dotnet pack --output nupkgs
  ```

* 将当前目录中的项目打包到 `nupkgs` 文件夹并跳过生成步骤：

  ```console
  dotnet pack --no-build --output nupkgs
  ```

* 将项目的版本后缀配置为 *.csproj* 文件中的 `<VersionSuffix>$(VersionSuffix)</VersionSuffix>`，使用给定的后缀打包当前项目，并更新生成的程序包版本：

  ```console
  dotnet pack --version-suffix "ci-1234"
  ```

* 使用 `PackageVersion` MSBuild 属性将包版本设置为 `2.1.0`：

  ```console
  dotnet pack -p:PackageVersion=2.1.0
  ```

* 打包特定[目标框架](../../standard/frameworks.md)的项目：

  ```console
  dotnet pack -p:TargetFrameworks=net45
  ```

* 打包项目，并使用特定运行时 (Windows 10) 进行还原操作（.NET Core SDK 2.0 及更高版本）：

  ```console
  dotnet pack --runtime win10-x64
  ```

* 使用 [.nuspec 文件](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-using-a-nuspec)打包项目：

  ```console
  dotnet pack ~/projects/app1/project.csproj /p:NuspecFile=~/projects/app1/project.nuspec /p:NuspecBasePath=~/projects/app1/nuget
  ```
