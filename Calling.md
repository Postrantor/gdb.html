---
tip: translate by openai@2023-06-23 18:49:17
...
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

> 評估表達式`expr`並顯示結果值。該表達式可能包括調試程序中的函數調用。

`call expr`


Evaluate the expression `expr` without displaying `void` returned values.

> 評估表達式`expr`而不顯示返回的`void`值。


You can use this variant of the `print` command if you want to execute a function from your program that does not return anything (a.k.a. *a void function*), but without cluttering the output with `void` returned values that [GDB] will otherwise print. If the result is not void, it is printed and saved in the value history.

> 你可以使用这个版本的`print`命令，如果你想要执行一个程序中不会返回任何值（也就是*void函数*），而不会让[GDB]输出`void`返回值。如果结果不是void，它就会被打印出来并保存在值历史中。


It is possible for the function you call via the `print` or `call` command to generate a signal (e.g., if there's a bug in the function, or if you passed it incorrect arguments). What happens in that case is controlled by the `set unwindonsignal` command.

> 可以通过`print`或`call`命令调用的函数可能会产生信号（例如，如果函数中存在错误，或者您传入了不正确的参数）。在这种情况下，受`set unwindonsignal`命令的控制。


Similarly, with a C++ program it is possible for the function you call via the `print` or `call` command to generate an exception that is not handled due to the constraints of the dummy frame. In this case, any exception that is raised in the frame, but has an out-of-frame exception handler will not be found. GDB builds a dummy-frame for the inferior function call, and the unwinder cannot seek for exception handlers outside of this dummy-frame. What happens in that case is controlled by the `set unwind-on-terminating-exception` command.

> 同样，在C++程序中，您通过“print”或“call”命令调用的函数可能会引发由于虚拟帧的限制而未处理的异常。在这种情况下，任何在帧中引发的但具有超出帧的异常处理程序的异常都将无法找到。GDB为次级函数调用构建了一个虚拟帧，异常解除器无法在此虚拟帧之外查找异常处理程序。此时发生的情况由“set unwind-on-terminating-exception”命令控制。

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

> 当在程序中调用一个函数时，可能会发生程序进入一个永远无法从函数返回的状态。如果发生这种情况，可以通过输入中断字符（通常是[Ctrl-c]）来中断函数调用。


If a called function is interrupted for any reason, including hitting a breakpoint, or triggering a watchpoint, and the stack is not unwound due to `set unwind-on-terminating-exception on` or `set unwindonsignal on` (see [stack unwind settings](#stack-unwind-settings)), then the dummy-frame, created by [GDB] to facilitate the call to the program function, will be visible in the backtrace, for example frame `#3` in the following backtrace:

> 如果被调用的函数因任何原因（包括遇到断点或触发观察点）被中断，且由于“设置unwind-on-terminating-exception”或“设置unwindonsignal”（参见[堆栈解包设置]（#stack-unwind-settings））而未展开堆栈，那么[GDB]为了方便调用程序函数而创建的虚拟帧就会出现在回溯中，例如以下回溯中的第3帧：

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

> 在这一点上，可以像检查其他停止一样检查劣势状态。


Depending on why the function was interrupted then it may be possible to resume the inferior (using commands like `continue`, `step`, etc). In this case, when the inferior finally returns to the dummy-frame, [GDB] will once again halt the inferior.

> 取决于为什么中断函数，可能可以恢复次要（使用像`continue`、`step`等命令）。在这种情况下，当次要最终返回到虚拟帧时，[GDB]将再次暂停次要。

#### 17.5.1 Calling functions with no debug info


Sometimes, a function you wish to call is missing debug information. In such case, [GDB] refuses to call the function unless you tell it the type of the function.

> 有时，您希望调用的函数缺少调试信息。在这种情况下，GDB拒绝调用该函数，除非您告诉它函数的类型。


For prototyped (i.e. ANSI/ISO style) functions, there are two ways to do that. The simplest is to cast the call to the function's declared return type. For example:

> 对于原型（即ANSI / ISO样式）函数，有两种方法可以做到这一点。最简单的是将调用转换为函数声明的返回类型。例如：

::: smallexample

```bash
(gdb) p getenv ("PATH")
'getenv' has unknown return type; cast the call to its declared return type
(gdb) p (char *) getenv ("PATH")
$1 = 0x7fffffffe7ba "/usr/local/bin:/"...
```

:::


Casting the return type of a no-debug function is equivalent to casting the function to a pointer to a prototyped function that has a prototype that matches the types of the passed-in arguments, and calling that. I.e., the call above is equivalent to:

> 将不调试函数的返回类型投射等同于将该函数投射为具有与传入参数类型匹配的原型函数的指针，并调用它。即，上述调用等同于：

::: smallexample

```bash
(gdb) p ((char * (*) (const char *)) getenv) ("PATH")
```

:::


and given this prototyped C or C++ function with float parameters:

> 给定这个用浮点参数原型化的C或C++函数：

::: smallexample

```bash
float multiply (float v1, float v2) 
```

:::


these calls are equivalent:

> 这些调用是等价的。

::: smallexample

```bash
(gdb) p (float) multiply (2.0f, 3.0f)
(gdb) p ((float (*) (float, float)) multiply) (2.0f, 3.0f)
```

:::


If the function you wish to call is declared as unprototyped (i.e. old K&R style), you must use the cast-to-function-pointer syntax, so that [GDB] knows that it needs to apply default argument promotions (promote float arguments to double). See [float promotion](ABI.html#ABI). For example, given this unprototyped C function with float parameters, and no debug info:

> 如果您想要调用的函数声明为未原型化（即旧的K＆R样式），则必须使用函数指针转换语法，以便[GDB]知道它需要应用默认参数促进（将float参数升级为double）。参见[浮点促进](ABI.html#ABI)。例如，给定具有float参数且没有调试信息的此未原型化的C函数：

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
