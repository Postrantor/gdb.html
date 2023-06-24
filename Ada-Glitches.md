---
tip: translate by openai@2023-06-23 16:57:30
...
---
description: Ada Glitches (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Glitches (Debugging with GDB)
lang: en
resource-type: document
title: Ada Glitches (Debugging with GDB)
---
::: header
Previous: [Ada Source Character Set](Ada-Source-Character-Set.html#Ada-Source-Character-Set)]
:::

---

#### 15.4.10.11 Known Peculiarities of Ada Mode


Besides the omissions listed previously (see [Omissions from Ada](Omissions-from-Ada.html#Omissions-from-Ada)), we know of several problems with and limitations of Ada mode in [GDB], some of which will be fixed with planned future releases of the debugger and the GNU Ada compiler.

> 除了前面列出的遗漏（参见[Ada的遗漏] (Omissions-from-Ada.html#Omissions-from-Ada)）外，我们还知道[GDB]中Ada模式存在的一些问题和限制，其中一些将通过调试器和GNU Ada编译器的计划未来版本来解决。


- Static constants that the compiler chooses not to materialize as objects in storage are invisible to the debugger.

> 编译器选择不将静态常量作为存储中的对象材料化的常量对调试器来说是不可见的。

- Named parameter associations in function argument lists are ignored (the argument lists are treated as positional).

> 函数参数列表中的命名参数关联会被忽略（参数列表被当作位置参数处理）。
- Many useful library packages are currently invisible to the debugger.

- Fixed-point arithmetic, conversions, input, and output is carried out using floating-point arithmetic, and may give results that only approximate those on the host machine.

> 固定点算术、转换、输入和输出使用浮点算术进行，可能会给出只接近主机机器上结果的结果。

- The GNAT compiler never generates the prefix `Standard` for any of the standard symbols defined by the Ada language. [GDB] knows about this: it will strip the prefix from names when you use it, and will never look for a name you have so qualified among local symbols, nor match against symbols in other packages or subprograms. If you have defined entities anywhere in your program other than parameters and local variables whose simple names match names in `Standard`, GNAT's lack of qualification here can cause confusion. When this happens, you can usually resolve the confusion by qualifying the problematic names with package `Standard` explicitly.

> GNAT 编译器从不为 Ada 语言定义的标准符号生成前缀'Standard'。GDB 知道这一点：当您使用它时，它会从名称中清除前缀，永远不会在本地符号中查找您已经指定的名称，也不会与其他包或子程序中的符号匹配。如果您在程序中定义的实体（除了参数和局部变量）的简单名称与`Standard`中的名称相匹配，GNAT 在此处缺乏限定可能会引起混乱。当发生这种情况时，通常可以通过显式限定问题名称与包`Standard`来解决混乱。


Older versions of the compiler sometimes generate erroneous debugging information, resulting in the debugger incorrectly printing the value of affected entities. In some cases, the debugger is able to work around an issue automatically. In other cases, the debugger is able to work around the issue, but the work-around has to be specifically enabled.

> 旧版本的编译器有时会生成错误的调试信息，导致调试器错误地打印受影响实体的值。在某些情况下，调试器能够自动解决问题。在其他情况下，调试器可以解决问题，但必须特别启用解决方案。

`set ada trust-PAD-over-XVS on`


:   Configure GDB to strictly follow the GNAT encoding when computing the value of Ada entities, particularly when `PAD` and `PAD___XVS` types are involved (see `ada/exp_dbug.ads` in the GCC sources for a complete description of the encoding used by the GNAT compiler). This is the default.

> 配置GDB严格遵循GNAT编码计算Ada实体的值，特别是当涉及`PAD`和`PAD___XVS`类型时（有关GNAT编译器使用的编码的完整描述，请参见GCC源中的`ada/exp_dbug.ads`）。这是默认设置。

`set ada trust-PAD-over-XVS off`


:   This is related to the encoding using by the GNAT compiler. If [GDB] sometimes prints the wrong value for certain entities, changing `ada trust-PAD-over-XVS` to `off` activates a work-around which may fix the issue. It is always safe to set `ada trust-PAD-over-XVS` to `off`, but this incurs a slight performance penalty, so it is recommended to leave this setting to `on` unless necessary.

> 这与GNAT编译器使用的编码有关。如果[GDB]有时会为某些实体打印错误的值，将`ada trust-PAD-over-XVS`更改为`off`可以激活一种可能解决该问题的解决方案。将`ada trust-PAD-over-XVS`设置为`off`总是安全的，但这会导致性能略有降低，因此除非必要，否则建议将此设置保留为`on`。


Internally, the debugger also relies on the compiler following a number of conventions known as the '`GNAT Encoding` in the GCC sources. This encoding describes how the debugging information should be generated for certain types. In particular, this convention makes use of *descriptive types*, which are artificial types generated purely to help the debugger.

> 调试器内部也依赖于编译器遵循GCC源代码中称为'GNAT Encoding'的一系列约定。这种编码描述了为某些类型生成调试信息的方式。特别是，该约定使用描述性类型，这些类型是纯粹用于帮助调试器的人工类型。


These encodings were defined at a time when the debugging information format used was not powerful enough to describe some of the more complex types available in Ada. Since DWARF allows us to express nearly all Ada features, the long-term goal is to slowly replace these descriptive types by their pure DWARF equivalent. To facilitate that transition, a new maintenance option is available to force the debugger to ignore those descriptive types. It allows the user to quickly evaluate how well [GDB] works without them.

> 这些编码是在调试信息格式不足以描述Ada可用的更复杂类型时定义的。由于DWARF允许我们表达几乎所有Ada特性，长期目标是逐步用它们的纯DWARF等价物替换这些描述性类型。为了促进这种过渡，新的维护选项可用于强制调试器忽略这些描述性类型。它允许用户快速评估[GDB]在没有它们时的工作效果。

`maintenance ada set ignore-descriptive-types [on|off]`


Control whether the debugger should ignore descriptive types. The default is not to ignore descriptives types (`off`).

> 控制调试器是否应该忽略描述性类型。默认不忽略描述性类型（`关闭`）。

`maintenance ada show ignore-descriptive-types`


Show if descriptive types are ignored by [GDB].

> 查看[GDB]是否忽略描述性类型。

---

::: header
Previous: [Ada Source Character Set](Ada-Source-Character-Set.html#Ada-Source-Character-Set)]
:::
