---
title: 如何：使用画布的附加属性来定位子元素
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- attached properties [WPF Designer]
- Canvas control [WPF], attached properties
ms.assetid: 48f1d25d-3820-4107-a4cc-d6c1e5664a44
ms.openlocfilehash: 886440304dc1bebdcfae66676254bef7ac35457d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-use-the-attached-properties-of-canvas-to-position-child-elements"></a>如何：使用画布的附加属性来定位子元素
此示例演示如何使用的附加的属性<xref:System.Windows.Controls.Canvas>来定位子元素。  
  
## <a name="example"></a>示例  
 下面的示例添加四个<xref:System.Windows.Controls.Button>元素作为子元素的父<xref:System.Windows.Controls.Canvas>。 每个子元素表示的非重复的附加的属性的<xref:System.Windows.Controls.Canvas>: <xref:System.Windows.Controls.Canvas.Bottom%2A>， <xref:System.Windows.Controls.Canvas.Left%2A>， <xref:System.Windows.Controls.Canvas.Right%2A>，和<xref:System.Windows.Controls.Canvas.Top%2A>。 每个<xref:System.Windows.Controls.Button>位于相对于父<xref:System.Windows.Controls.Canvas>并根据其分配的属性值。  
  
 [!code-cpp[CanvasAttachedProperties#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/CanvasAttachedProperties/CPP/CanvasAttachedProps.cpp#1)]
 [!code-csharp[CanvasAttachedProperties#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasAttachedProperties/CSharp/CanvasAttachedProps.cs#1)]
 [!code-vb[CanvasAttachedProperties#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasAttachedProperties/VisualBasic/CanvasAttachedProps.vb#1)]  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Windows.Controls.Canvas>  
 <xref:System.Windows.Controls.Canvas.Bottom%2A>  
 <xref:System.Windows.Controls.Canvas.Left%2A>  
 <xref:System.Windows.Controls.Canvas.Right%2A>  
 <xref:System.Windows.Controls.Canvas.Top%2A>  
 <xref:System.Windows.Controls.Button>  
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)  
 [帮助主题](../../../../docs/framework/wpf/controls/canvas-how-to-topics.md)  
 [附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)
