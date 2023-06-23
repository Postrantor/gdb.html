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

Note that before the debugged program has started execution, no DLLs will have been loaded. The easiest way around this problem is simply to start the program --- either by setting a breakpoint or letting the program run once to completion.

#### 21.1.4.2 DLL Name Prefixes

In keeping with the naming conventions used by the Microsoft debugging tools, DLL export symbols are made available with a prefix based on the DLL name, for instance `KERNEL32!CreateFileA`. The plain name is also entered into the symbol table, so `CreateFileA` is often sufficient. In some cases there will be name clashes within a program (particularly if the executable itself includes full debugging symbols) necessitating the use of the fully qualified name when referring to the contents of the DLL. Use single-quotes around the name to avoid the exclamation mark ("!") being interpreted as a language operator.

Note that the internal name of the DLL may be all upper-case, even though the file name of the DLL is lower-case, or vice-versa. Since symbols within [GDB] are *case-sensitive* this may cause some confusion. If in doubt, try the `info functions` and `info variables` commands or even `maint print msymbols` (see [Symbols](Symbols.html#Symbols)). Here's an example:

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

Variables are generally treated as pointers and dereferenced automatically. For this reason, it is often necessary to prefix a variable name with the address-of operator ("&") and provide explicit type information in the command. Here's an example of the type of problem:

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

::: smallexample

```bash
(gdb) break *&'python22!PyOS_Readline'
Breakpoint 1 at 0x1e04eff0
```

:::

The author of these extensions is not entirely convinced that setting a break point within a shared DLL like `kernel32.dll` is completely safe.

---

::: header
Up: [Cygwin Native](Cygwin-Native.html#Cygwin-Native)]
:::
