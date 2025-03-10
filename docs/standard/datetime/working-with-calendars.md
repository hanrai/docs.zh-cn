---
title: 使用日历
ms.date: 04/01/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- globalization [.NET], calendars
- calendars, global applications
- global applications, calendars
- world-ready applications, calendars
- international applications [.NET], calendars
- culture, calendars
ms.assetid: 0c1534e5-979b-4c8a-a588-1c24301aefb3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e92d5564308d31609b9fb024f3d3368a19b76b1d
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106703"
---
# <a name="working-with-calendars"></a>使用日历

尽管日期和时间值表示时间中的某一刻，但其字符串表示形式区分区域性，并取决于特定区域性显示日期和时间值所用的约定以及该区域性使用的日历。 本主题探讨了对 .NET 中的日历的支持, 并讨论了使用日期值时的 calendar 类的使用。

## <a name="calendars-in-net"></a>.NET 中的日历

.Net 中的所有日历均派生<xref:System.Globalization.Calendar?displayProperty=nameWithType>自类, 该类提供基本日历实现。 从 <xref:System.Globalization.Calendar> 类继承的类之一是 <xref:System.Globalization.EastAsianLunisolarCalendar> 类，该类是所有阴阳历的基类。 .NET 包括以下日历实现:

- <xref:System.Globalization.ChineseLunisolarCalendar>，表示中国阴阳历。

- <xref:System.Globalization.GregorianCalendar>，表示公历。 此日历进一步细分为 <xref:System.Globalization.GregorianCalendarTypes?displayProperty=nameWithType> 枚举定义的子类型（如阿拉伯和中东法国）。 <xref:System.Globalization.GregorianCalendar.CalendarType%2A?displayProperty=nameWithType> 属性指定公历的子类型。

- <xref:System.Globalization.HebrewCalendar>，表示希伯来历。

- <xref:System.Globalization.HijriCalendar>，表示回历。

- <xref:System.Globalization.JapaneseCalendar>，表示日本历。

- <xref:System.Globalization.JapaneseLunisolarCalendar>，表示日本阴阳历。

- <xref:System.Globalization.JulianCalendar>，表示罗马儒略历。

- <xref:System.Globalization.KoreanCalendar>，表示朝鲜历。

- <xref:System.Globalization.KoreanLunisolarCalendar>，表示朝鲜阴阳历。

- <xref:System.Globalization.PersianCalendar>，表示波斯历。

- <xref:System.Globalization.TaiwanCalendar>，表示台湾历。

- <xref:System.Globalization.TaiwanLunisolarCalendar>，表示台湾阴阳历。

- <xref:System.Globalization.ThaiBuddhistCalendar>，表示泰国佛历。

- <xref:System.Globalization.UmAlQuraCalendar>，表示古兰经历。

可通过以下两种方法之一来使用日历：

- 作为特定区域性使用的日历。 每个 <xref:System.Globalization.CultureInfo> 对象都有当前日历，这是该对象当前使用的日历。 所有日期和时间值的字符串表示形式会自动反映当前的区域性及其当前日历。 通常，当前的日历是该区域性的默认日历。 <xref:System.Globalization.CultureInfo>对象还具有可选日历, 其中包含区域性可使用的其他日历。

- 作为与特定区域性无关的独立日历。 在这种情况下，<xref:System.Globalization.Calendar> 方法用于将日期表示为反映日历的值。

请注意，以下六个日历类只能用作独立日历：<xref:System.Globalization.ChineseLunisolarCalendar>、<xref:System.Globalization.JapaneseLunisolarCalendar>、<xref:System.Globalization.JulianCalendar>、<xref:System.Globalization.KoreanLunisolarCalendar>、<xref:System.Globalization.PersianCalendar> 和 <xref:System.Globalization.TaiwanLunisolarCalendar>。 任何区域性都不将这些日历用作默认日历或可选日历。

## <a name="calendars-and-cultures"></a>日历和区域性

每个区域性都有默认日历，由 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType> 属性定义。 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 属性可返回 <xref:System.Globalization.Calendar> 对象的数组，该数组指定特定区域性支持的所有日历，包括该区域性的默认日历。

下面的示例演示 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType> 和 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 属性。 该示例为泰语（泰国）和日语（日本）区域性创建 `CultureInfo` 对象，并显示它们的默认和可选日历。 请注意，在这两种情况下，区域性的默认日历也包括在 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 集合中。

[!code-csharp[Conceptual.Calendars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/calendarinfo1.cs#1)]
[!code-vb[Conceptual.Calendars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/calendarinfo1.vb#1)]

特定 <xref:System.Globalization.CultureInfo> 对象当前正在使用的日历由区域性的 <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=nameWithType> 属性定义。 区域性的 <xref:System.Globalization.DateTimeFormatInfo> 对象由 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType> 属性返回。 创建区域性时，其默认值与 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType> 属性的值相同。 但是，可将区域性的当前日历更改为 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 属性返回的数组中包含的任何日历。 如果尝试将当前日历设置为 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> 属性值中不包括的日历，则会引发 <xref:System.ArgumentException>。

以下示例将更改阿拉伯（沙特阿拉伯）区域性使用的日历。 它首先实例化一个 <xref:System.DateTime> 值并使用当前区域性（在此示例中，为英语（美国））和当前区域性的日历（在此示例中，为公历）显示该值。 接下来，该示例将当前区域性更改为阿拉伯语（沙特阿拉伯），并使用其默认的古兰经历显示该日期。 然后，该示例调用 `CalendarExists` 方法来确定阿拉伯语（沙特阿拉伯）区域性是否支持该回历。 因为该日历受支持，所以该示例将当前日历更改为回历并再次显示日期。 请注意，在每种情况下，均使用当前区域性的当前日历来显示日期。

[!code-csharp[Conceptual.Calendars#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/changecalendar2.cs#2)]
[!code-vb[Conceptual.Calendars#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/changecalendar2.vb#2)]

## <a name="dates-and-calendars"></a>日期和日历

除包括 <xref:System.Globalization.Calendar> 类型参数并允许日期的元素（即月、日和年）以指定日历反映值的构造函数外，<xref:System.DateTime> 和 <xref:System.DateTimeOffset> 值始终基于公历。 例如，这意味着 <xref:System.DateTime.Year%2A?displayProperty=nameWithType> 属性返回公历的年，<xref:System.DateTime.Day%2A?displayProperty=nameWithType> 属性返回公历的当月日期。

> [!IMPORTANT]
> 请记住，日期值与其字符串表示形式之间是有差异的，这一点很重要。 前者基于公历，后者基于特定区域性的当前日历。

下面的示例演示了 <xref:System.DateTime> 属性与其对应的 <xref:System.Globalization.Calendar> 方法之间的这一差异。 在此示例中，当前区域性为阿拉伯语（埃及），当前日历为古兰经历。 <xref:System.DateTime> 值设置为 2011 年 7 月 15 日。 很显然，该值被解释为公历日期，因为这些相同的值是由 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 方法在使用不变区域性的约定时返回的。 使用当前区域性的约定设置格式后，该日期的字符串表示形式为 14/08/32，与古兰经历中的日期等效。 接下来，使用 `DateTime` 和 `Calendar` 的成员返回 <xref:System.DateTime> 值的日、月和年。 在每种情况下，<xref:System.DateTime> 成员返回的值反映公历中的值，而 <xref:System.Globalization.UmAlQuraCalendar> 成员返回的值反映古兰经历中的值。

[!code-csharp[Conceptual.Calendars#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/datesandcalendars2.cs#3)]
[!code-vb[Conceptual.Calendars#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/datesandcalendars2.vb#3)]

### <a name="instantiating-dates-based-on-a-calendar"></a>基于日历实例化日期

由于 <xref:System.DateTime> 和 <xref:System.DateTimeOffset> 值基于公历，因此如果要使用不同日历中的日、月或年的值，必须调用包括 <xref:System.Globalization.Calendar> 类型参数的重载构造函数来实例化日期值。 还可以调用特定日历的 <xref:System.Globalization.Calendar.ToDateTime%2A?displayProperty=nameWithType> 方法的重载之一，以基于特定日历的值来实例化 <xref:System.DateTime> 对象。

下面的示例通过向 <xref:System.DateTime> 构造函数传递一个 <xref:System.Globalization.HebrewCalendar> 对象来实例化一个 <xref:System.DateTime> 值，通过调用 <xref:System.DateTime> 方法来实例化另一个 <xref:System.Globalization.HebrewCalendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType> 值。 由于这两个值是使用希伯来历中的相同值创建的，因此对 <xref:System.DateTime.Equals%2A?displayProperty=nameWithType> 方法的调用显示这两个 <xref:System.DateTime> 值相等。

[!code-csharp[Conceptual.Calendars#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatehcdate1.cs#4)]
[!code-vb[Conceptual.Calendars#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatehcdate1.vb#4)]

### <a name="representing-dates-in-the-current-calendar"></a>表示当前日历中的日期

在将日期转换为字符串时，日期和时间格式设置方法始终使用当前日历。 这意味着，年、月和当月日期的字符串表示形式反映当前日历，不一定反映公历。

下面的示例演示当前日历如何影响日期的字符串表示形式。 该示例将当前区域性更改为中文（繁体，台湾），并实例化日期值。 然后，该示例显示当前日历和日期，将当前日历更改为 <xref:System.Globalization.TaiwanCalendar>，并再次显示当前日历和日期。 初次显示日期时，它表示为公历日期。 第二次显示日期时，它表示为台湾日历中的日期。

[!code-csharp[Conceptual.Calendars#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/currentcalendar1.cs#5)]
[!code-vb[Conceptual.Calendars#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/currentcalendar1.vb#5)]

### <a name="representing-dates-in-a-non-current-calendar"></a>表示非当前日历中的日期

若要使用特定区域性的当前日历之外的日历表示日期，必须调用该 <xref:System.Globalization.Calendar> 对象的方法。 例如，<xref:System.Globalization.Calendar.GetYear%2A?displayProperty=nameWithType>、<xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=nameWithType> 和 <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=nameWithType> 方法可将年、月和日转换为反映特定日历的值。

> [!WARNING]
> 由于某些日历不是任何区域性的可选日历，因此用这些日历表示日期始终需要调用日历方法。 对于派生自 <xref:System.Globalization.EastAsianLunisolarCalendar>、<xref:System.Globalization.JulianCalendar> 和 <xref:System.Globalization.PersianCalendar> 类的所有日历而言，均为这种情况。

下面的示例使用 <xref:System.Globalization.JulianCalendar> 对象实例化罗马儒略历的日期 1905 年 1 月 9 日。 使用默认（公历）日历显示此日期时，该日期表示为 1905 年 1 月 22 日。 通过调用各种 <xref:System.Globalization.JulianCalendar> 方法，可用罗马儒略历表示日期。

[!code-csharp[Conceptual.Calendars#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/noncurrentcalendar1.cs#6)]
[!code-vb[Conceptual.Calendars#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/noncurrentcalendar1.vb#6)]

### <a name="calendars-and-date-ranges"></a>日历和日期范围

日历支持的最早日期由其 <xref:System.Globalization.Calendar.MinSupportedDateTime%2A?displayProperty=nameWithType> 属性指示。 对于 <xref:System.Globalization.GregorianCalendar> 类，该日期为公历公元 0001 年 1 月 1 日。 .NET 中的大多数其他日历都支持更晚的日期。 尝试使用日历支持的最早日期前面的日期和时间值将引发 <xref:System.ArgumentOutOfRangeException> 异常。

但是，有一个很重要的异常。 <xref:System.DateTime> 对象和 <xref:System.DateTimeOffset> 对象的默认（未初始化的）值等于 <xref:System.Globalization.GregorianCalendar.MinSupportedDateTime%2A?displayProperty=nameWithType> 值。 如果你尝试在不支持0001年1月1日的日历中设置此日期的格式 并且不提供格式说明符, 格式设置方法使用 "s" (可排序日期/时间模式) 格式说明符, 而不是 "G" (常规日期/时间模式) 格式说明符。 因此，格式设置操作将不会引发 <xref:System.ArgumentOutOfRangeException> 异常。 相反，它会返回不受支持的日期。 下面的示例阐释了这一点，在使用日语日历将当前区域性设置为日语（日本）以及使用古兰经历将当前区域性设置为阿拉伯语（埃及）时，它将显示 <xref:System.DateTime.MinValue?displayProperty=nameWithType> 的值。 它还会将当前区域性设置为英语（美国），并调用 <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=nameWithType> 方法以及所有这些 <xref:System.Globalization.CultureInfo> 对象。 在每种情况下，均使用可排序的日期/时间模式来显示日期。

[!code-csharp[Conceptual.Calendars#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/minsupporteddatetime1.cs#11)]
[!code-vb[Conceptual.Calendars#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/minsupporteddatetime1.vb#11)]

## <a name="working-with-eras"></a>使用纪元

日历通常将日期划分为纪元。 但是, .net <xref:System.Globalization.Calendar>中的类不支持日历定义的每个纪元, 并且大多数<xref:System.Globalization.Calendar>类只支持单个纪元。 只有 <xref:System.Globalization.JapaneseCalendar> 和 <xref:System.Globalization.JapaneseLunisolarCalendar> 类支持多个纪元。

> [!IMPORTANT]
> Reiwa 时代, <xref:System.Globalization.JapaneseCalendar>和<xref:System.Globalization.JapaneseLunisolarCalendar>中的新纪元于5月1日 (2019) 开始。 此更改会影响使用这些日历的所有应用程序。 有关详细信息, 请参阅以下文章:
> - 在[.net 的日式日历中处理新时代](https://devblogs.microsoft.com/dotnet/handling-a-new-era-in-the-japanese-calendar-in-net/), 这会将添加到 .net 的功能记录为支持包含多个纪元的日历, 并讨论在处理多个纪元日历时要使用的最佳方案。
> - [准备应用程序以进行日本时代更改](/windows/uwp/design/globalizing/japanese-era-change), 这提供了有关在 Windows 上测试应用程序以确保其对时代的准备情况发生变化的信息。
> - [.NET Framework 的新日语时代更新的摘要](https://support.microsoft.com/help/4477957/new-japanese-era-updates-for-net-framework), 其中列出了与新日语日历时代相关的单独 Windows 版本 .NET Framework 更新, 为多个时代支持提供新 .NET Framework 功能的说明, 并包括在测试应用程序中查找。

大多数日历中的纪元表示非常长的时间段。 例如, 在公历中, 当前纪元跨越两个以上的 millennia。 <xref:System.Globalization.JapaneseCalendar> 对于<xref:System.Globalization.JapaneseLunisolarCalendar>和, 两个支持多个纪元的日历不是这样。 纪元对应于高层的 reign 的时间段。 支持多个纪元, 特别是当前纪元的上限未知时, 会带来特殊的挑战。

### <a name="eras-and-era-names"></a>纪元和纪元名称

在 .net 中, 表示特定日历实现支持的纪元的整数以相反顺序<xref:System.Globalization.Calendar.Eras%2A?displayProperty=nameWithType>存储在数组中。 当前纪元 (即具有最新时间范围的纪元) 位于索引零处, 对于<xref:System.Globalization.Calendar>支持多个纪元的类, 每个连续索引将反映以前的纪元。 静态的 <xref:System.Globalization.Calendar.CurrentEra?displayProperty=nameWithType> 属性定义当前纪元在 <xref:System.Globalization.Calendar.Eras%2A?displayProperty=nameWithType> 数组中的索引；它是一个值始终为零的常数。 各个 <xref:System.Globalization.Calendar> 类还包括可返回当前纪元值的静态字段。 下表中列出了这些字段。

| 日历类                                        | 当前纪元字段                                                 |
| ----------------------------------------------------- | ----------------------------------------------------------------- |
| <xref:System.Globalization.ChineseLunisolarCalendar>  | <xref:System.Globalization.ChineseLunisolarCalendar.ChineseEra>   |
| <xref:System.Globalization.GregorianCalendar>         | <xref:System.Globalization.GregorianCalendar.ADEra>               |
| <xref:System.Globalization.HebrewCalendar>            | <xref:System.Globalization.HebrewCalendar.HebrewEra>              |
| <xref:System.Globalization.HijriCalendar>             | <xref:System.Globalization.HijriCalendar.HijriEra>                |
| <xref:System.Globalization.JapaneseLunisolarCalendar> | <xref:System.Globalization.JapaneseLunisolarCalendar.JapaneseEra> |
| <xref:System.Globalization.JulianCalendar>            | <xref:System.Globalization.JulianCalendar.JulianEra>              |
| <xref:System.Globalization.KoreanCalendar>            | <xref:System.Globalization.KoreanCalendar.KoreanEra>              |
| <xref:System.Globalization.KoreanLunisolarCalendar>   | <xref:System.Globalization.KoreanLunisolarCalendar.GregorianEra>  |
| <xref:System.Globalization.PersianCalendar>           | <xref:System.Globalization.PersianCalendar.PersianEra>            |
| <xref:System.Globalization.ThaiBuddhistCalendar>      | <xref:System.Globalization.ThaiBuddhistCalendar.ThaiBuddhistEra>  |
| <xref:System.Globalization.UmAlQuraCalendar>          | <xref:System.Globalization.UmAlQuraCalendar.UmAlQuraEra>          |

通过将特定纪元编号传递给 <xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=nameWithType> 或 <xref:System.Globalization.DateTimeFormatInfo.GetAbbreviatedEraName%2A?displayProperty=nameWithType> 方法，可检索与该纪元编号对应的名称。 下面的示例调用这些方法来检索有关 <xref:System.Globalization.GregorianCalendar> 类中的纪元支持信息。 它显示与当前纪元的第二年1月1日相对应的公历日期, 以及与每个受支持的日文日历时代的第二年1月1日相对应的公历日期。

[!code-csharp[Conceptual.Calendars#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatewithera1.cs)]
[!code-vb[Conceptual.Calendars#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatewithera1.vb)]

此外，“g”自定义日期和时间格式字符串还包括一个日期和时间的字符串表示形式的日期纪元名称。 有关详细信息, 请参阅[自定义日期和时间格式字符串](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)。

### <a name="instantiating-a-date-with-an-era"></a>使用纪元实例化日期

对于支持多<xref:System.Globalization.Calendar>个纪元的两个类, 由特定年份、月份和月份值组成的日期可能是不明确的。 例如, 支持的所有纪元的<xref:System.Globalization.JapaneseCalendar>年份数为1。 通常，如果未指定纪元，则日期和时间以及日历方法都假定该值属于当前纪元。 这适用于包含<xref:System.Globalization.Calendar>类型参数的<xref:System.DateTime.%23ctor%2A> 和<xref:System.DateTimeOffset.%23ctor%2A>构造函数, 以及 [JapaneseCalendar.ToDateTime](xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)) 和 [JapaneseLunisolarCalendar.ToDateTime](xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)) 方法。 下面的示例实例化表示未指定纪元的第二年1月1日的日期。 如果在 Reiwa 纪元为当前纪元时执行该示例, 则该日期将被解释为 Reiwa 纪元的第二年。 纪元令和在由<xref:System.DateTime.ToString(System.String,System.IFormatProvider)?displayProperty=nameWithType>方法返回的字符串中的年份之前, 并对应于公历的2020年1月1日。 (Reiwa 时代从公历的2019年开始。)

[!code-csharp[A date in the current era](~/samples/snippets/standard/datetime/calendars/current-era/cs/program.cs)]
[!code-vb[A date in the current era](~/samples/snippets/standard/datetime/calendars/current-era/vb/program.vb)]

但是, 如果纪元发生更改, 则此代码的目的不明确。 表示当前纪元的第二年的日期, 或它是否用于表示 Heisei 时代的第二年？ 可以通过两种方法来避免这种歧义:

- 使用默认<xref:System.Globalization.GregorianCalendar>类实例化日期和时间值。 然后, 可以使用日语日历或日语阴阳历来表示日期的字符串表示形式, 如下面的示例所示。

  [!code-csharp[Insantiating a Gregorian date](~/samples/snippets/standard/datetime/calendars/gregorian/cs/program.cs)]
  [!code-vb[Instantiating a Gregorian date](~/samples/snippets/standard/datetime/calendars/gregorian/vb/program.vb)]

- 调用显式指定纪元的日期和时间方法。 这包括以下方法:

  - <xref:System.Globalization.JapaneseCalendar> <xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)>或类<xref:System.Globalization.JapaneseLunisolarCalendar>的方法。

  - <xref:System.DateTime>或分析<xref:System.DateTimeOffset>方法(如<xref:System.DateTime.TryParse%2A> <xref:System.Globalization.DateTimeStyles> 、、或)<xref:System.DateTime.TryParseExact%2A>, 其中包括要分析的字符串和可选的参数 (如果当前区域性为日语-日本 (" <xref:System.DateTime.ParseExact%2A> <xref:System.DateTime.Parse%2A>ja-jp "), 并且该区域性的日历是<xref:System.Globalization.JapaneseCalendar>。 要分析的字符串必须包括纪元。

  - 一个<xref:System.DateTime>或<xref:System.DateTimeOffset> 分析方法<xref:System.IFormatProvider>, 其中包含类型的参数。`provider` `provider`<xref:System.Globalization.CultureInfo>必须是一个对象, 该对象表示其当前日历为<xref:System.Globalization.DateTimeFormatInfo> <xref:System.Globalization.JapaneseCalendar>的或其<xref:System.Globalization.DateTimeFormatInfo.Calendar>属性为<xref:System.Globalization.JapaneseCalendar>的对象。 要分析的字符串必须包括纪元。

  下面的示例使用三种方法来实例化 Meiji 纪元中的日期和时间, 该日期和时间从1868年9月8日开始, 结束于1912年7月29日结束。

  [!code-csharp[A date in a specified era](~/samples/snippets/standard/datetime/calendars/specify-era/cs/program.cs)]
  [!code-vb[A date in a specified era](~/samples/snippets/standard/datetime/calendars/specify-era/vb/program.vb)]

> [!TIP]
> 处理支持多个纪元的日历时,*始终*使用公历日期来实例化日期, 或者在基于该日历实例化日期和时间时指定纪元。

在为<xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)>方法指定纪元时, 提供日历的<xref:System.Globalization.Calendar.Eras>属性中的纪元索引。 但对于其纪元可能会发生更改的日历, 这些索引不是常量值;当前纪元位于索引 0, 最早的纪元位于索引`Eras.Length - 1`处。 将新纪元添加到日历时, 先前纪元的索引将增加1。 可以提供相应的纪元索引, 如下所示:

- 对于当前纪元中的日期, 请始终使用日历的<xref:System.Globalization.Calendar.CurrentEra>属性。

- 对于指定纪元中的日期, 请使用<xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=nameWithType>方法检索对应于指定纪元名称的索引。 这要求<xref:System.Globalization.JapaneseCalendar>是表示 ja-jp 区域性的<xref:System.Globalization.CultureInfo>对象的当前日历。  (此方法也适用<xref:System.Globalization.JapaneseLunisolarCalendar>于, 因为它支持与相同的纪元<xref:System.Globalization.JapaneseCalendar>。)前面的示例演示了这种方法。

### <a name="calendars-eras-and-date-ranges-relaxed-range-checks"></a>日历、纪元和日期范围:宽松范围检查

与单个日历非常类似, 它们具有受支持的日期范围<xref:System.Globalization.JapaneseCalendar> , <xref:System.Globalization.JapaneseLunisolarCalendar>和类中的纪元也具有受支持的范围。 以前, .NET 使用了严格的纪元范围检查, 以确保特定于纪元的日期在纪元的范围内。 也就是说, 如果日期在指定纪元的范围之外, 则该方法将引发<xref:System.ArgumentOutOfRangeException>。 目前, 默认情况下, .NET 使用宽松范围检查。 所有版本的 .NET 的更新引入了宽松纪元范围检查;尝试将位于指定纪元范围之外的特定于纪元的日期实例化到以下纪元, 并且不会引发异常。

下面的示例尝试在 Showa 纪元的65th 年中实例化日期, 该日期从1926年12月25日开始, 到1989年1月7日结束。 此日期对应于1990年1月9日, 超过了 Showa 时代<xref:System.Globalization.JapaneseCalendar>的范围。 如示例中的输出所示, 该示例显示的日期为1990年1月9日, 在 Heisei 时代的第二年。

  [!code-csharp[Relaxed range checks](~/samples/snippets/standard/datetime/calendars/relaxed-range/cs/program.cs)]
  [!code-vb[Relaxed range checks](~/samples/snippets/standard/datetime/calendars/relaxed-range/vb/program.vb)]

如果不需要宽松范围检查, 则可以通过多种方式还原严格范围检查, 具体取决于运行应用程序的 .NET 版本:

- **.NET Core:** 可以将以下内容添加到*netcore*配置文件:

  ```json
  "runtimeOptions": {
    "configProperties": {
        "Switch.System.Globalization.EnforceJapaneseEraYearRanges": true
    }
  }
  ```

- **.NET Framework 4.6 或更高版本:** 可以设置以下 AppContext 开关:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.EnforceJapaneseEraYearRanges=true" />
    </runtime>
  </configuration>
  ```

- **.NET Framework 4.5.2 或更早版本:** 可以设置以下注册表值:

   |  |  |
   |--|--|
   |Key | HKEY_LOCAL_MACHINE\Software\Microsoft\.NETFramework\AppContext |
   |name | Switch.System.Globalization.EnforceJapaneseEraYearRanges |
   |类型 | REG_SZ |
   |值 | true |

启用严格范围检查后, 上面的示例将引发<xref:System.ArgumentOutOfRangeException> , 并显示以下输出:

```console
Unhandled Exception: System.ArgumentOutOfRangeException: Valid values are between 1 and 64, inclusive.
Parameter name: year
   at System.Globalization.GregorianCalendarHelper.GetYearOffset(Int32 year, Int32 era, Boolean throwOnError)
   at System.Globalization.GregorianCalendarHelper.ToDateTime(Int32 year, Int32 month, Int32 day, Int32 hour, Int32 minute, Int32 second, Int32 millisecond, Int32 era)
   at Example.Main()
```

### <a name="representing-dates-in-calendars-with-multiple-eras"></a>用多个纪元表示日历中的日期

如果 <xref:System.Globalization.Calendar> 对象支持纪元并且是 <xref:System.Globalization.CultureInfo> 对象的当前日历，则纪元将包括在完整日期和时间、长日期和短日期模式的日期和时间值的字符串表示形式中。 下面的示例显示当前区域性为日语（日本）并且当前日历为日本日历时的这些日期模式。

[!code-csharp[Conceptual.Calendars#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings1.cs#8)]
[!code-vb[Conceptual.Calendars#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings1.vb#8)]

> [!WARNING]
> 类是 .net 中唯一支持多个纪元中的日期并且可以是<xref:System.Globalization.CultureInfo>对象的当前日历 (具体而言, 是表示日语 (日本) 区域性的<xref:System.Globalization.CultureInfo>对象) 的 calendar 类。 <xref:System.Globalization.JapaneseCalendar>

对于所有日历，“g”自定义格式说明符会在结果字符串中包括纪元。 下面的示例使用“MM-dd-yyyy g”自定义格式字符串，在当前日历为公历时在结果字符串中包括纪元。

[!code-csharp[Conceptual.Calendars#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings2.cs#9)]
[!code-vb[Conceptual.Calendars#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings2.vb#9)]

当日期的字符串表示形式用非当前日历来表示时，<xref:System.Globalization.Calendar> 类包括一个可与 <xref:System.Globalization.Calendar.GetEra%2A?displayProperty=nameWithType>、<xref:System.Globalization.Calendar.GetYear%2A?displayProperty=nameWithType> 和 <xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=nameWithType> 方法一起使用的 <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=nameWithType> 方法，以明确指示日期及其所属纪元。 下面的示例使用 <xref:System.Globalization.JapaneseLunisolarCalendar> 类来提供演示。 但请注意，在结果字符串中包括有意义的名称或缩写（而不是表示纪元的整数）需要您实例化 <xref:System.Globalization.DateTimeFormatInfo> 对象并使 <xref:System.Globalization.JapaneseCalendar> 成为其当前日历。 （<xref:System.Globalization.JapaneseLunisolarCalendar> 日历不能为任何区域性的当前日历，但在此示例中，两个日历共享相同的纪元。）

[!code-csharp[Conceptual.Calendars#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings3.cs#10)]
[!code-vb[Conceptual.Calendars#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings3.vb#10)]

在日本日历中, 年代的第一年称为 Gannen (元年)。 例如, Heisei 时代的第一年不是 Heisei 1, 而是 Heisei Gannen。 当使用以下标准或自定义日期和时间格式字符串与<xref:System.Globalization.CultureInfo>表示日语-日本 ("ja-jp") 区域性的对象使用时,.net采用这种格式设置操作的格式<xref:System.Globalization.JapaneseCalendar>类:

- [长日期模式](../base-types/standard-date-and-time-format-strings.md#LongDate), 由 "D" 标准日期和时间格式字符串指示。
- "F" 标准日期和时间格式字符串指示[的完整日期长时间模式](../base-types/standard-date-and-time-format-strings.md#FullDateLongTime)。
- "F" 标准日期和时间格式字符串指示[的完整日期短时间模式](../base-types/standard-date-and-time-format-strings.md#FullDateShortTime)。
- [年份/月份模式](../base-types/standard-date-and-time-format-strings.md#YearMonth), 由 Y "或" y "标准日期和时间格式字符串指示。
- ["Ggy" 年 "" 或 "ggy年"[自定义日期和时间格式字符串](../base-types/custom-date-and-time-format-strings.md)。

例如, 下面的示例在的 Heisei 时代<xref:System.Globalization.JapaneseCalendar>的第一年显示日期。

  [!code-csharp[gannen](~/samples/snippets/standard/datetime/calendars/gannen/cs/program.cs)]
  [!code-vb[gannen](~/samples/snippets/standard/datetime/calendars/gannen/vb/gannen-fmt.vb)]

如果在格式设置操作中不需要此行为, 则可以通过执行下列操作来还原以前的行为, 该行为始终将纪元的第一年表示为 "1", 而不是 "Gannen", 具体取决于 .NET 的版本:

- **.NET Core:** 可以将以下内容添加到*netcore*配置文件:

  ```json
  "runtimeOptions": {
    "configProperties": {
        "Switch.System.Globalization.FormatJapaneseFirstYearAsANumber": true
    }
  }
  ```

- **.NET Framework 4.6 或更高版本:** 可以设置以下 AppContext 开关:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.FormatJapaneseFirstYearAsANumber=true" />
    </runtime>
  </configuration>
  ```

- **.NET Framework 4.5.2 或更早版本:** 可以设置以下注册表值:

   |  |  |
   |--|--|
   |Key | HKEY_LOCAL_MACHINE\Software\Microsoft\.NETFramework\AppContext |
   |名称 | Switch.System.Globalization.FormatJapaneseFirstYearAsANumber |
   |类型 | REG_SZ |
   |值 | true |

如果禁用格式设置操作中的 gannen 支持, 上一个示例将显示以下输出:

```console
Japanese calendar date: 平成1年8月18日 (Gregorian: Friday, August 18, 1989)
```

.NET 还进行了更新, 以便日期和时间分析操作支持包含 "1" 或 Gannen 表示的年份的字符串。 尽管不需要执行此操作, 但可以还原以前的行为, 以便仅将 "1" 识别为纪元的第一年。 可以按以下方式执行此操作, 具体取决于 .NET 的版本:

- **.NET Core:** 可以将以下内容添加到*netcore*配置文件:

  ```json
  "runtimeOptions": {
    "configProperties": {
        "Switch.System.Globalization.EnforceLegacyJapaneseDateParsing": true
    }
  }
  ```

- **.NET Framework 4.6 或更高版本:** 可以设置以下 AppContext 开关:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.EnforceLegacyJapaneseDateParsing=true" />
    </runtime>
  </configuration>
  ```

- **.NET Framework 4.5.2 或更早版本:** 可以设置以下注册表值:

   |  |  |
   |--|--|  
   |Key | HKEY_LOCAL_MACHINE\Software\Microsoft\.NETFramework\AppContext |
   |name | Switch.System.Globalization.EnforceLegacyJapaneseDateParsing |
   |类型 | REG_SZ |
   |值 | true | 

## <a name="see-also"></a>请参阅

- [如何：以非公历日历显示日期](../../../docs/standard/base-types/how-to-display-dates-in-non-gregorian-calendars.md)
- [示例：日历周范围实用工具](https://code.msdn.microsoft.com/NET-Framework-4-Calendar-3360a84a)
- [Calendar 类](xref:System.Globalization.Calendar)
