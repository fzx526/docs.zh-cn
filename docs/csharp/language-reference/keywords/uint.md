---
title: uint（C# 参考）
ms.date: 03/14/2017
f1_keywords:
- uint
- uint_CSharpKeyword
helpviewer_keywords:
- uint keyword [C#]
ms.assetid: e93e42c6-ec72-4b0b-89df-2fd8d36f7a7b
ms.openlocfilehash: fa0169ad92819cee36832d6c928202eb0dd6733e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="uint-c-reference"></a>uint（C# 参考）

`uint` 关键字表示一种整型类型，该类型根据下表显示的大小和范围存储值。  
  
|类型|范围|大小|.NET Framework 类型|  
|----------|-----------|----------|-------------------------|  
|`uint`|0 到 4,294,967,295|无符号的 32 位整数|<xref:System.UInt32?displayProperty=nameWithType>|  
  
 **请注意**：`uint` 类型不符合 CLS。 请尽可能使用 `int`。  
  
## <a name="literals"></a>文本  

可以通过为其分配十进制文本、十六进制文本或（从 C# 7.0 开始）二进制文本来声明和初始化 `uint` 变量。 如果整数文本在 `uint` 范围之外（即，如果它小于 <xref:System.UInt32.MinValue?displayProperty=nameWithType> 或大于 <xref:System.UInt32.MaxValue?displayProperty=nameWithType>），会发生编译错误。

在以下示例中，表示为十进制、十六进制和二进制文本且等于 3,000,000,000 的整数被分配给 `uint` 值。  
  
[!code-csharp[uint](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#UInt)]  

> [!NOTE] 
> 使用前缀 `0x` 或 `0X` 表示十六进制文本，使用前缀 `0b` 或 `0B` 表示二进制文本。 十进制文本没有前缀。 

从 C# 7.0 开始，添加了一些功能以增强可读性。 
 - C# 7.0 允许将下划线字符 (`_`) 用作数字分隔符。
 - C# 7.2 允许将 `_` 用作二进制或十六进制文本的数字分隔符，位于前缀之后。 十进制文本不能够有前导下划线。

下面是一些示例。

[!code-csharp[uint](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#UIntS)]  
 
 整数文本还可包含表示类型的后缀。 后缀 `U` 或“u”表示 `uint` 或 `ulong`，具体取决于文本的数字值。 以下示例使用 `u` 后缀来表示这两种类型的无符号整数。 请注意第一个文本为 `uint`，因为其值小于 <xref:System.UInt32.MaxValue?displayProperty=nameWithType>，而第二个文本为 `ulong`，因为其值大于 <xref:System.UInt32.MaxValue?displayProperty=nameWithType>。

[!code-csharp[usuffix](../../../../samples/snippets/csharp/language-reference/keywords/numeric-suffixes.cs#1)]  
 
如果整数文本没有后缀，则其类型为以下类型中可表示其值的第一个类型： 

1. [int](int.md)
2. `uint`
3. [long](../../../csharp/language-reference/keywords/long.md)
4. [ulong](../../../csharp/language-reference/keywords/ulong.md) 
  
## <a name="conversions"></a>转换  
 存在从 `uint` 到 [long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md)、[float](../../../csharp/language-reference/keywords/float.md)、[double](../../../csharp/language-reference/keywords/double.md) 或 [decimal](../../../csharp/language-reference/keywords/decimal.md) 的预定义隐式转换。 例如:  
  
```csharp  
float myFloat = 4294967290;   // OK: implicit conversion to float  
```  
  
 存在从 [byte](../../../csharp/language-reference/keywords/byte.md)、[ushort](../../../csharp/language-reference/keywords/ushort.md) 或 [char](../../../csharp/language-reference/keywords/char.md) 到 `uint` 的预定义隐式转换。 否则必须使用转换。 例如，如果不使用转换，以下赋值语句会生成编译错误：  
  
```csharp  
long aLong = 22;  
// Error -- no implicit conversion from long:  
uint uInt1 = aLong;   
// OK -- explicit conversion:  
uint uInt2 = (uint)aLong;  
```  
  
 另请注意，不存在从浮点类型到 `uint` 类型的隐式转换。 例如，除非使用显式强制转换，否则以下语句将生成编译器错误：  
  
```csharp  
// Error -- no implicit conversion from double:  
uint x = 3.0;  
// OK -- explicit conversion:  
uint y = (uint)3.0;   
```  
  
 有关兼用浮点类型和整型类型的算术表达式的信息，请参阅 [float](../../../csharp/language-reference/keywords/float.md) 和 [double](../../../csharp/language-reference/keywords/double.md)。  
  
 有关隐式数值转换规则的详细信息，请参阅[隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 <xref:System.UInt32>  
 [C# 参考](../../../csharp/language-reference/index.md)  
 [C# 编程指南](../../../csharp/programming-guide/index.md)  
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)  
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)  
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)  
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)  
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
