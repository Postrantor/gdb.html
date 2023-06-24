---
tip: translate by openai@2023-06-24 00:32:48
...
---
description: Non-debug DLL Symbols (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Non-debug DLL Symbols (Debugging with GDB)
lang: en
resource-type: document
title: Non-debug DLL Symbols (Debugging with GDB)
---
::: header
Up: [Cygwin Native](Cygwin-Native.html#Cygwin-Native)]
:::

---

#### 21.1.4.1 Support for DLLs without Debugging Symbols


Very often on windows, some of the DLLs that your program relies on do not include symbolic debugging information (for example, `kernel32.dll` as "minimal symbols".

> 很多时候，在Windows上，你的程序依赖的某些DLL不包含符号调试信息（例如，“kernel32.dll”作为“最小符号”）。


Note that before the debugged program has started execution, no DLLs will have been loaded. The easiest way around this problem is simply to start the program --- either by setting a breakpoint or letting the program run once to completion.

> 注意，在调试的程序开始执行之前，没有加载任何DLL。解决这个问题最简单的方法就是开始程序---设置断点或者让程序运行一次到结束。

#### 21.1.4.2 DLL Name Prefixes


In keeping with the naming conventions used by the Microsoft debugging tools, DLL export symbols are made available with a prefix based on the DLL name, for instance `KERNEL32!CreateFileA`. The plain name is also entered into the symbol table, so `CreateFileA` is often sufficient. In some cases there will be name clashes within a program (particularly if the executable itself includes full debugging symbols) necessitating the use of the fully qualified name when referring to the contents of the DLL. Use single-quotes around the name to avoid the exclamation mark ("!") being interpreted as a language operator.

> 按照Microsoft调试工具的命名规则，DLL导出符号以DLL名称为前缀提供，例如'KERNEL32！CreateFileA'。符号表中也会输入简单的名称，因此通常只需要'CreateFileA'。在某些情况下，程序中可能会发生名称冲突（特别是如果可执行文件本身包含完整的调试符号），这时在引用DLL内容时需要使用完全限定的名称。使用单引号括起名称以避免感叹号（“！”）被解释为语言运算符。


Note that the internal name of the DLL may be all upper-case, even though the file name of the DLL is lower-case, or vice-versa. Since symbols within [GDB] are *case-sensitive* this may cause some confusion. If in doubt, try the `info functions` and `info variables` commands or even `maint print msymbols` (see [Symbols](Symbols.html#Symbols)). Here's an example:

> 注意，DLL的内部名称可能全部是大写字母，即使DLL的文件名是小写字母，或者反之亦然。由于[GDB]中的符号是*大小写敏感*的，这可能会引起一些混乱。如果有疑问，请尝试使用`info functions`和`info variables`命令，或者甚至`maint print msymbols`（请参见[Symbols]（Symbols.html#Symbols））。这里有一个例子：

::: smallexample

```bash
(gdb) info function CreateFileA
All functions matching regular expression "CreateFileA":

Non-debugging symbols:
0x77e885f4  CreateFileA
0x77e885f4  KERNEL32!CreateFileA
```

:::

::: smallexample

```bash
(gdb) info function !
All functions matching regular expression "!":

Non-debugging symbols:
0x6100114c  cygwin1!__assert
0x61004034  cygwin1!_dll_crt0@0
0x61004240  cygwin1!dll_crt0(per_process *)
[etc...]
```

:::

#### 21.1.4.3 Working with Minimal Symbols


Symbols extracted from a DLL's export table do not contain very much type information. All that [GDB] can do is guess whether a symbol refers to a function or variable depending on the linker section that contains the symbol. Also note that the actual contents of the memory contained in a DLL are not available unless the program is running. This means that you cannot examine the contents of a variable or disassemble a function within a DLL without a running program.

> 从DLL的导出表中提取的符号不包含太多类型信息。[GDB]所能做的就是猜测一个符号是指函数还是变量，这取决于包含该符号的链接器部分。此外，除非程序正在运行，否则无法访问DLL中存储的实际内容。这意味着，在没有运行程序的情况下，无法检查变量的内容或解析DLL中的函数。


Variables are generally treated as pointers and dereferenced automatically. For this reason, it is often necessary to prefix a variable name with the address-of operator ("&") and provide explicit type information in the command. Here's an example of the type of problem:

> 变量通常被视为指针，并自动解引用。因此，通常需要在命令中使用地址运算符("&")为变量名称加上前缀，并提供明确的类型信息。这里是一个类型问题的示例：

::: smallexample

```bash
(gdb) print 'cygwin1!__argv'
'cygwin1!__argv' has unknown type; cast it to its declared type
```

:::

::: smallexample

```bash
(gdb) x 'cygwin1!__argv'
'cygwin1!__argv' has unknown type; cast it to its declared type
```

:::

And two possible solutions:

::: smallexample

```bash
(gdb) print ((char **)'cygwin1!__argv')[0]
$2 = 0x22fd98 "/cygdrive/c/mydirectory/myprogram"
```

:::

::: smallexample

```bash
(gdb) x/2x &'cygwin1!__argv'
0x610c0aa8 <cygwin1!__argv>:    0x10021608      0x00000000
(gdb) x/x 0x10021608
0x10021608:     0x0022fd98
(gdb) x/s 0x0022fd98
0x22fd98:        "/cygdrive/c/mydirectory/myprogram"
```

:::


Setting a break point within a DLL is possible even before the program starts execution. However, under these circumstances, [GDB] can't examine the initial instructions of the function in order to skip the function's frame set-up code. You can work around this by using "\*&" to set the breakpoint at a raw memory address:

> 在DLL中设置断点是可能的，即使在程序开始执行之前也是如此。但是，在这种情况下，[GDB]无法检查函数的初始指令，以跳过函数的帧设置代码。您可以通过使用“\*＆”在原始内存地址处设置断点来解决此问题：

::: smallexample

```bash
(gdb) break *&'python22!PyOS_Readline'
Breakpoint 1 at 0x1e04eff0
```

:::


The author of these extensions is not entirely convinced that setting a break point within a shared DLL like `kernel32.dll` is completely safe.

> 作者对于在像`kernel32.dll`这样的共享动态链接库中设置断点并不完全确信是安全的。

---

::: header
Up: [Cygwin Native](Cygwin-Native.html#Cygwin-Native)]
:::
