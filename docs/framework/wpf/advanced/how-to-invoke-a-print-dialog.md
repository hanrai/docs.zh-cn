---
title: 如何：调用打印对话框
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- invoking print dialogs [WPF]
- print dialogs [WPF], invoking
ms.assetid: e3a2c84c-74fe-45a4-8501-5813f9dbfed2
ms.openlocfilehash: cd7b06030e0fb2bba74590ee80c07c34047c5b47
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950613"
---
# <a name="how-to-invoke-a-print-dialog"></a>如何：调用打印对话框
若要提供从应用程序打印的功能, 只需创建并打开<xref:System.Windows.Controls.PrintDialog>对象即可。  
  
## <a name="example"></a>示例  
 <xref:System.Windows.Controls.PrintDialog> 控件为 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]、配置和 [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] 作业提交提供单一入口点。 控件易于使用, 并且可以通过使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]标记或代码来实例化。 下面的示例演示如何在代码中实例化和打开控件, 以及如何从代码中进行打印。 它还显示了如何确保对话框将为用户授予设置特定页面范围的选项。 示例代码假定在 C: 驱动器的根目录中有一个文件 FixedDocumentSequence。  
  
 [!code-csharp[printdialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PrintDialog/CSharp/Window1.xaml.cs#1)]
 [!code-vb[printdialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrintDialog/visualbasic/window1.xaml.vb#1)]  
  
 对话框打开后, 用户将能够从其计算机上安装的打印机中进行选择。 他们还可以选择[Microsoft XPS 文档编写器](https://go.microsoft.com/fwlink/?LinkId=147319)来创建[!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)]文件而不是打印。  
  
> [!NOTE]
> 本主题中[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]讨论的的<xref:System.Windows.Forms.PrintDialog?displayProperty=nameWithType>控件不应与 Windows 窗体的组件混淆。 <xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType>  
  
 严格地说, 您可以使用<xref:System.Windows.Controls.PrintDialog.PrintDocument%2A>方法, 而不必打开对话框。 在这种意义上, 控件可用作不可见的打印组件。 但出于性能原因, 最好是<xref:System.Printing.PrintQueue.AddJob%2A>使用方法, 或者使用的多个<xref:System.Windows.Xps.XpsDocumentWriter.Write%2A>和<xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A>方法<xref:System.Windows.Xps.XpsDocumentWriter>之一。 有关详细信息, 请参阅[以编程方式打印 XPS 文件](how-to-programmatically-print-xps-files.md)和。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Controls.PrintDialog>
- [WPF 中的文档](documents-in-wpf.md)
- [打印概述](printing-overview.md)
- [Microsoft XPS 文档编写器](https://go.microsoft.com/fwlink/?LinkId=147319)
