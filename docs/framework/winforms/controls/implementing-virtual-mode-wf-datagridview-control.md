---
title: 演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data [Windows Forms], managing large data sets
- DataGridView control [Windows Forms], virtual mode
- virtual mode [Windows Forms], walkthroughs
- DataGridView control [Windows Forms], large data sets
- walkthroughs [Windows Forms], DataGridView control
ms.assetid: 74eb5276-5ab8-4ce0-8005-dae751d85f7c
ms.openlocfilehash: 52e93ebe0b2903fdf2fe97f4ce812331e740f8b0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="walkthrough-implementing-virtual-mode-in-the-windows-forms-datagridview-control"></a>演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式
如果想要显示非常大量的表格数据<xref:System.Windows.Forms.DataGridView>控件，则可设置<xref:System.Windows.Forms.DataGridView.VirtualMode%2A>属性`true`和显式管理与其数据存储区的控件的交互。 这样可以微调控件在此情况下的性能。  
  
 <xref:System.Windows.Forms.DataGridView>控件提供可以处理与自定义数据存储区交互的几个事件。 本演练将指导你完成实现这些事件处理程序的过程。 本主题中的代码示例用于说明目的使用非常简单的数据源。 在生产设置中，你通常将加载只有需要到缓存中，显示和处理的行<xref:System.Windows.Forms.DataGridView>事件交互并进行更新缓存。 有关详细信息，请参阅[实时数据加载在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)  
  
 若要将代码复制本主题中的一个单独的清单，请参阅[如何： 在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md)。  
  
## <a name="creating-the-form"></a>创建窗体  
  
#### <a name="to-implement-virtual-mode"></a>若要实现虚拟模式  
  
1.  创建一个类，派生自<xref:System.Windows.Forms.Form>和包含<xref:System.Windows.Forms.DataGridView>控件。  
  
     下面的代码包含一些基本的初始化。 它声明将在后续步骤中使用某些变量，提供`Main`方法，并提供在类构造函数的简单窗体布局。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#001](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#001)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#001](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#001)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#001](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#001)]  
    [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#002](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#002)]
    [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#002](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#002)]
    [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#002](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#002)]  
  
2.  实现你的窗体的处理<xref:System.Windows.Forms.Form.Load>初始化的事件<xref:System.Windows.Forms.DataGridView>控件并填充具有示例值的数据存储区。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#110](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#110)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#110)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#110)]  
  
3.  实现的处理程序<xref:System.Windows.Forms.DataGridView.CellValueNeeded>从数据存储中检索请求的单元格的值的事件或`Customer`当前正在编辑的对象。  
  
     每当发生此事件<xref:System.Windows.Forms.DataGridView>控件需要绘制单元格。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#120](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#120)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#120)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#120)]  
  
4.  实现的处理程序<xref:System.Windows.Forms.DataGridView.CellValuePushed>存储中的编辑后的单元值的事件`Customer`表示编辑过的行的对象。 每当用户提交单元格值更改，将发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#130](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#130)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#130](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#130)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#130](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#130)]  
  
5.  实现的处理程序<xref:System.Windows.Forms.DataGridView.NewRowNeeded>创建一个新的事件`Customer`表示新创建的行的对象。  
  
     每当用户输入新记录的行，将发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#140](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#140)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#140](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#140)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#140](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#140)]  
  
6.  实现的处理程序<xref:System.Windows.Forms.DataGridView.RowValidated>将新的或已修改行保存到数据存储的事件。  
  
     每当用户更改当前行，将发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#150](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#150)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#150](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#150)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#150](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#150)]  
  
7.  实现的处理程序<xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>事件，该值指示是否<xref:System.Windows.Forms.DataGridView.CancelRowEdit>用户按 esc 键两次处于编辑模式或第一次外部编辑模式，用信号通知行恢复时，事件将会发生。  
  
     默认情况下，<xref:System.Windows.Forms.DataGridView.CancelRowEdit>在恢复行已被修改任何当前行中的单元格，除非时发生<xref:System.Windows.Forms.QuestionEventArgs.Response%2A?displayProperty=nameWithType>属性设置为`true`中<xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>事件处理程序。 当在运行时确定提交作用域时，此事件非常有用。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#160](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#160)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#160](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#160)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#160](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#160)]  
  
8.  实现的处理程序<xref:System.Windows.Forms.DataGridView.CancelRowEdit>放弃的值的事件`Customer`对象，表示当前行。  
  
     当用户按 esc 键两次处于编辑模式或第一次外部编辑模式，用信号通知行恢复时，将发生此事件。 如果没有当前行中的单元格进行了修改，或如果不会发生此事件的值<xref:System.Windows.Forms.QuestionEventArgs.Response%2A?displayProperty=nameWithType>属性已设置为`false`中<xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>事件处理程序。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#170](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#170)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#170](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#170)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#170](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#170)]  
  
9. 实现的处理程序<xref:System.Windows.Forms.DataGridView.UserDeletingRow>删除现有的事件`Customer`从数据存储的对象或放弃未保存`Customer`表示新创建的行的对象。  
  
     每当用户通过单击行标题并按 DELETE 键删除行，将发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#180](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#180)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#180](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#180)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#180](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#180)]  
  
10. 实现一个简单`Customers`类来表示此代码示例使用的数据项目。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#200](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#200)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#200](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#200)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#200](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#200)]  
  
## <a name="testing-the-application"></a>测试应用程序  
 你现在可以测试窗体，以确保其行为与预期相同。  
  
#### <a name="to-test-the-form"></a>若要测试窗体  
  
-   编译并运行该应用程序。  
  
     你将看到<xref:System.Windows.Forms.DataGridView>填充三个客户记录的控件。 你可以修改行中的多个单元格的值，并按 ESC，两次处于编辑模式和一次外部编辑模式，以便还原为其原始值的整个行。 当你修改、 添加或删除在控件中，行`Customer`修改、 添加或删除以及数据存储区中的对象。  
  
## <a name="next-steps"></a>后续步骤  
 此应用程序，必须处理才能实现中的虚拟模式的事件基本了解<xref:System.Windows.Forms.DataGridView>控件。 您可以提高此多种方式的基本应用程序：  
  
-   实现缓存从外部数据库的值的数据存储区。 缓存应检索并放弃根据需要的值，以使其仅包含必要的操作时使用的少量内存客户端计算机上的显示。  
  
-   微调具体取决于你的要求的数据存储的性能。 例如，你可能想要通过使用更大的缓存大小以及尽量减少数据库查询数补偿慢速网络连接，而不是客户端计算机的内存限制。  
  
 有关缓存从外部数据库的值的详细信息，请参阅[如何： 实现虚拟模式在 Windows 窗体 DataGridView 控件中的实时数据加载](../../../../docs/framework/winforms/controls/virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Windows.Forms.DataGridView>  
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>  
 <xref:System.Windows.Forms.DataGridView.CellValueNeeded>  
 <xref:System.Windows.Forms.DataGridView.CellValuePushed>  
 <xref:System.Windows.Forms.DataGridView.NewRowNeeded>  
 <xref:System.Windows.Forms.DataGridView.RowValidated>  
 <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>  
 <xref:System.Windows.Forms.DataGridView.CancelRowEdit>  
 <xref:System.Windows.Forms.DataGridView.UserDeletingRow>  
 [Windows 窗体 DataGridView 控件中的性能调整](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)  
 [有关缩放 Windows 窗体 DataGridView 控件的最佳做法](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)  
 [在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)  
 [如何：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md)
