---
description: Calling (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Calling (Debugging with GDB)
lang: en
resource-type: document
title: Calling (Debugging with GDB)
---
::: header
Next: [Patching](Patching.html#Patching)]
:::

---

### 17.5 Calling Program Functions

`print expr`

Evaluate the expression `expr` and display the resulting value. The expression may include calls to functions in the program being debugged.

`call expr`

Evaluate the expression `expr` without displaying `void` returned values.

You can use this variant of the `print` command if you want to execute a function from your program that does not return anything (a.k.a. *a void function*), but without cluttering the output with `void` returned values that [GDB] will otherwise print. If the result is not void, it is printed and saved in the value history.

It is possible for the function you call via the `print` or `call` command to generate a signal (e.g., if there's a bug in the function, or if you passed it incorrect arguments). What happens in that case is controlled by the `set unwindonsignal` command.

Similarly, with a C++ program it is possible for the function you call via the `print` or `call` command to generate an exception that is not handled due to the constraints of the dummy frame. In this case, any exception that is raised in the frame, but has an out-of-frame exception handler will not be found. GDB builds a dummy-frame for the inferior function call, and the unwinder cannot seek for exception handlers outside of this dummy-frame. What happens in that case is controlled by the `set unwind-on-terminating-exception` command.

`set unwindonsignal`

:

```
Set unwinding of the stack if a signal is received while in a function that [GDB] stops in the frame where the signal was received.
```

`show unwindonsignal`

:

```
Show the current setting of stack unwinding in the functions called by [GDB].
```

`set unwind-on-terminating-exception`

:

```
Set unwinding of the stack if a C++ exception is raised, but left unhandled while in a function that [GDB] the exception is delivered to the default C++ exception handler and the inferior terminated.
```

`show unwind-on-terminating-exception`

:

```
Show the current setting of stack unwinding in the functions called by [GDB].
```

`set may-call-functions`

:

```
Set permission to call functions in the program. This controls whether [GDB] will attempt to call functions in the program, such as with expressions in the `print` command. It defaults to `on`.

To call a function in the program, [GDB] from calling functions in the program being debugged. If calling functions in the program is forbidden, GDB will throw an error when a command (such as printing an expression) starts a function call in the program.
```

`show may-call-functions`

:

```
Show permission to call functions in the program.
```

When calling a function within a program, it is possible that the program could enter a state from which the called function may never return. If this happens then it is possible to interrupt the function call by typing the interrupt character (often [Ctrl-c]).

If a called function is interrupted for any reason, including hitting a breakpoint, or triggering a watchpoint, and the stack is not unwound due to `set unwind-on-terminating-exception on` or `set unwindonsignal on` (see [stack unwind settings](#stack-unwind-settings)), then the dummy-frame, created by [GDB] to facilitate the call to the program function, will be visible in the backtrace, for example frame `#3` in the following backtrace:

::: smallexample

```bash
(gdb) backtrace
#0  0x00007ffff7b3d1e7 in nanosleep () from /lib64/libc.so.6
#1  0x00007ffff7b3d11e in sleep () from /lib64/libc.so.6
#2  0x000000000040113f in deadlock () at test.cc:13
#3  <function called from gdb>
#4  breakpt () at test.cc:20
#5  0x0000000000401151 in main () at test.cc:25
```

:::

At this point it is possible to examine the state of the inferior just like any other stop.

Depending on why the function was interrupted then it may be possible to resume the inferior (using commands like `continue`, `step`, etc). In this case, when the inferior finally returns to the dummy-frame, [GDB] will once again halt the inferior.

#### 17.5.1 Calling functions with no debug info

Sometimes, a function you wish to call is missing debug information. In such case, [GDB] refuses to call the function unless you tell it the type of the function.

For prototyped (i.e. ANSI/ISO style) functions, there are two ways to do that. The simplest is to cast the call to the function's declared return type. For example:

::: smallexample

```bash
(gdb) p getenv ("PATH")
'getenv' has unknown return type; cast the call to its declared return type
(gdb) p (char *) getenv ("PATH")
$1 = 0x7fffffffe7ba "/usr/local/bin:/"...
```

:::

Casting the return type of a no-debug function is equivalent to casting the function to a pointer to a prototyped function that has a prototype that matches the types of the passed-in arguments, and calling that. I.e., the call above is equivalent to:

::: smallexample

```bash
(gdb) p ((char * (*) (const char *)) getenv) ("PATH")
```

:::

and given this prototyped C or C++ function with float parameters:

::: smallexample

```bash
float multiply (float v1, float v2) 
```

:::

these calls are equivalent:

::: smallexample

```bash
(gdb) p (float) multiply (2.0f, 3.0f)
(gdb) p ((float (*) (float, float)) multiply) (2.0f, 3.0f)
```

:::

If the function you wish to call is declared as unprototyped (i.e. old K&R style), you must use the cast-to-function-pointer syntax, so that [GDB] knows that it needs to apply default argument promotions (promote float arguments to double). See [float promotion](ABI.html#ABI). For example, given this unprototyped C function with float parameters, and no debug info:

::: smallexample

```bash
float
multiply_noproto (v1, v2)
  float v1, v2;
{
  return v1 * v2;
}
```

:::

you call it like this:

::: smallexample

```bash
  (gdb) p ((float (*) ()) multiply_noproto) (2.0f, 3.0f)
```

:::

---

::: header
Next: [Patching](Patching.html#Patching)]
:::
