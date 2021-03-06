---
title: 如何： 实例化 TimeZoneInfo 对象
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- instantiating time zone objects
- time zone objects [.NET Framework], instantiation
ms.assetid: 8cb620e5-c6a6-4267-a52e-beeb73cd1a34
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e15e7f8968d7edf87ae3cd709d8fb26a2f49826a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-instantiate-a-timezoneinfo-object"></a>如何： 实例化 TimeZoneInfo 对象

实例化 <xref:System.TimeZoneInfo> 对象的常用方法是从注册表中检索与其有关的信息。 本主题讨论如何从本地系统注册表中实例化 <xref:System.TimeZoneInfo> 对象。

### <a name="to-instantiate-a-timezoneinfo-object"></a>实例化 TimeZoneInfo 对象

1. 声明 <xref:System.TimeZoneInfo> 对象。

2. 调用`static`(`Shared`在 Visual Basic 中)<xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A?displayProperty=nameWithType>方法。

3. 处理方法引发的所有异常，尤其是注册表中未定义时区时引发的 <xref:System.TimeZoneNotFoundException> 。

## <a name="example"></a>示例

下面的代码会检索表示东部标准时区并显示本地时间所对应的东部标准时间的 <xref:System.TimeZoneInfo> 对象。

[!code-csharp[System.TimeZone2.Concepts#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#5)]
[!code-vb[System.TimeZone2.Concepts#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#5)]

<xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A?displayProperty=nameWithType>方法的单个参数是时区的标识符，你想要检索，对应于对象的<xref:System.TimeZoneInfo.Id%2A?displayProperty=nameWithType>属性。 时区标识符是唯一标识时区的键字段。 虽然大多数键都相对较短，但时区标识符相对较长。 在大多数情况下，其值对应于 <xref:System.TimeZoneInfo.StandardName%2A> 对象的 <xref:System.TimeZoneInfo> 属性，该属性用于提供时区标准时间的名称。 但是，有例外情况。 确保提供有效标识符的最好方法是枚举系统上可用的时区，然后记下上面显示的时区标识符。 有关说明，请参阅 [如何：枚举计算机上存在的时区](../../../docs/standard/datetime/enumerate-time-zones.md)。 [查找本地系统上定义的时区](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)主题还包含了一个所选时区标识符列表。

如果找到时区，该方法将返回其 <xref:System.TimeZoneInfo> 对象。 如果未找到时区，该方法将引发 <xref:System.TimeZoneNotFoundException>。 如果找到该时区但其数据已损坏或不完整，该方法将引发 <xref:System.InvalidTimeZoneException>。

如果你的应用程序依赖于一个必须存在的时区，则应首先调用 <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> 方法从注册表中检索时区信息。 如果方法调用失败，则异常处理程序应创建时区的新实例，或通过对序列化的 <xref:System.TimeZoneInfo> 对象进行反序列化来重新创建它。 请参阅[如何： 从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)有关示例。

## <a name="see-also"></a>请参阅

[日期、 时间和时区](../../../docs/standard/datetime/index.md)
[查找本地系统上定义的时区](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)
[如何： 访问预定义的 UTC 和当地时间区域对象](../../../docs/standard/datetime/access-utc-and-local.md)
