---
title: 203 - ClientParameterInspectorAfterCallInvoked
ms.date: 03/30/2017
ms.assetid: b9592212-07e2-43e0-8b00-affd195cf55a
ms.openlocfilehash: 57192b44a0c3babc77fcca13ad4a1433b85bfdd7
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="203---clientparameterinspectoraftercallinvoked"></a>203 - ClientParameterInspectorAfterCallInvoked
## <a name="properties"></a>属性  
  
|||  
|-|-|  
|ID|203|  
|关键字|疑难解答，ServiceModel|  
|级别|信息|  
|通道|Microsoft-Windows-应用程序服务器-应用程序/分析|  
  
## <a name="description"></a>描述  
 服务模型在客户端参数检查器上调用 `AfterCall` 方法之后，将发出此事件。  
  
## <a name="message"></a>消息  
 调度程序对“%1”类型的 ClientParameterInspector 调用了“AfterCall”。  
  
## <a name="details"></a>详细信息  
  
|数据项名称|数据项类型|描述|  
|--------------------|--------------------|-----------------|  
|TypeName|`xs:string`|所调用检查器的类型的 CLR FullName。|  
|HostReference|`xs:string`|对于 Web 承载的服务，此字段唯一标识 Web 层次结构中的服务。 其格式定义为网站名称应用程序虚拟路径&#124;服务虚拟路径&#124;ServiceName。 示例: 默认网站/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|
