---
title: 图像处理概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- metadata [WPF], images
- displaying images [WPF]
- Imaging API [WPF]
- image metadata [WPF]
- converting images [WPF]
- encoding image formats [WPF]
- format decoding for images [WPF]
- painting with images [WPF]
- stretching images [WPF]
- images [WPF], about imaging
- format encoding for images [WPF]
- cropping images [WPF]
- decoding image formats [WPF]
- rotating images [WPF]
ms.assetid: 72aad87a-e6f3-4937-94cd-a18b7766e990
ms.openlocfilehash: 13d5ea2735a799332edd8e552198de0f2b970dad
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69914099"
---
# <a name="imaging-overview"></a>图像处理概述
本主题介绍 [!INCLUDE[TLA#tla_wic](../../../../includes/tlasharptla-wic-md.md)]。 借助 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]，开发人员可以显示、转换图像和设置图像的格式。  

## <a name="wpf-imaging-component"></a>WPF 图像处理组件  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 使得 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 内的图像处理功能得到了极大改进。 映像功能 (如显示位图或在公共控件上使用图像) 以前依赖于 Microsoft Windows 图形设备接口 (GDI) 或 Microsoft Windows GDI + 库。 这些 API 提供基线映像功能, 但缺乏功能, 如支持编解码器扩展性和高保真图像支持。 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]旨在克服 GDI 和 GDI + 的缺点, 并提供一组新的 API, 用于在应用程序中显示和使用图像。  
  
 可以通过两种方法访问[!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] API、托管组件和非托管组件。 非托管组件提供以下功能。  
  
- 适用于新的或专用图像格式的扩展性模型。  
  
- 改进了本机映像格式的性能和安全性, 包括位图 (BMP)、联合图像专家组 (JPEG)、可移植网络图形 ( [!INCLUDE[TLA#tla_tiff](../../../../includes/tlasharptla-tiff-md.md)]PNG [!INCLUDE[TLA#tla_wdp](../../../../includes/tlasharptla-wdp-md.md)])、、、图形交换格式 (GIF) 和图标 (.ico)。  
  
- 高位深图像数据最多保留 8 位/通道（32 位/像素）。  
  
- 非破坏性图像缩放、剪切和旋转。  
  
- 简化的颜色管理。  
  
- 对文件内的专用元数据的支持。  
  
- 托管组件利用非托管基础结构提供图像与其他 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 功能（如 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]、动画和图形）的无缝集成。 托管组件还受益于 Windows Presentation Foundation (WPF) 映像编解码器扩展性模型, 该模型可在应用程序中[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]自动识别新图像格式。  
  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]托管<xref:System.Windows.Controls?displayProperty=nameWithType> API 的大部分位于<xref:System.Windows.Media?displayProperty=nameWithType> <xref:System.Windows.Media.ImageBrush> <xref:System.Windows.Media.Imaging?displayProperty=nameWithType>命名空间中, 但有几个重要类型 (如和<xref:System.Windows.Media.ImageDrawing> ) 驻留在命名空间中<xref:System.Windows.Controls.Image> , 并驻留在名称.  
  
 本主题提供有关托管组件的其他信息。 有关非托管 API 的详细信息, 请参阅[非托管 WPF 图像处理组件](/windows/desktop/wic/-wic-lh)文档。  
  
<a name="_imageformats"></a>   
## <a name="wpf-image-formats"></a>WPF 图像格式  
 编解码器用于对特定媒体格式进行解码或编码。 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]包含 BMP、JPEG、PNG、 [!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)]、 [!INCLUDE[TLA2#tla_wdp](../../../../includes/tla2sharptla-wdp-md.md)]、GIF 和图标图像格式的编解码器。 利用上述每个编解码器，应用程序可以对其各自的图像格式进行解码（ICON 除外）和编码。  
  
 <xref:System.Windows.Media.Imaging.BitmapSource>是用于对图像进行解码和编码的重要类。 它是 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 管道的基本构建基块，表示具有特定大小和分辨率的单个不变的像素集。 可以是多个框架图像的单个帧, 也可以是<xref:System.Windows.Media.Imaging.BitmapSource>在上执行的转换的结果。 <xref:System.Windows.Media.Imaging.BitmapSource> 它是在图像 (如) [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] <xref:System.Windows.Media.Imaging.BitmapFrame>中使用的很多主要类的父级。  
  
 <xref:System.Windows.Media.Imaging.BitmapFrame>用于存储图像格式的实际位图数据。 许多图像格式仅支持单个<xref:System.Windows.Media.Imaging.BitmapFrame>, 但[!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)] GIF 等格式支持每个图像多个帧。 帧由解码器用作输入数据，并传递到编码器以创建图像文件。  
  
 下面的示例演示如何<xref:System.Windows.Media.Imaging.BitmapFrame> <xref:System.Windows.Media.Imaging.BitmapSource>从创建[!INCLUDE[TLA2#tla_tiff](../../../../includes/tla2sharptla-tiff-md.md)] , 然后将添加到映像。  
  
 [!code-csharp[BitmapFrameExample#10](~/samples/snippets/csharp/VS_Snippets_Wpf/BitmapFrameExample/CSharp/BitmapFrame.cs#10)]
 [!code-vb[BitmapFrameExample#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitmapFrameExample/VB/BitmapFrame.vb#10)]  
  
### <a name="image-format-decoding"></a>图像格式解码  
 图像解码是指将某种图像格式转换为可以由系统使用的图像数据。 然后，此图像数据可以用于显示、处理或编码为其他格式。 根据图像格式选择解码器。 自动选择编解码器，除非指定了特定解码器。 [在 WPF 中显示图像](#_displayingimages)一节中的示例演示了自动解码。 使用非托管 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 界面开发并向系统注册的自定义格式解码器会自动加入到解码器选择队列。 这将使得自定义格式可以自动显示在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序中。  
  
 下面的示例演示如何使用位图解码器来解码 BMP 格式的图像。  
  
 [!code-cpp[BmpBitmapDecoderEncoder#5](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#5)]
 [!code-csharp[BmpBitmapDecoderEncoder#5](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#5)]
 [!code-vb[BmpBitmapDecoderEncoder#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#5)]  
  
### <a name="image-format-encoding"></a>图像格式编码  
 图像编码是指将图像数据转换为特定的图像格式。 然后，已编码的图像数据可以用于创建新的图像文件。 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 为上面介绍的每种图像格式提供编码器。  
  
 以下示例演示使用编码器保存一个新创建的位图图像。  
  
 [!code-cpp[BmpBitmapDecoderEncoder#3](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#3)]
 [!code-csharp[BmpBitmapDecoderEncoder#3](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#3)]
 [!code-vb[BmpBitmapDecoderEncoder#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#3)]  
  
<a name="_displayingimages"></a>   
## <a name="displaying-images-in-wpf"></a>在 WPF 中显示图像  
 可以通过多种方式在 Windows Presentation Foundation (WPF) 应用程序中显示图像。 图像可以使用<xref:System.Windows.Controls.Image>控件显示, 使用在视觉对象<xref:System.Windows.Media.ImageBrush>上绘制, 或使用<xref:System.Windows.Media.ImageDrawing>绘制。  
  
### <a name="using-the-image-control"></a>使用 Image 控件  
 <xref:System.Windows.Controls.Image>是框架元素, 是在应用程序中显示图像的主要方式。 在[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]中<xref:System.Windows.Controls.Image> , 可以通过两种方式使用: 属性语法或属性语法。 以下示例演示如何使用特性语法或属性标记语法来呈现宽度为 200 像素的图像。 有关特性语法和属性语法的详细信息，请参阅[依赖属性概述](../advanced/dependency-properties-overview.md)。  
  
 [!code-xaml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
 许多示例使用<xref:System.Windows.Media.Imaging.BitmapImage>对象来引用映像文件。 <xref:System.Windows.Media.Imaging.BitmapImage>是一种<xref:System.Windows.Media.Imaging.BitmapSource>专用化的, [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]它针对加载进行了优化, 并且是一种<xref:System.Windows.Controls.Image.Source%2A>将<xref:System.Windows.Controls.Image>图像显示为控件的简单方法。  
  
 以下示例演示如何使用代码呈现宽度为 200 像素的图像。  
  
> [!NOTE]
> <xref:System.Windows.Media.Imaging.BitmapImage><xref:System.ComponentModel.ISupportInitialize>实现接口, 以优化多个属性的初始化。 只能在对象初始化过程中进行属性更改。 调用<xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A>以发送初始化已开始的信号<xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A> , 并通知初始化已完成。 初始化后，将忽略所做的属性更改。  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
#### <a name="rotating-converting-and-cropping-images"></a>旋转、转换和剪切图像  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]允许用户使用<xref:System.Windows.Media.Imaging.BitmapImage>或的其他<xref:System.Windows.Media.Imaging.BitmapSource>对象 (如<xref:System.Windows.Media.Imaging.CroppedBitmap>或<xref:System.Windows.Media.Imaging.FormatConvertedBitmap>) 来转换图像。 上述图像转换可以缩放或旋转图像、更改图像的像素格式或剪切图像。  
  
 使用的<xref:System.Windows.Media.Imaging.BitmapImage.Rotation%2A> <xref:System.Windows.Media.Imaging.BitmapImage>属性执行图像旋转。 只能以 90 度为增量进行旋转。 在以下示例中，图像旋转了 90 度。  
  
 [!code-xaml[ImageElementExample#TransformedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml#transformedxaml2)]  
  
 [!code-csharp[ImageElementExample#TransformedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml.cs#transformedcsharp1)]
 [!code-vb[ImageElementExample#TransformedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/TransformedImageExample.xaml.vb#transformedcsharp1)]  
  
 将图像转换为其他像素格式 (如灰度) 使用<xref:System.Windows.Media.Imaging.FormatConvertedBitmap>完成。 在下面的示例中, 将图像转换为<xref:System.Windows.Media.PixelFormats.Gray4%2A>。  
  
 [!code-xaml[ImageElementExample_snip#ConvertedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml#convertedxaml2)]  
  
 [!code-csharp[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml.cs#convertedcsharp1)]
 [!code-vb[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/FormatConvertedExample.xaml.vb#convertedcsharp1)]  
  
 若要裁剪图像, 可以使用<xref:System.Windows.UIElement.Clip%2A> <xref:System.Windows.Controls.Image>或<xref:System.Windows.Media.Imaging.CroppedBitmap>的属性。 通常, 如果只想显示部分图像, <xref:System.Windows.UIElement.Clip%2A>则应使用。 如果需要编码并保存裁剪后的图像, 则<xref:System.Windows.Media.Imaging.CroppedBitmap>应使用。 在下面的示例中, 使用剪辑属性<xref:System.Windows.Media.EllipseGeometry>裁剪图像。  
  
 [!code-xaml[ImageElementExample_snip#CroppedXAMLUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml#croppedxamlusingclip1)]  
  
 [!code-csharp[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml.cs#croppedcsharpusingclip1)]
 [!code-vb[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/CroppedImageExample.xaml.vb#croppedcsharpusingclip1)]  
  
#### <a name="stretching-images"></a>拉伸图像  
 <xref:System.Windows.Controls.Image.Stretch%2A>属性控制如何拉伸图像以填充其容器。 <xref:System.Windows.Controls.Image.Stretch%2A>属性接受<xref:System.Windows.Media.Stretch>由枚举定义的下列值:  
  
- <xref:System.Windows.Media.Stretch.None>：不拉伸图像来填充输出区域。 如果图像比输出区域大，将图像绘制到输出区域，剪裁掉无法容纳的内容。  
  
- <xref:System.Windows.Media.Stretch.Fill>：缩放图像以适合输出区域。 由于图像的高度和宽度独立进行缩放，因此图像的原始纵横比可能不会保留。 也就是说，为了完全填充输出容器，图像可能会扭曲。  
  
- <xref:System.Windows.Media.Stretch.Uniform>：缩放图像, 使其完全适合输出区域。 图像的纵横比会保留。  
  
- <xref:System.Windows.Media.Stretch.UniformToFill>：缩放图像, 使其完全填充输出区域, 同时保留图像的原始纵横比。  
  
 下面的示例将每个可用<xref:System.Windows.Media.Stretch>枚举<xref:System.Windows.Controls.Image>应用于。  
  
 下图显示了该示例的输出, 并演示了应用于图像<xref:System.Windows.Controls.Image.Stretch%2A>时不同设置的影响。  
  
 ![Different TileBrush Stretch settings](./media/img-mmgraphics-stretchenum.jpg "img_mmgraphics_stretchenum")  
不同的拉伸设置  
  
 [!code-xaml[ImageElementExample_snip#ImageStretchExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageStretchExample.xaml#imagestretchexamplewholepage)]  
  
### <a name="painting-with-images"></a>使用图像进行绘制  
 通过使用绘制, <xref:System.Windows.Media.Brush>还可以在应用程序中显示图像。 借助画笔，可以利用任意内容（从简单的纯色到复杂的图案和图像集）绘制 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 对象。 若要使用图像进行绘制, <xref:System.Windows.Media.ImageBrush>请使用。 是将其内容定义<xref:System.Windows.Media.TileBrush>为位图图像的类型。 <xref:System.Windows.Media.ImageBrush> 显示单个图像, 由其<xref:System.Windows.Media.ImageBrush.ImageSource%2A>属性指定。 <xref:System.Windows.Media.ImageBrush> 可以控制图像的拉伸、对齐和平铺方式，从而防止失真并生成图案和其他效果。 下图显示了可使用<xref:System.Windows.Media.ImageBrush>实现的一些效果。  
  
 ![System.windows.media.imagebrush> 输出示例](./media/wcpsdk-mmgraphics-imagebrushexamples.gif "wcpsdk_mmgraphics_imagebrushexamples")  
图像画笔可以填充形状、控件、文本等  
  
 下面的示例演示如何使用<xref:System.Windows.Media.ImageBrush>图像绘制按钮的背景。  
  
 [!code-xaml[UsingImageBrush#4](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush/CS/PaintingWithImages.xaml#4)]  
  
 有关<xref:System.Windows.Media.ImageBrush>和绘制图像的其他信息, 请参阅[通过图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)。  
  
<a name="_metadata"></a>   
## <a name="image-metadata"></a>图像元数据  
 某些图像文件包含用于描述文件的内容或特征的元数据。 例如，大多数数数字相机创建的图像中包含用于捕获该图像的照相机品牌和型号的元数据。 每种图像格式处理元数据的方式不同，但 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 为存储和检索每种受支持图像格式的元数据提供了一种统一方式。  
  
 通过<xref:System.Windows.Media.Imaging.BitmapSource>对象的属性提供对元<xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A>数据的访问。 <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A>返回一个<xref:System.Windows.Media.Imaging.BitmapMetadata>对象, 该对象包含图像所包含的所有元数据。 此数据可以位于一个元数据架构中或位于不同架构的组合中。 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]支持以下图像元数据架构:可交换图像文件 (Exif)、文本 (PNG 文本数据)、图像文件目录 (IFD)、国际新闻通信委员会 (IPTC) 和[!INCLUDE[TLA#tla_xmp](../../../../includes/tlasharptla-xmp-md.md)]。  
  
 为了简化读取元数据<xref:System.Windows.Media.Imaging.BitmapMetadata>的过程, 提供了多个可以轻松访问的命名属性, <xref:System.Windows.Media.Imaging.BitmapMetadata.Author%2A>如、 <xref:System.Windows.Media.Imaging.BitmapMetadata.Title%2A>和<xref:System.Windows.Media.Imaging.BitmapMetadata.CameraModel%2A>。 许多命名属性还可以用于编写元数据。 元数据查询读取器提供对读取元数据的其他支持。 方法用于检索元数据查询读取器, 方法是提供一个字符串查询, 如 *"/app1/exif/"。* <xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> 在下面的示例中<xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> , 用于获取存储在 *"/Text/Description"* 位置中的文本。  
  
 [!code-cpp[BitmapMetadata#GetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#getquery)]
 [!code-csharp[BitmapMetadata#GetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#getquery)]
 [!code-vb[BitmapMetadata#GetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#getquery)]  
  
 若要编写元数据，请使用元数据查询编写器。 <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A>获取查询编写器并设置所需的值。 在下面的示例中<xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> , 用于写入 *"/Text/Description"* 位置中存储的文本。  
  
 [!code-cpp[BitmapMetadata#SetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#setquery)]
 [!code-csharp[BitmapMetadata#SetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#setquery)]
 [!code-vb[BitmapMetadata#SetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#setquery)]  
  
<a name="_extensibility"></a>   
## <a name="codec-extensibility"></a>编解码器扩展性  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] 的核心功能是用于新图像编解码器的扩展性模型。 通过这些非托管的接口，编解码器开发人员可以将编解码器与 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 集成，这样 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序就可以自动使用新的图像格式。  
  
 有关扩展性 API 的示例, 请参阅[Win32 示例编解码器](https://go.microsoft.com/fwlink/?LinkID=160052)。 此示例演示如何为自定义图像格式创建解码器和编码器。  
  
> [!NOTE]
> 编解码器必须进行数字签名，系统才能够识别它。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Media.Imaging.BitmapSource>
- <xref:System.Windows.Media.Imaging.BitmapImage>
- <xref:System.Windows.Controls.Image>
- <xref:System.Windows.Media.Imaging.BitmapMetadata>
- [2D 图形和图像处理](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [Win32 示例编解码器](https://go.microsoft.com/fwlink/?LinkID=160052)
