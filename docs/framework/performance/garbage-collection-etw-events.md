---
title: "垃圾回收 ETW 事件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ETW, 垃圾回收事件 (CLR)"
  - "垃圾回收事件 [.NET Framework]"
  - "GC 事件"
ms.assetid: f14b6fd7-0966-4d87-bc89-54ef3a44a94a
caps.latest.revision: 21
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 20
---
# 垃圾回收 ETW 事件
<a name="top"></a> 这些事件可收集有关垃圾回收的信息。 它们可帮助进行诊断和调试，包括确定垃圾回收执行的次数、垃圾回收期间释放的内存量等。  
  
 此类别包含以下事件：  
  
-   [GCStart\_V1 事件](#gcstart_v1_event)  
  
-   [GCEnd\_V1 事件](#gcend_v1_event)  
  
-   [GCHeapStats\_V1 事件](#gcheapstats_v1_event)  
  
-   [GCCreateSegment\_V1 事件](#gccreatesegment_v1_event)  
  
-   [GCFreeSegment\_V1 事件](#gcfreesegment_v1_event)  
  
-   [GCRestartEEBegin\_V1 事件](#gcrestarteebegin_v1_event)  
  
-   [GCRestartEEEnd\_V1 事件](#gcrestarteeend_v1_event)  
  
-   [GCSuspendEE\_V1 事件](#gcsuspendee_v1_event)  
  
-   [GCSuspendEEEnd\_V1 事件](#gcsuspendeeend_v1_event)  
  
-   [GCAllocationTick\_V2 事件](#gcallocationtick_v2_event)  
  
-   [GCFinalizersBegin\_V1 事件](#gcfinalizersbegin_v1_event)  
  
-   [GCFinalizersEnd\_V1 事件](#gcfinalizersend_v1_event)  
  
-   [GCCreateConcurrentThread\_V1 事件](#gccreateconcurrentthread_v1_event)  
  
-   [GCTerminateConcurrentThread\_V1 事件](#gcterminateconcurrentthread_v1_event)  
  
<a name="gcstart_v1_event"></a>   
## GCStart\_V1 事件  
 下表显示了关键字和级别。 （有关详细信息，请参阅 [CLR ETW 关键字和级别](../../../docs/framework/performance/clr-etw-keywords-and-levels.md)。）  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCStart_V1`|1|垃圾回收已启动。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|---------|----------|--------|  
|计数|win:UInt32|第 *n* 代垃圾回收。|  
|深度|win:UInt32|正在回收的代。|  
|原因|win:UInt32|垃圾回收的触发原因：<br /><br /> 0x0 \- 小型对象堆分配。<br /><br /> 0x1 \- 已引发。<br /><br /> 0x2 \- 内存不足。<br /><br /> 0x3 \- 空。<br /><br /> 0x4 \- 大型对象堆分配。<br /><br /> 0x5 \- 空间不足（针对小型对象堆）。<br /><br /> 0x6 \- 空间不足（针对大型对象堆）。<br /><br /> 0x7 \- 已引发，但未强制为阻止。|  
|类型|win:UInt32|0x0 \- 在后台垃圾回收外部发生了垃圾回收阻止。<br /><br /> 0x1 \- 后台垃圾回收。<br /><br /> 0x0 \- 后台垃圾回收期间发生了垃圾回收阻止。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 [返回页首](#top)  
  
<a name="gcend_v1_event"></a>   
## GCEnd\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCEnd_V1`|2|垃圾回收已结束。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|---------|----------|--------|  
|计数|win:UInt32|第 *n* 代垃圾回收。|  
|深度|win:UInt32|已回收的代。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 [返回页首](#top)  
  
<a name="gcheapstats_v1_event"></a>   
## GCHeapStats\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|说明|  
|-----------|-----------|--------|  
|`GCHeapStats_V1`|4|在每次垃圾回收结束时显示堆统计信息。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|---------|----------|--------|  
|GenerationSize0|win:UInt64|第 0 代内存的大小（以字节为单位）。|  
|TotalPromotedSize0|win:UInt64|从第 0 代提升到第 1 代的字节数。|  
|GenerationSize1|win:UInt64|第 1 代内存的大小（以字节为单位）。|  
|TotalPromotedSize1|win:UInt64|从第 1 代提升到第 2 代的字节数。|  
|GenerationSize2|win:UInt64|第 2 代内存的大小（以字节为单位）。|  
|TotalPromotedSize2|win:UInt64|上次回收后仍存在于第 2 代中的字节数。|  
|GenerationSize3|win:UInt64|大型对象堆的大小（以字节为单位）。|  
|TotalPromotedSize3|win:UInt64|上次回收后仍存在于大型对象堆中的字节数。|  
|FinalizationPromotedSize|win:UInt64|准备终结的对象的总大小（以字节为单位）。|  
|FinalizationPromotedCount|win:UInt64|已准备好进行终结的对象的数目。|  
|PinnedObjectCount|win:UInt32|固定（不可移动）对象的数目。|  
|SinkBlockCount|win:UInt32|正在使用的同步块的数目。|  
|GCHandleCount|win:UInt32|使用中的垃圾回收句柄的数目。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 [返回页首](#top)  
  
<a name="gccreatesegment_v1_event"></a>   
## GCCreateSegment\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCCreateSegment_V1`|5|已创建的新的垃圾回收段。 此外，当在已运行的进程中启用跟踪时，将为每个现有段引发此事件。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|---------|----------|--------|  
|Address|win:UInt64|段的地址。|  
|大小|win:UInt64|段的大小。|  
|类型|win:UInt32|0x0 \- 小型对象堆。<br /><br /> 0x0 \- 大型对象堆。<br /><br /> 0x2 \- 只读堆。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 请注意，由垃圾回收器分配的段的大小特定于实现，且随时可能更改（包括定期更新）。 应用程序不应假设特定段的大小或依赖于此大小，也不应尝试配置段分配可用的内存量。  
  
 [返回页首](#top)  
  
<a name="gcfreesegment_v1_event"></a>   
## GCFreeSegment\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCFreeSegment_V1`|6|已释放垃圾回收段。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|---------|----------|--------|  
|Address|win:UInt64|段的地址。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 [返回页首](#top)  
  
<a name="gcrestarteebegin_v1_event"></a>   
## GCRestartEEBegin\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCRestartEEBegin_V1`|7|已开始从公共语言运行时挂起进行恢复。|  
  
 无事件数据。  
  
 [返回页首](#top)  
  
<a name="gcrestarteeend_v1_event"></a>   
## GCRestartEEEnd\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCRestartEEEnd_V1`|3|从公共语言运行时挂起进行的恢复已结束。|  
  
 无事件数据。  
  
 [返回页首](#top)  
  
<a name="gcsuspendee_v1_event"></a>   
## GCSuspendEE\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCSuspendEE_V1`|9|开始挂起垃圾回收的执行引擎。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|---------|----------|--------|  
|原因|win:UInt16|0x0 \- 其他。<br /><br /> 0x1 \- 垃圾回收。<br /><br /> 0x2 \- 应用程序域关闭。<br /><br /> 0x3 \- 代码间距调整。<br /><br /> 0x4 \- 关闭。<br /><br /> 0x5 \- 调试器。<br /><br /> 0x6 \- 准备垃圾回收。|  
|计数|win:UInt32|挂起的线程数。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 [返回页首](#top)  
  
<a name="gcsuspendeeend_v1_event"></a>   
## GCSuspendEEEnd\_V1 事件  
 下表显示了关键字和级别：  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息：  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCSuspendEEEnd_V1`|8|结束垃圾回收执行引擎的挂起。|  
  
 无事件数据。  
  
 [返回页首](#top)  
  
<a name="gcallocationtick_v2_event"></a>   
## GCAllocationTick\_V2 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCAllocationTick_V2`|10|每次大约分配 100 KB。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|---------|----------|--------|  
|AllocationAmount|win:UInt32|分配大小（以字节为单位）。 对于小于 ULONG（4,294,967,295 字节）长度的分配，此值为精确值。 如果分配长度更大，则此字段包含了截断的值。 对于非常大的分配使用 `AllocationAmount64`。|  
|AllocationKind|win:UInt32|0x0 \- 小型对象分配（小型对象堆中的分配）。<br /><br /> 0x0 \- 大型对象分配（大型对象堆中的分配）。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
|AllocationAmount64|win:UInt64|分配大小（以字节为单位）。 对于非常大的分配，此值为精确值。|  
|TypeId|win:Pointer|MethodTable 的地址。 如果在此事件期间分配了几种类型的对象，则此地址为对应于分配的最后一个对象（导致超过 100 KB 阙值的对象）的 MethodTable 地址。|  
|TypeName|win:UnicodeString|已分配的类型的名称。 如果在此事件期间分配了几种类型的对象，则此地址为对应于分配的最后一个类型（导致超过 100 KB 阙值的对象）。|  
|HeapIndex|win:UInt32|此对象所分配到的堆。 与工作站垃圾回收一起运行时，此值为 0（零）。|  
  
 [返回页首](#top)  
  
<a name="gcfinalizersbegin_v1_event"></a>   
## GCFinalizersBegin\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCFinalizersBegin_V1`|14|开始运行终结器。|  
  
 无事件数据。  
  
 [返回页首](#top)  
  
<a name="gcfinalizersend_v1_event"></a>   
## GCFinalizersEnd\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCFinalizersEnd_V1`|13|结束运行终结器。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|---------|----------|--------|  
|计数|win:UInt32|运行的终结器数。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
 [返回页首](#top)  
  
<a name="gccreateconcurrentthread_v1_event"></a>   
## GCCreateConcurrentThread\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
|`ThreadingKeyword` \(0x10000\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCCreateConcurrentThread_V1`|11|已创建并发垃圾回收线程。|  
  
 无事件数据。  
  
 [返回页首](#top)  
  
<a name="gcterminateconcurrentthread_v1_event"></a>   
## GCTerminateConcurrentThread\_V1 事件  
 下表显示了关键字和级别。  
  
|引发事件的关键字|级别|  
|--------------|--------|  
|`GCKeyword` \(0x1\)|信息性 \(4\)|  
|`ThreadingKeyword` \(0x10000\)|信息性 \(4\)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|-----------|----------------|  
|`GCTerminateConcurrentThread_V1`|12|已终止并发垃圾回收线程。|  
  
 无事件数据。  
  
## 请参阅  
 [CLR ETW 事件](../../../docs/framework/performance/clr-etw-events.md)