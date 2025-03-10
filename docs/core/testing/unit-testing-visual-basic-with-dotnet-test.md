---
title: 使用 dotnet test 和 xUnit 对 .NET Core 中的 Visual Basic 进行单元测试
description: 通过使用 dotnet test 和 xUnit 分步生成 Visual Basic 示例解决方案的交互体验，了解 .NET Core 中的单元测试概念。
author: billwagner
ms.author: wiwagn
ms.date: 09/01/2017
ms.custom: seodec18
ms.openlocfilehash: 867b6e3c9c647cd302b0635de1d02573485e89c7
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70168257"
---
# <a name="unit-testing-visual-basic-net-core-libraries-using-dotnet-test-and-xunit"></a>使用 dotnet test 和 xUnit 进行 Visual Basic .NET Core 库单元测试

本教程介绍分步构建示例解决方案的交互式体验，以了解单元测试概念。 如果希望使用预构建解决方案学习本教程，请在开始前[查看或下载示例代码](https://github.com/dotnet/samples/tree/master/core/getting-started/unit-testing-vb-dotnet-test)。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

## <a name="creating-the-source-project"></a>创建源项目

打开 shell 窗口。 创建一个名为 unit-testing-vb-using-dotnet-test  的目录，以保留该解决方案。
在此新目录中，运行 [`dotnet new sln`](../tools/dotnet-new.md) 创建新的解决方案。 此做法便于管理类库和单元测试项目。
在解决方案目录中，创建 PrimeService  目录。 目前目录和文件结构如下所示：

```console
/unit-testing-using-dotnet-test
    unit-testing-using-dotnet-test.sln
    /PrimeService
```

将 *PrimeService* 作为当前目录，然后运行 [`dotnet new classlib -lang VB`](../tools/dotnet-new.md) 以创建源项目。 将 Class1.VB  重命名为 PrimeService.VB  。 创建 `PrimeService` 类的失败实现：

```vb
Namespace Prime.Services
    Public Class PrimeService
        Public Function IsPrime(candidate As Integer) As Boolean
            Throw New NotImplementedException("Please create a test first")
        End Function
    End Class
End Namespace
```

将目录更改回 unit-testing-vb-using-dotnet-test  目录。 运行 [`dotnet sln add .\PrimeService\PrimeService.vbproj`](../tools/dotnet-sln.md) 向解决方案添加类库项目。

## <a name="creating-the-test-project"></a>创建测试项目

接下来，创建 PrimeService.Tests  目录。 下图显示了它的目录结构：

```console
/unit-testing-vb-using-dotnet-test
    unit-testing-vb-using-dotnet-test.sln
    /PrimeService
        Source Files
        PrimeService.vbproj
    /PrimeService.Tests
```

将 *PrimeService.Tests* 目录作为当前目录，并使用 [`dotnet new xunit -lang VB`](../tools/dotnet-new.md) 创建一个新项目。 此命令会创建将 xUnit 用作测试库的测试项目。 生成的模板在 PrimeServiceTests.vbproj  中配置了测试运行程序：

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0-preview-20170628-02" />
  <PackageReference Include="xunit" Version="2.2.0" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0" />
</ItemGroup>
```

测试项目需要其他包创建和运行单元测试。 `dotnet new` 在以前的步骤中已添加 xUnit 和 xUnit 运行程序。 现在，将 `PrimeService` 类库作为另一个依赖项添加到项目中。 使用 [`dotnet add reference`](../tools/dotnet-add-reference.md) 命令：

```console
dotnet add reference ../PrimeService/PrimeService.vbproj
```

可以在 GitHub 上的[示例存储库](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-vb-dotnet-test/PrimeService.Tests/PrimeService.Tests.vbproj)中看到整个文件。

最终的文件夹布局将如下所示：

```console
/unit-testing-using-dotnet-test
    unit-testing-using-dotnet-test.sln
    /PrimeService
        Source Files
        PrimeService.vbproj
    /PrimeService.Tests
        Test Source Files
        PrimeServiceTests.vbproj
```

在 unit-testing-vb-using-dotnet-test  目录中执行 [`dotnet sln add .\PrimeService.Tests\PrimeService.Tests.vbproj`](../tools/dotnet-sln.md)。 

## <a name="creating-the-first-test"></a>创建第一个测试

编写一个失败测试，使其通过，然后重复此过程。 从 PrimeService.Tests  目录删除 UnitTest1.vb  ，并创建一个名为 PrimeService_IsPrimeShould.VB  的新 Visual Basic 文件。 添加以下代码：

```vb
Imports Xunit

Namespace PrimeService.Tests
    Public Class PrimeService_IsPrimeShould
        Private _primeService As Prime.Services.PrimeService = New Prime.Services.PrimeService()

        <Fact>
        Sub IsPrime_InputIs1_ReturnFalse()
            Dim result As Boolean = _primeService.IsPrime(1)

            Assert.False(result, "1 should not be prime")
        End Sub

    End Class
End Namespace
```

`<Fact>` 属性表示由测试运行程序运行的测试方法。 在 unit-testing-using-dotnet-test  中，执行 [`dotnet test`](../tools/dotnet-test.md) 以构建测试和类库，然后运行测试。 xUnit 测试运行程序包含要运行测试的程序入口点。 `dotnet test` 使用已创建的单元测试项目启动测试运行程序。

测试失败。 尚未创建实现。 在起作用的 `PrimeService` 类中编写最简单的代码，使此测试通过：

```vb
Public Function IsPrime(candidate As Integer) As Boolean
    If candidate = 1 Then
        Return False
    End If
    Throw New NotImplementedException("Please create a test first.")
End Function
```

在 unit-testing-vb-using-dotnet-test  目录中，再次运行 `dotnet test`。 `dotnet test` 命令构建 `PrimeService` 项目，然后构建 `PrimeService.Tests` 项目。 构建这两个项目后，该命令将运行此单项测试。 测试通过。

## <a name="adding-more-features"></a>添加更多功能

你已经通过了一个测试，现在可以编写更多测试。 质数有其他几种简单情况：0、-1。 可以将这些情况添加为具有 `<Fact>` 属性的新测试，但这很快就会变得枯燥乏味。 还有其他 xUnit 属性，可使你编写类似测试套件。  `<Theory>` 属性表示执行相同代码，但具有不同输入参数一系列测试。 可以使用 `<InlineData>` 属性来指定这些输入的值。

可以不使用这两个属性创建新测试，而用来创建单个索引。 此索引是测试多个小于 2（即最小的质数）的值的方法：

[!code-vb[Sample_TestCode](../../../samples/core/getting-started/unit-testing-vb-dotnet-test/PrimeService.Tests/PrimeService_IsPrimeShould.vb?name=Sample_TestCode)]

运行 `dotnet test`，两项测试均失败。 若要使所有测试通过，可以更改方法开头的 `if` 子句：

```vb
if candidate < 2
```

通过在主库中添加更多测试、理论和代码继续循环访问。 你将拥有[已完成的测试版本](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-vb-dotnet-test/PrimeService.Tests/PrimeService_IsPrimeShould.vb)和[库的完整实现](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-vb-dotnet-test/PrimeService/PrimeService.vb)。

你已生成一个小型库和该库的一组单元测试。 你已将解决方案结构化，使添加新包和新测试成为了正常工作流的一部分。 你已将多数的时间和精力集中在解决应用程序的目标上。
