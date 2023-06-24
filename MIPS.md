---
tip: translate by openai@2023-06-24 00:23:56
...
---
description: MIPS (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: MIPS (Debugging with GDB)
lang: en
resource-type: document
title: MIPS (Debugging with GDB)
---
::: header
Next: [HPPA](HPPA.html#HPPA)]
:::

---

#### 21.4.4 MIPS


Alpha- and MIPS-based computers use an unusual stack frame, which sometimes requires [GDB] to search backward in the object code to find the beginning of a function.

> α和MIPS基础计算机使用一种不寻常的堆栈框架，有时需要[GDB]在对象代码中向后搜索以找到函数的开头。


To improve response time (especially for embedded applications, where [GDB] may be restricted to a slow serial line for this search) you may want to limit the size of this search, using one of these commands:

> 为了提高响应时间（尤其是对于使用[GDB]进行搜索的嵌入式应用程序，其可能受限于缓慢的串行线路），您可能希望限制此搜索的大小，使用以下命令之一：

`set heuristic-fence-post limit`


Restrict [GDB], the larger the limit the more bytes `heuristic-fence-post` must search and therefore the longer it takes to run. You should only need to use this command when debugging a stripped executable.

> 限制GDB，限制越大，heuristic-fence-post必须搜索的字节越多，因此运行时间越长。只有在调试剥离可执行文件时，才需要使用此命令。

`show heuristic-fence-post`

Display the current limit.


These commands are available *only* when [GDB] is configured for debugging programs on Alpha or MIPS processors.

> 这些命令仅在配置用于调试Alpha或MIPS处理器上的程序时才可用。


Several MIPS-specific commands are available when debugging MIPS programs:

> 有几个专门用于调试MIPS程序的MIPS命令可供使用。

`set mips abi arg`

Tell [GDB] are:

'`auto`'

The default ABI associated with the current binary (this is the default).

'`o32`'

'`o64`'

'`n32`'

'`n64`'

'`eabi32`'

'`eabi64`'

`show mips abi`

Show the MIPS ABI used by [GDB] to debug the inferior.

`set mips compression arg`


Tell [GDB] uses this for code disassembly and other internal interpretation purposes. This setting is only referred to when no executable has been associated with the debugging session or the executable does not provide information about the encoding it uses. Otherwise this setting is automatically updated from information provided by the executable.

> 告诉GDB使用这个进行代码反汇编和其他内部解释用途。除非没有与调试会话关联的可执行文件或者可执行文件没有提供有关其使用的编码的信息，否则此设置将自动从可执行文件提供的信息更新。


Possible values of `arg`', as executables containing MIPS16 code frequently are not identified as such.

> 可能的arg值，因为包含MIPS16代码的可执行文件通常不被识别为此类文件。


This setting is "sticky"; that is, it retains its value across debugging sessions until reset either explicitly with this command or implicitly from an executable.

> 这个设置是“粘性”的；也就是说，它在调试会话之间保持其值，直到通过此命令显式重置或从可执行文件隐式重置。


The compiler and/or assembler typically add symbol table annotations to identify functions compiled for the MIPS16 or microMIPS ISAs. If these function-scope annotations are present, [GDB] uses them in preference to the global compressed ISA encoding setting.

> 编译器和/或汇编器通常会添加符号表注释来标识为MIPS16或microMIPS ISAs编译的函数。如果存在这些函数作用域注释，[GDB]会优先使用它们，而不是全局压缩ISA编码设置。

`show mips compression`


Show the MIPS compressed ISA encoding used by [GDB] to debug the inferior.

> 请帮助我翻译，“显示[GDB]用于调试下级的MIPS压缩ISA编码。”为“简体中文”

`set mipsfpu`

`show mipsfpu`

See [set mipsfpu](MIPS-Embedded.html#MIPS-Embedded).

`set mips mask-address arg`


This command determines whether the most-significant 32 bits of 64-bit MIPS addresses are masked off. The argument `arg` determine the correct value.

> 这个命令确定64位MIPS地址的最高32位是否被屏蔽。参数`arg`确定正确的值。

`show mips mask-address`

Show whether the upper 32 bits of MIPS addresses are masked off or not.

`set remote-mips64-transfers-32bit-regs`


This command controls compatibility with 64-bit MIPS targets that transfer data in 32-bit quantities. If you have an old MIPS 64 target that transfers 32 bits for some registers, like [SR]'.

> 这个命令控制与64位MIPS目标的兼容性，它们以32位数量传输数据。如果你有一个旧的MIPS 64目标，它会为某些寄存器传输32位，比如[SR]。

`show remote-mips64-transfers-32bit-regs`

Show the current setting of compatibility with older MIPS 64 targets.

`set debug mips`


This command turns on and off debugging messages for the MIPS-specific target code in [GDB].

> 这个命令用于在[GDB]中开启和关闭MIPS特定目标代码的调试消息。

`show debug mips`

Show the current setting of MIPS debugging messages.

---

::: header
Next: [HPPA](HPPA.html#HPPA)]
:::
