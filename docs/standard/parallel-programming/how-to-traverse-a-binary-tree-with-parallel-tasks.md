---
title: 如何：使用并行任务遍历二叉树
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to traverse a tree
ms.assetid: 4265d169-6c69-4f36-b10d-b7ae7f72f4df
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d6446145d34d22503697bbca59bc2cb2cd2619cb
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-traverse-a-binary-tree-with-parallel-tasks"></a>如何：使用并行任务遍历二叉树
下面的示例展示了两种使用并行任务遍历树数据结构的方式。 树创建本身是留给大家练练手的。  
  
## <a name="example"></a>示例  
 [!code-csharp[TPL#16](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#16)]
 [!code-vb[TPL#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/treewalk.vb#16)]  
  
 上面的两种方法在功能上是相当的。 通过使用 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> 方法创建和运行任务，可以从可用于等待任务和处理异常的任务中返回句柄。  
  
## <a name="see-also"></a>请参阅  
 [任务并行库 (TPL)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)
