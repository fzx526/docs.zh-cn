---
title: 未能从委托中推理类型参数
ms.date: 07/20/2015
f1_keywords:
- bc36564
- vbc36564
helpviewer_keywords:
- BC36564
ms.assetid: 21312807-e1cd-4ac1-ae1c-c28a9c25164d
ms.openlocfilehash: 757483f1e88276dd9db82de1c2a7e47b5c975b0a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="type-arguments-could-not-be-inferred-from-the-delegate"></a>未能从委托中推理类型参数
赋值语句使用 `AddressOf` 将泛型过程的地址赋给委托，但它不会为泛型过程提供任何类型参数。  
  
 通常，在调用某个泛型类型时，要为该泛型类型定义的每个类型形参提供一个类型实参。 如果未提供任何类型实参，编译器将尝试推断要传递给类型形参的类型。 如果上下文未提供充足的信息供编译器推断类型，则将生成错误。  
  
 **错误 ID:** BC36564  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   为 `AddressOf` 表达式中的泛型过程指定类型参数。  
  
## <a name="see-also"></a>请参阅  
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)  
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)  
 [在 Visual Basic 中的泛型过程](../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)  
 [类型列表](../../../visual-basic/language-reference/statements/type-list.md)  
 [扩展方法](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
