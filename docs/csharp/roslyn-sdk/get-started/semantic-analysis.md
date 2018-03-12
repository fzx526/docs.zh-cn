---
title: "语义分析入门"
description: "本教程概述如何使用.NET 编译器 SDK 进行语义分析。"
author: billwagner
ms.author: wiwagn
ms.date: 02/06/2018
ms.topic: conceptual
ms.prod: .net
ms.devlang: devlang-csharp
ms.custom: mvc
ms.openlocfilehash: 04bd57dfd32a51bf5d7e3a573e34140b0feec90f
ms.sourcegitcommit: 3a96c706e4dbb4667bf3bf37edac9e1666646f93
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/27/2018
---
# <a name="get-started-with-semantic-analysis"></a><span data-ttu-id="7d176-103">语义分析入门</span><span class="sxs-lookup"><span data-stu-id="7d176-103">Get started with semantic analysis</span></span>

<span data-ttu-id="7d176-104">本教程假定你熟悉语法 API。</span><span class="sxs-lookup"><span data-stu-id="7d176-104">This tutorial assumes you're familiar with the Syntax API.</span></span> <span data-ttu-id="7d176-105">[语法分析入门](syntax-analysis.md)一文提供了详细介绍。</span><span class="sxs-lookup"><span data-stu-id="7d176-105">The [get started with syntax analysis](syntax-analysis.md) article provides sufficient introduction.</span></span>

<span data-ttu-id="7d176-106">在本教程中，你将了解“符号”和“绑定 API”。</span><span class="sxs-lookup"><span data-stu-id="7d176-106">In this tutorial, you explore the **Symbol** and **Binding APIs**.</span></span> <span data-ttu-id="7d176-107">这些 API 提供关于程序语义含义的信息。</span><span class="sxs-lookup"><span data-stu-id="7d176-107">These APIs provide information about the _semantic meaning_ of a program.</span></span> <span data-ttu-id="7d176-108">它们帮助你就程序中的符号所代表的类型进行问答。</span><span class="sxs-lookup"><span data-stu-id="7d176-108">They enable you to ask and answer questions about the types represented by any symbol in your program.</span></span>

## <a name="understanding-compilations-and-symbols"></a><span data-ttu-id="7d176-109">了解编译和符号</span><span class="sxs-lookup"><span data-stu-id="7d176-109">Understanding Compilations and Symbols</span></span>

<span data-ttu-id="7d176-110">随着 .NET 编译器 SDK 的使用越来越多，你会越来越熟悉语法 API 和语义 API 之间的区别。</span><span class="sxs-lookup"><span data-stu-id="7d176-110">As you work more with the .NET Compiler SDK, you become familiar with the distinctions between Syntax API and the Semantic API.</span></span> <span data-ttu-id="7d176-111">“语法 API”使你可以看到程序的结构。</span><span class="sxs-lookup"><span data-stu-id="7d176-111">The **Syntax API** allows you to look at the _structure_ of a program.</span></span> <span data-ttu-id="7d176-112">但是经常会需要更多关于程序的语义或含义的信息。</span><span class="sxs-lookup"><span data-stu-id="7d176-112">However, often you want richer information about the semantics or _meaning_ of a program.</span></span> <span data-ttu-id="7d176-113">虽然可以独立地对松散的代码文件或 VB 或 C# 代码的代码片段进行语法上的分析，但是凭空提出类似“这是什么类型的变量？”这样的问题毫无意义。</span><span class="sxs-lookup"><span data-stu-id="7d176-113">While a loose code file or snippet of VB or C# code can be syntactically analyzed in isolation, it's not meaningful to ask questions such as "what's the type of this variable" in a vacuum.</span></span> <span data-ttu-id="7d176-114">类型名称的含义可能取决于程序集引用、命名空间导入或其他代码文件。</span><span class="sxs-lookup"><span data-stu-id="7d176-114">The meaning of a type name may be dependent on assembly references, namespace imports, or other code files.</span></span> <span data-ttu-id="7d176-115">使用**语义 API** 回答这些问题，特别是 <xref:Microsoft.CodeAnalysis.Compilation?displayProperty=nameWithType> 类。</span><span class="sxs-lookup"><span data-stu-id="7d176-115">Those questions are answered using the **Semantic API**, specifically the <xref:Microsoft.CodeAnalysis.Compilation?displayProperty=nameWithType> class.</span></span>

<span data-ttu-id="7d176-116"><xref:Microsoft.CodeAnalysis.Compilation> 实例类似于编译器所看见的单个项目，且代表编译 Visual Basic 或 C# 程序所需的一切。</span><span class="sxs-lookup"><span data-stu-id="7d176-116">An instance of <xref:Microsoft.CodeAnalysis.Compilation> is analogous to a single project as seen by the compiler and represents everything needed to compile a Visual Basic or C# program.</span></span> <span data-ttu-id="7d176-117">“编译”包括一组要编译的源文件、程序集引用和编译器选项。</span><span class="sxs-lookup"><span data-stu-id="7d176-117">The **compilation** includes the set of source files to be compiled, assembly references, compiler options.</span></span> <span data-ttu-id="7d176-118">可以使用此上下文中所有的其他信息来推断代码的含义。</span><span class="sxs-lookup"><span data-stu-id="7d176-118">You can reason about the meaning of the code using all the other information in this context.</span></span> <span data-ttu-id="7d176-119"><xref:Microsoft.CodeAnalysis.Compilation> 允许你查找“符号” - 类似名称和其他表达式引用的类型、命名空间、成员和变量的实体。</span><span class="sxs-lookup"><span data-stu-id="7d176-119">A <xref:Microsoft.CodeAnalysis.Compilation> allows you to find **Symbols** - entities such as types, namespaces, members, and variables which names and other expressions refer to.</span></span> <span data-ttu-id="7d176-120">将名称和表达式与“符号”进行关联的过程被称为“绑定”。</span><span class="sxs-lookup"><span data-stu-id="7d176-120">The process of associating names and expressions with **Symbols** is called **Binding**.</span></span>

<span data-ttu-id="7d176-121">与 <xref:Microsoft.CodeAnalysis.SyntaxTree?displayProperty=nameWithType> 类似，<xref:Microsoft.CodeAnalysis.Compilation> 是一个带有语言特定派生类的抽象类。</span><span class="sxs-lookup"><span data-stu-id="7d176-121">Like <xref:Microsoft.CodeAnalysis.SyntaxTree?displayProperty=nameWithType>, <xref:Microsoft.CodeAnalysis.Compilation> is an abstract class with language-specific derivatives.</span></span> <span data-ttu-id="7d176-122">在创建编译实例时，必须在 <xref:Microsoft.CodeAnalysis.CSharp.CSharpCompilation?displayProperty=nameWithType>（或 <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicCompilation?displayProperty=nameWithType>）类上调用工厂方法。</span><span class="sxs-lookup"><span data-stu-id="7d176-122">When creating an instance of Compilation, you must invoke a factory method on the <xref:Microsoft.CodeAnalysis.CSharp.CSharpCompilation?displayProperty=nameWithType> (or <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicCompilation?displayProperty=nameWithType>) class.</span></span>

## <a name="querying-symbols"></a><span data-ttu-id="7d176-123">查询符号</span><span class="sxs-lookup"><span data-stu-id="7d176-123">Querying symbols</span></span>

<span data-ttu-id="7d176-124">在本教程中，你会再次看到“Hello World”程序。</span><span class="sxs-lookup"><span data-stu-id="7d176-124">In this tutorial, you look at the "Hello World" program again.</span></span> <span data-ttu-id="7d176-125">这次你将在该程序中查询符号，以理解这些符号所代表的类型。</span><span class="sxs-lookup"><span data-stu-id="7d176-125">This time, you query the symbols in the program to understand what types those symbols represent.</span></span> <span data-ttu-id="7d176-126">在命名空间中查询类型，并学习如何查找类型上可用的方法。</span><span class="sxs-lookup"><span data-stu-id="7d176-126">You query for the types in a namespace, and learn to find the methods available on a type.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d176-127">下列示例需要安装 .NET 编译器 SDK 作为 Visual Studio 2017 的一部分。</span><span class="sxs-lookup"><span data-stu-id="7d176-127">The following samples require the **.NET Compiler SDK** installed as part of Visual Studio 2017.</span></span> <span data-ttu-id="7d176-128">你可以找到 .NET 编译器 SDK，它是列在 Visual Studio 扩展开发工作负荷下的最后一个可选组件。</span><span class="sxs-lookup"><span data-stu-id="7d176-128">You can find the .NET Compiler SDK as the last optional component listed under the **Visual Studio extension development** workload.</span></span> <span data-ttu-id="7d176-129">安装此组件时，不会安装模板。</span><span class="sxs-lookup"><span data-stu-id="7d176-129">The templates aren't installed without this component.</span></span>

<span data-ttu-id="7d176-130">可以在[我们的 GitHub 示例存储库](https://github.com/dotnet/samples/csharp/roslyn-sdk/SemanticQuickStart)中看到此示例的已完成代码。</span><span class="sxs-lookup"><span data-stu-id="7d176-130">You can see the finished code for this sample in [our GitHub samples repository](https://github.com/dotnet/samples/csharp/roslyn-sdk/SemanticQuickStart).</span></span>

> [!NOTE]
> <span data-ttu-id="7d176-131">语法树类型使用继承描述不同的语法元素，这些语法元素在程序中的不同位置生效。</span><span class="sxs-lookup"><span data-stu-id="7d176-131">The Syntax Tree types use inheritance to describe the different syntax elements that are valid at different locations in the program.</span></span> <span data-ttu-id="7d176-132">使用这些 API 通常意味着将属性或集合成员强制转换为特定的派生类型。</span><span class="sxs-lookup"><span data-stu-id="7d176-132">Using these APIs often means casting properties or collection members to specific derived types.</span></span> <span data-ttu-id="7d176-133">在以下示例中，作业和强制转换分别是独立的语句，采用显式类型化变量。</span><span class="sxs-lookup"><span data-stu-id="7d176-133">In the following examples, the assignment and the casts are separate statements, using explicitly typed variables.</span></span> <span data-ttu-id="7d176-134">你可以读取代码以查看 API 的返回类型以及所返回对象的运行时类型。</span><span class="sxs-lookup"><span data-stu-id="7d176-134">You can read the code to see the return types of the API and the runtime type of the objects returned.</span></span> <span data-ttu-id="7d176-135">在实践中，更常见的是使用隐式类型化变量并靠 API 名称来描述要检查的对象的类型。</span><span class="sxs-lookup"><span data-stu-id="7d176-135">In practice, it's more common to use implicitly typed variables and rely on API names to describe the type of objects being examined.</span></span>

<span data-ttu-id="7d176-136">新建 C#“独立代码分析工具”项目：</span><span class="sxs-lookup"><span data-stu-id="7d176-136">Create a new C# **Stand-Alone Code Analysis Tool** project:</span></span>

* <span data-ttu-id="7d176-137">在 Visual Studio 中，选择“文件” > “新建” > “项目”，显示新建项目对话框。</span><span class="sxs-lookup"><span data-stu-id="7d176-137">In Visual Studio, choose **File** > **New** > **Project** to display the New Project dialog.</span></span>
* <span data-ttu-id="7d176-138">在“Visual C#” > “扩展性”下，选择“独立代码分析工具”。</span><span class="sxs-lookup"><span data-stu-id="7d176-138">Under **Visual C#** > **Extensibility**, choose **Stand-Alone Code Analysis Tool**.</span></span>
* <span data-ttu-id="7d176-139">将项目命名为“SemanticQuickStart”并单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="7d176-139">Name your project "**SemanticQuickStart**" and click OK.</span></span>

<span data-ttu-id="7d176-140">你将分析上面展示过的基本“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="7d176-140">You're going to analyze the basic "Hello World!"</span></span> <span data-ttu-id="7d176-141">程序。</span><span class="sxs-lookup"><span data-stu-id="7d176-141">program shown earlier.</span></span>
<span data-ttu-id="7d176-142">为 Hello World 程序添加文本，作为 `Program` 类中的常量：</span><span class="sxs-lookup"><span data-stu-id="7d176-142">Add the text for the Hello World program as a constant in your `Program` class:</span></span>

[!code-csharp[Declare the program test](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#1 "Declare a constant string for the program text to analyze")]

<span data-ttu-id="7d176-143">下一步，添加以下代码，为 `programText` 常量中的代码文本生成语法树。</span><span class="sxs-lookup"><span data-stu-id="7d176-143">Next, add the following code to build the syntax tree for the code text in the `programText` constant.</span></span>  <span data-ttu-id="7d176-144">将下面这行代码添加到 `Main` 方法中：</span><span class="sxs-lookup"><span data-stu-id="7d176-144">Add the following line to your `Main` method:</span></span>

[!code-csharp[Create the tree](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#2 "Create the syntax tree")]

<span data-ttu-id="7d176-145">接下来，从已创建的树生成 <xref:Microsoft.CodeAnalysis.CSharp.CSharpCompilation>。</span><span class="sxs-lookup"><span data-stu-id="7d176-145">Next, build a <xref:Microsoft.CodeAnalysis.CSharp.CSharpCompilation> from the tree you already created.</span></span> <span data-ttu-id="7d176-146">“Hello World”示例依赖于 <xref:System.String> 和 <xref:System.Console> 类型。</span><span class="sxs-lookup"><span data-stu-id="7d176-146">The "Hello World" sample relies on the <xref:System.String> and <xref:System.Console> types.</span></span> <span data-ttu-id="7d176-147">需要引用在编译中声明这两种类型的程序集。</span><span class="sxs-lookup"><span data-stu-id="7d176-147">You need to reference the assembly that declares those two types in your compilation.</span></span> <span data-ttu-id="7d176-148">将下面这行代码添加到 `Main` 方法以创建语法树的编译，包括对相应程序集的引用：</span><span class="sxs-lookup"><span data-stu-id="7d176-148">Add the following line to your `Main` method to create a compilation of your syntax tree, including the reference to the appropriate assembly:</span></span>

[!code-csharp[Create the compilation](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#3 "Create the compilation for the semantic model")]

<span data-ttu-id="7d176-149"><xref:Microsoft.CodeAnalysis.CSharp.CSharpCompilation.AddReferences%2A?displayProperty=nameWithType> 方法将引用添加到编译。</span><span class="sxs-lookup"><span data-stu-id="7d176-149">The <xref:Microsoft.CodeAnalysis.CSharp.CSharpCompilation.AddReferences%2A?displayProperty=nameWithType> method adds references to the compilation.</span></span> <span data-ttu-id="7d176-150"><xref:Microsoft.CodeAnalysis.MetadataReference.CreateFromFile(System.String,Microsoft.CodeAnalysis.MetadataReferenceProperties,Microsoft.CodeAnalysis.DocumentationProvider)> 方法加载程序集作为引用。</span><span class="sxs-lookup"><span data-stu-id="7d176-150">The <xref:Microsoft.CodeAnalysis.MetadataReference.CreateFromFile(System.String,Microsoft.CodeAnalysis.MetadataReferenceProperties,Microsoft.CodeAnalysis.DocumentationProvider)> method loads an assembly as a reference.</span></span> 

## <a name="querying-the-semantic-model"></a><span data-ttu-id="7d176-151">查询语义模型</span><span class="sxs-lookup"><span data-stu-id="7d176-151">Querying the semantic model</span></span>

<span data-ttu-id="7d176-152">如果有 <xref:Microsoft.CodeAnalysis.Compilation>，你可以向它查询 <xref:Microsoft.CodeAnalysis.Compilation> 所包含的任何 <xref:Microsoft.CodeAnalysis.SyntaxTree> 的 <xref:Microsoft.CodeAnalysis.SemanticModel>。</span><span class="sxs-lookup"><span data-stu-id="7d176-152">Once you have a <xref:Microsoft.CodeAnalysis.Compilation> you can ask it for a <xref:Microsoft.CodeAnalysis.SemanticModel> for any <xref:Microsoft.CodeAnalysis.SyntaxTree> contained in that <xref:Microsoft.CodeAnalysis.Compilation>.</span></span> <span data-ttu-id="7d176-153">你可将语义模型看作通常从智能感知中获取的所有信息的来源。</span><span class="sxs-lookup"><span data-stu-id="7d176-153">You can think of the semantic model as the source for all the information would normally get from intellisense.</span></span> <span data-ttu-id="7d176-154"><xref:Microsoft.CodeAnalysis.SemanticModel> 可以回答类似“在此位置有哪些名称在范围内？”的问题</span><span class="sxs-lookup"><span data-stu-id="7d176-154">A <xref:Microsoft.CodeAnalysis.SemanticModel> can answer questions like "What names are in scope at this location?"</span></span> <span data-ttu-id="7d176-155">“通过此方法可以访问哪些成员？”</span><span class="sxs-lookup"><span data-stu-id="7d176-155">"What members are accessible from this method?"</span></span> <span data-ttu-id="7d176-156">“此程序块或文本中使用了什么变量？”</span><span class="sxs-lookup"><span data-stu-id="7d176-156">"What variables are used in this block of text?"</span></span> <span data-ttu-id="7d176-157">以及“这个名称/表达式指的是什么？”</span><span class="sxs-lookup"><span data-stu-id="7d176-157">and "What does this name/expression refer to?"</span></span> <span data-ttu-id="7d176-158">添加此声明以创建语义模型：</span><span class="sxs-lookup"><span data-stu-id="7d176-158">Add this statement to create the semantic model:</span></span>

[!code-csharp[Create the semantic model](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#4 "Create the semantic model")]

## <a name="binding-a-name"></a><span data-ttu-id="7d176-159">绑定名称</span><span class="sxs-lookup"><span data-stu-id="7d176-159">Binding a name</span></span>

<span data-ttu-id="7d176-160"><xref:Microsoft.CodeAnalysis.Compilation> 从 <xref:Microsoft.CodeAnalysis.SyntaxTree> 创建 <xref:Microsoft.CodeAnalysis.SemanticModel></span><span class="sxs-lookup"><span data-stu-id="7d176-160">The <xref:Microsoft.CodeAnalysis.Compilation> creates the  <xref:Microsoft.CodeAnalysis.SemanticModel> from the <xref:Microsoft.CodeAnalysis.SyntaxTree>.</span></span> <span data-ttu-id="7d176-161">创建模型后，你可以查询以找到第一个 `using` 指令，并检索 `System` 命名空间的符号信息。</span><span class="sxs-lookup"><span data-stu-id="7d176-161">After creating the model, you can query it to find the first `using` directive, and retrieve the symbol information for the `System` namespace.</span></span> <span data-ttu-id="7d176-162">将这两行代码添加到 `Main` 方法以创建语义模型，并检索第一个 using 语句的符号：</span><span class="sxs-lookup"><span data-stu-id="7d176-162">Add these two lines to your `Main` method to create the semantic model and retrieve the symbol for the first using statement:</span></span>

[!code-csharp[Find the namespace symbol for the first using](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#5 "Find the namespace symbol for the first using")]

<span data-ttu-id="7d176-163">上述代码显示了如何获取 HelloWorld <xref:Microsoft.CodeAnalysis.SyntaxTree> 的 <xref:Microsoft.CodeAnalysis.SemanticModel> 对象。</span><span class="sxs-lookup"><span data-stu-id="7d176-163">The preceding code shows how to obtain a <xref:Microsoft.CodeAnalysis.SemanticModel> object for your HelloWorld <xref:Microsoft.CodeAnalysis.SyntaxTree>.</span></span> <span data-ttu-id="7d176-164">获取模型以后，绑定第一个 `using` 指令中的名称以检索 `System` 命名空间的 <xref:Microsoft.CodeAnalysis.SymbolInfo?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7d176-164">Once the model is obtained, the name in the first `using` directive is bound to retrieve a <xref:Microsoft.CodeAnalysis.SymbolInfo?displayProperty=nameWithType> for the `System` namespace.</span></span> <span data-ttu-id="7d176-165">上述代码还说明，使用语法模型查找代码的结构；使用语义模型理解它的含义。</span><span class="sxs-lookup"><span data-stu-id="7d176-165">The preceding code also illustrates that you use the **syntax model** to find the structure of the code; you use the **semantic model** to understand its meaning.</span></span> <span data-ttu-id="7d176-166">语法模型在 using 语句中找到字符串 `System`。</span><span class="sxs-lookup"><span data-stu-id="7d176-166">The **syntax model** finds the string `System` in the using statement.</span></span> <span data-ttu-id="7d176-167">语义模型具有关于 `System` 命名空间中所定义类型的全部信息。</span><span class="sxs-lookup"><span data-stu-id="7d176-167">The **semantic model** has all the information about the types defined in the `System` namespace.</span></span>

<span data-ttu-id="7d176-168">可以从 <xref:Microsoft.CodeAnalysis.SymbolInfo> 对象获取使用 <xref:Microsoft.CodeAnalysis.SymbolInfo.Symbol?displayProperty=nameWithType> 属性的 <xref:Microsoft.CodeAnalysis.ISymbol?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7d176-168">From the <xref:Microsoft.CodeAnalysis.SymbolInfo> object you can obtain the <xref:Microsoft.CodeAnalysis.ISymbol?displayProperty=nameWithType> using the <xref:Microsoft.CodeAnalysis.SymbolInfo.Symbol?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="7d176-169">此属性返回此表达式所引用的符号。</span><span class="sxs-lookup"><span data-stu-id="7d176-169">This property returns the symbol this expression refers to.</span></span> <span data-ttu-id="7d176-170">对于不引用任何内容的表达式（例如数字参数），此属性为 `null`。</span><span class="sxs-lookup"><span data-stu-id="7d176-170">For expressions that don't refer to anything (such as numeric literals) this property is `null`.</span></span> <span data-ttu-id="7d176-171">若 <xref:Microsoft.CodeAnalysis.SymbolInfo.Symbol?displayProperty=nameWithType> 不为 null，<xref:Microsoft.CodeAnalysis.ISymbol.Kind?displayProperty=nameWithType> 表示符号的类型。</span><span class="sxs-lookup"><span data-stu-id="7d176-171">When the <xref:Microsoft.CodeAnalysis.SymbolInfo.Symbol?displayProperty=nameWithType> is not null, the <xref:Microsoft.CodeAnalysis.ISymbol.Kind?displayProperty=nameWithType> denotes the type of the symbol.</span></span> <span data-ttu-id="7d176-172">在此示例中，<xref:Microsoft.CodeAnalysis.ISymbol.Kind?displayProperty=nameWithType> 属性是 <xref:Microsoft.CodeAnalysis.SymbolKind.Namespace?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="7d176-172">In this example, the <xref:Microsoft.CodeAnalysis.ISymbol.Kind?displayProperty=nameWithType> property is a <xref:Microsoft.CodeAnalysis.SymbolKind.Namespace?displayProperty=nameWithType>.</span></span> <span data-ttu-id="7d176-173">将以下代码添加到 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="7d176-173">Add the following code to your `Main` method.</span></span> <span data-ttu-id="7d176-174">它检索 `System` 命名空间的符号，然后将 `System` 命名空间中声明的所有子命名空间显示出来：</span><span class="sxs-lookup"><span data-stu-id="7d176-174">It retrieves the symbol for the `System` namespace and then displays all the child namespaces declared in the `System` namespace:</span></span>

[!code-csharp[Display all the child namespaces](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#6 "Display all the child namespaces from this compilation")]

<span data-ttu-id="7d176-175">运行该程序，然后应看到以下输出：</span><span class="sxs-lookup"><span data-stu-id="7d176-175">Run the program and you should see the following output:</span></span>

```
Collections
Configuration
Deployment
Diagnostics
Globalization
IO
Reflection
Resources
Runtime
Security
StubHelpers
Text
Threading
Press any key to continue . . .
```

> [!NOTE]
> <span data-ttu-id="7d176-176">该输出不包含 `System` 命名空间的每个子命名空间。</span><span class="sxs-lookup"><span data-stu-id="7d176-176">The output does not include every namespace that is a child namespace of the `System` namespace.</span></span> <span data-ttu-id="7d176-177">它显示此编译中存在的每个命名空间，只引用声明了 `System.String` 的程序集。</span><span class="sxs-lookup"><span data-stu-id="7d176-177">It displays every namespace that is present in this compilation, which only references the assembly where `System.String` is declared.</span></span> <span data-ttu-id="7d176-178">此编译不了解其他程序集中所声明的任何命名空间</span><span class="sxs-lookup"><span data-stu-id="7d176-178">Any namespaces declared in other assemblies are not known to this compilation</span></span>

### <a name="binding-an-expression"></a><span data-ttu-id="7d176-179">绑定表达式</span><span class="sxs-lookup"><span data-stu-id="7d176-179">Binding an expression</span></span>

<span data-ttu-id="7d176-180">上述代码显示如何通过绑定到名称来查找符号。</span><span class="sxs-lookup"><span data-stu-id="7d176-180">The preceding code shows how to find a symbol by binding to a name.</span></span> <span data-ttu-id="7d176-181">在可以绑定的 C# 程序中还有其他不是名称的表达式。</span><span class="sxs-lookup"><span data-stu-id="7d176-181">There are other expressions in a C# program that can be bound that aren't names.</span></span> <span data-ttu-id="7d176-182">为演示此功能，我们绑定到简单的字符串文本。</span><span class="sxs-lookup"><span data-stu-id="7d176-182">To demonstrate this capability, let's access the binding to a simple string literal.</span></span>

<span data-ttu-id="7d176-183">“Hello World”程序包含一个 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.LiteralExpressionSyntax?displayProperty=nameWithType>，即“Hello, World!”</span><span class="sxs-lookup"><span data-stu-id="7d176-183">The "Hello World" program contains a <xref:Microsoft.CodeAnalysis.CSharp.Syntax.LiteralExpressionSyntax?displayProperty=nameWithType>, the "Hello, World!"</span></span> <span data-ttu-id="7d176-184">向控制台显示的字符串。</span><span class="sxs-lookup"><span data-stu-id="7d176-184">string displayed to the console.</span></span>

<span data-ttu-id="7d176-185">通过找到程序中的单个字符串文本</span><span class="sxs-lookup"><span data-stu-id="7d176-185">You find the "Hello, World!"</span></span> <span data-ttu-id="7d176-186">查找到“Hello World!”字符串。</span><span class="sxs-lookup"><span data-stu-id="7d176-186">string by locating the single string literal in the program.</span></span> <span data-ttu-id="7d176-187">找到语法节点后，从语义模型中获取该节点的类型信息。</span><span class="sxs-lookup"><span data-stu-id="7d176-187">Then, once you've located the syntax node, get the type info for that node from the semantic model.</span></span> <span data-ttu-id="7d176-188">将以下代码添加到 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="7d176-188">Add the following code to your `Main` method:</span></span>

[!code-csharp[Find the namespace symbol for the only using](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#7 "Find the namespace symbol for the only using")]

<span data-ttu-id="7d176-189"><xref:Microsoft.CodeAnalysis.TypeInfo?displayProperty=nameWithType> 结构包括 <xref:Microsoft.CodeAnalysis.TypeInfo.Type?displayProperty=nameWithType> 属性，此属性可启用对关于文本类型的语义信息的访问。</span><span class="sxs-lookup"><span data-stu-id="7d176-189">The <xref:Microsoft.CodeAnalysis.TypeInfo?displayProperty=nameWithType> struct includes a <xref:Microsoft.CodeAnalysis.TypeInfo.Type?displayProperty=nameWithType> property that enables access to the semantic information about the type of the literal.</span></span> <span data-ttu-id="7d176-190">在此例中为 `string` 类型。</span><span class="sxs-lookup"><span data-stu-id="7d176-190">In this example, that's the `string` type.</span></span> <span data-ttu-id="7d176-191">添加将此属性分配至本地变量的声明：</span><span class="sxs-lookup"><span data-stu-id="7d176-191">Add a declaration that assigns this property to a local variable:</span></span>

[!code-csharp[Find the semantic information about the string type](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#8 "Use the string literal to access the semantic information in the string type.")]

<span data-ttu-id="7d176-192">要完成本教程，让我们生成 LINQ 查询，该查询会创建一个在 `string` 类型上声明并返回 `string` 的所有公共方法的序列。</span><span class="sxs-lookup"><span data-stu-id="7d176-192">To finish this tutorial, let's build a LINQ query that creates a sequence of all the public methods declared on the `string` type that return a `string`.</span></span> <span data-ttu-id="7d176-193">此查询比较复杂，我们将逐行生成，然后将其重新构造为单个查询。</span><span class="sxs-lookup"><span data-stu-id="7d176-193">This query gets complex, so let's build it line by line, then reconstruct it as a single query.</span></span> <span data-ttu-id="7d176-194">此查询的源是 `string` 类型上所声明全部成员的序列：</span><span class="sxs-lookup"><span data-stu-id="7d176-194">The source for this query is the sequence of all members declared on the `string` type:</span></span>

[!code-csharp[Access the sequence of members on the string type](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#9 "Access the sequence of members on the string type.")]

<span data-ttu-id="7d176-195">该源序列包含所有成员（包括属性和字段），使用 <xref:System.Collections.Immutable.ImmutableArray%601.OfType%2A?displayProperty=nameWithType> 方法对其进行筛选以查找属于 <xref:Microsoft.CodeAnalysis.IMethodSymbol?diplayProperty=nameWithType> 对象的元素：</span><span class="sxs-lookup"><span data-stu-id="7d176-195">That source sequence conatins all members, including properties and fields, so filter it using the <xref:System.Collections.Immutable.ImmutableArray%601.OfType%2A?displayProperty=nameWithType> method to find elements that are <xref:Microsoft.CodeAnalysis.IMethodSymbol?diplayProperty=nameWithType> objects:</span></span>

[!code-csharp[Filter the sequence to only methods](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#10 "Find the subset of the collection that is the methods.")]

<span data-ttu-id="7d176-196">接下来，添加另一个筛选器，只返回这些属于公共方法并返回 `string` 的方法：</span><span class="sxs-lookup"><span data-stu-id="7d176-196">Next, add another filter to return only those methods that are public and return a `string`:</span></span>

[!code-csharp[Filter on return type and accessibility](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#11 "Find only the public methods that return a string.")]

<span data-ttu-id="7d176-197">只选择名称属性，且只通过删除任何重载来区分名称：</span><span class="sxs-lookup"><span data-stu-id="7d176-197">Select only the name property, and only distinct names by removing any overloads:</span></span>

[!code-csharp[find the distinct names.](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#12 "Use the string literal to access the semantic information in the string type.")]

<span data-ttu-id="7d176-198">还可以使用 LINQ 查询语法生成完整查询，然后在控制台中显示所有方法名称：</span><span class="sxs-lookup"><span data-stu-id="7d176-198">You can also build the full query using the LINQ query syntax, and then display all the method names in  the console:</span></span>

[!code-csharp[build and display the results of this query.](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/SemanticQuickStart/Program.cs#12 "Build and display the results of the query.")]

<span data-ttu-id="7d176-199">生成并运行该程序。</span><span class="sxs-lookup"><span data-stu-id="7d176-199">Build and run the program.</span></span> <span data-ttu-id="7d176-200">您应看到以下输出：</span><span class="sxs-lookup"><span data-stu-id="7d176-200">You should see the following output:</span></span>

```
Join
Substring
Trim
TrimStart
TrimEnd
Normalize
PadLeft
PadRight
ToLower
ToLowerInvariant
ToUpper
ToUpperInvariant
ToString
Insert
Replace
Remove
Format
Copy
Concat
Intern
IsInterned
Press any key to continue . . .
```
<span data-ttu-id="7d176-201">你已使用语义 API 来查找并显示关于属于此程序的符号的信息。</span><span class="sxs-lookup"><span data-stu-id="7d176-201">You've used the Semantic API to find and display information about the symbols that are part of this program.</span></span>