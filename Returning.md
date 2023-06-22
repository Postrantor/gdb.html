---
description: Returning (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Returning (Debugging with GDB)
lang: en
resource-type: document
title: Returning (Debugging with GDB)
---
::: header
Next: [Calling](Calling.html#Calling)]
:::

---

### 17.4 Returning from a Function

`return`

`return expression`

You can cancel execution of a function call with the `return` command. If you give an `expression` argument, its value is used as the function's return value.

When you use `return`, [GDB] discards the selected stack frame (and all frames within it). You can think of this as making the discarded frame return prematurely. If you wish to specify a value to be returned, give that value as the argument to `return`.

This pops the selected stack frame (see [Selecting a Frame](Selection.html#Selection)), and any other frames inside of it, leaving its caller as the innermost remaining frame. That frame becomes selected. The specified value is stored in the registers used for returning values of functions.

The `return` command does not resume execution; it leaves the program stopped in the state that would exist if the function had just returned. In contrast, the `finish` command (see [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping)) resumes execution until the selected stack frame returns naturally.

[GDB] already knows the OS ABI from its current target so it needs to find out also the type being returned to make the assignment into the right register(s).

Normally, the selected stack frame has debug info. [GDB] transparently converts the implicit `int` value of -1 into a `long long int`:

::: smallexample

```bash
Breakpoint 1, func () at gdb.base/return-nodebug.c:29
29        return 31;
(gdb) return -1
Make func return now? (y or n) y
#0  0x004004f6 in main () at gdb.base/return-nodebug.c:43
43        printf ("result=%lld\n", func ());
(gdb)
```

:::

However, if the selected stack frame does not have a debug info, e.g., if the function was compiled without debug info, [GDB] with its implicit type `int` would set only a part of a `long long int` result for a debug info less function (on 32-bit architectures). Therefore the user is required to specify the return type by an appropriate cast explicitly:

::: smallexample

```bash
Breakpoint 2, 0x0040050b in func ()
(gdb) return -1
Return value type not available for selected stack frame.
Please use an explicit cast of the value to return.
(gdb) return (long long int) -1
Make selected stack frame return now? (y or n) y
#0  0x00400526 in main ()
(gdb)
```

:::

---

::: header
Next: [Calling](Calling.html#Calling)]
:::
