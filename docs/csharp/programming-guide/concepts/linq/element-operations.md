---
title: 元素运算 (C#)
ms.date: 07/20/2015
ms.assetid: 283206c9-3246-4c48-b01a-d9de409a7231
ms.openlocfilehash: 5c10603d9e074faf891d41fa6b39614fcc167c8a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="element-operations-c"></a>元素运算 (C#)
元素运算从序列中返回唯一、特定的元素。  
  
 下节列出了执行元素运算的标准查询运算符方法。  
  
## <a name="methods"></a>方法  
  
|方法名|描述|C# 查询表达式语法|详细信息|  
|-----------------|-----------------|---------------------------------|----------------------|  
|ElementAt|返回集合中指定索引处的元素。|不适用。|<xref:System.Linq.Enumerable.ElementAt%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ElementAt%2A?displayProperty=nameWithType>|  
|ElementAtOrDefault|返回集合中指定索引处的元素；如果索引超出范围，则返回默认值。|不适用。|<xref:System.Linq.Enumerable.ElementAtOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ElementAtOrDefault%2A?displayProperty=nameWithType>|  
|First|返回集合的第一个元素或满足条件的第一个元素。|不适用。|<xref:System.Linq.Enumerable.First%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.First%2A?displayProperty=nameWithType>|  
|FirstOrDefault|返回集合的第一个元素或满足条件的第一个元素。 如果此类元素不存在，则返回默认值。|不适用。|<xref:System.Linq.Enumerable.FirstOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.FirstOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.FirstOrDefault%60%601%28System.Linq.IQueryable%7B%60%600%7D%29?displayProperty=nameWithType>|  
|上一个|返回集合的最后一个元素或满足条件的最后一个元素。|不适用。|<xref:System.Linq.Enumerable.Last%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Last%2A?displayProperty=nameWithType>|  
|LastOrDefault|返回集合的最后一个元素或满足条件的最后一个元素。 如果此类元素不存在，则返回默认值。|不适用。|<xref:System.Linq.Enumerable.LastOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.LastOrDefault%2A?displayProperty=nameWithType>|  
|Single|返回集合的唯一一个元素或满足条件的唯一一个元素。|不适用。|<xref:System.Linq.Enumerable.Single%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Single%2A?displayProperty=nameWithType>|  
|SingleOrDefault|返回集合的唯一一个元素或满足条件的唯一一个元素。 如果此类元素不存在，或该集合不是仅包含一个元素，则返回默认值。|不适用。|<xref:System.Linq.Enumerable.SingleOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.SingleOrDefault%2A?displayProperty=nameWithType>|  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Linq>  
 [标准查询运算符概述 (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)  
 [如何：查询目录树中的一个或多个最大的文件 (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-query-for-the-largest-file-or-files-in-a-directory-tree-linq.md)
