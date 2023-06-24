---
tip: translate by openai@2023-06-23 18:45:57
...
---
description: C Plus Plus Expressions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: C Plus Plus Expressions (Debugging with GDB)
lang: en
resource-type: document
title: C Plus Plus Expressions (Debugging with GDB)
---
::: header
Next: [C Defaults](C-Defaults.html#C-Defaults)]
:::

---

#### 15.4.1.3 C++ Expressions


[GDB] expression handling can interpret most C++ expressions.

> [GDB]处理表达式可以解释大多数C++表达式。

> *Warning:* [GDB] to debug C++ code. See [Compilation](Compilation.html#Compilation).


1. Member function calls are allowed; you can use expressions like

> 1. 允许调用成员函数；您可以使用类似表达式

::: smallexample

```bash
count = aml->GetOriginal(x, y)
```

:::
2. .

3.  does not perform overload resolution involving user-defined type conversions, calls to constructors, or instantiations of templates that do not exist in the program. It also cannot handle ellipsis argument lists or default arguments.

> 3.  不会执行涉及用户定义类型转换、构造函数调用或不存在于程序中的模板实例化的过载决策。它也无法处理省略号参数列表或默认参数。


It does perform integral conversions and promotions, floating-point promotions, arithmetic conversions, pointer conversions, conversions of class objects to base classes, and standard conversions such as those of functions or arrays to pointers; it requires an exact match on the number of function arguments.

> 它可以执行整数转换和提升，浮点提升，算术转换，指针转换，类对象到基类的转换，以及像函数或数组到指针的标准转换；它需要函数参数的完全匹配。


Overload resolution is always performed, unless you have specified `set overload-resolution off`. See [[GDB] Features for C++](Debugging-C-Plus-Plus.html#Debugging-C-Plus-Plus).

> 调用解析总是会执行，除非您指定 `set overload-resolution off`。详见[[GDB] C++ 特性](Debugging-C-Plus-Plus.html#Debugging-C-Plus-Plus)。


You must specify `set overload-resolution off` in order to use an explicit function signature to call an overloaded function, as in

> 必须指定`set overload-resolution off`，才能使用显式函数签名调用重载函数，例如

::: smallexample

```bash
p 'foo(char,int)'('x', 13)
```

:::


The [GDB] command-completion facility can simplify this; see [Command Completion](Completion.html#Completion).

> 命令补全功能可以简化这个过程；请参见[命令补全](Completion.html#Completion)。

4.  understands variables declared as C++ lvalue or rvalue references; you can use them in expressions just as you do in C++ source---they are automatically dereferenced.

> 4.能够理解C++中声明的lvalue或rvalue引用；您可以像在C++源代码中一样在表达式中使用它们——它们会自动解引用。


In the parameter list shown when [GDB]'.

> 在[GDB]显示的参数列表中。

5. [GDB] also allows resolving name scope by reference to source files, in both C and C++ debugging (see [Program Variables](Variables.html#Variables)).

> GDB也允许通过参考源文件来解析C和C++调试中的名称范围（参见[程序变量](Variables.html#Variables)）。

6. [GDB] performs argument-dependent lookup, following the C++ specification.

> GDB遵循C++规范，执行参数依赖查找。

---

::: header
Next: [C Defaults](C-Defaults.html#C-Defaults)]
:::
