---
tip: translate by openai@2023-06-23 13:09:43
...
---
description: Set Watchpoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Set Watchpoints (Debugging with GDB)
lang: en
resource-type: document
title: Set Watchpoints (Debugging with GDB)
-------------------------------------------

::: header
Next: [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)]
:::

---

#### 5.1.2 Setting Watchpoints

You can use a watchpoint to stop execution whenever the value of an expression changes, without having to predict a particular place where this may happen. (This is sometimes called a *data breakpoint*.) The expression may be as simple as the value of a single variable, or as complex as many variables combined by operators. Examples include:

> 你可以使用一个监视点来在表达式的值发生变化时停止执行，而无需预测这可能发生的特定位置。（这有时被称为*数据断点*。）表达式可以是单个变量的值的简单，也可以是由操作符组合的多个变量的复杂。例子包括：

- A reference to the value of a single variable.
- An address cast to an appropriate data type. For example, '`*(int *)0x12345678`' will watch a 4-byte region at the specified address (assuming an `int` occupies 4 bytes).

> `(int *)0x12345678` 将监视指定地址处的 4 字节区域（假设 `int` 占用 4 字节），这是将地址转换为适当的数据类型。

- An arbitrarily complex expression, such as '`a*b + c/d`'. The expression can use any operators valid in the program's native language (see [Languages](Languages.html#Languages)).

> 一个任意复杂的表达式，比如'a*b + c/d'。表达式可以使用程序本地语言中有效的任何运算符（参见[语言]（Languages.html#Languages））。

You can set a watchpoint on an expression even if the expression can not be evaluated yet. For instance, you can set a watchpoint on '`*global_ptr` may not stop until the next time the expression changes.

> 你可以在一个表达式上设置一个观察点，即使这个表达式还不能被评估。例如，你可以在'*global_ptr'上设置一个观察点，直到表达式下次改变前都不会停止。

Depending on your system, watchpoints may be implemented in software or hardware. [GDB] does software watchpointing by single-stepping your program and testing the variable's value each time, which is hundreds of times slower than normal execution. (But this may still be worth it, to catch errors where you have no clue what part of your program is the culprit.)

> 根据你的系统，观察点可以用软件或者硬件实现。[GDB] 通过单步运行你的程序并每次测试变量的值来实现软件观察点，这比正常执行要慢上百倍。（但这可能仍然值得，以便捕获你不知道程序的哪个部分是罪魁祸首的错误。）

On some systems, such as most PowerPC or x86-based targets, [GDB] includes support for hardware watchpoints, which do not slow down the running of your program.

> 在一些系统上，如大多数基于 PowerPC 或 x86 的目标，[GDB]包括对硬件断点的支持，这不会减慢程序的运行速度。

`watch [-l|-location] expr [thread thread-id] [mask maskvalue] [task task-id]`

Set a watchpoint for an expression. [GDB] is written into by the program and its value changes. The simplest (and the most popular) use of this command is to watch the value of a single variable:

> 设置一个表达式的断点。[GDB]被程序写入，其值会改变。使用此命令最简单（也是最受欢迎）的方法是观察一个变量的值：

::: smallexample

```bash
(gdb) watch foo
```

:::

If the command includes a `[thread thread-id]` argument, [GDB] will not break. Note that watchpoints restricted to a single thread in this way only work with Hardware Watchpoints.

> 如果命令包含 `[thread thread-id]` 参数，[GDB]不会中断。请注意，以这种方式限定单个线程的观察点只适用于硬件观察点。

Similarly, if the `task` argument is given, then the watchpoint will be specific to the indicated Ada task (see [Ada Tasks](Ada-Tasks.html#Ada-Tasks)).

> 如果给定 `task` 参数，则监视点将特定于所指定的 Ada 任务（参见 [Ada 任务](Ada-Tasks.html#Ada-Tasks)）。

Ordinarily a watchpoint respects the scope of variables in `expr` will print an error.

> 通常情况下，断点观察会遵守变量的作用域，如果在 `expr` 中打印错误，则会报错。

The `[mask maskvalue]` argument allows creation of masked watchpoints, if the current architecture supports this feature (e.g., PowerPC Embedded architecture, see [PowerPC Embedded](PowerPC-Embedded.html#PowerPC-Embedded).) A *masked watchpoint* specifies a mask in addition to an address to watch. The mask specifies that some bits of an address (the bits which are reset in the mask) should be ignored when matching the address accessed by the inferior against the watchpoint address. Thus, a masked watchpoint watches many addresses simultaneously---those addresses whose unmasked bits are identical to the unmasked bits in the watchpoint address. The `mask` argument implies `-location`. Examples:

> mask 参数允许在当前架构支持的情况下创建 masked watchpoints（例如 PowerPC 嵌入式架构，参见 [PowerPC 嵌入式](PowerPC-Embedded.html#PowerPC-Embedded)）。masked watchpoint 指定除了地址外还有一个掩码。掩码指定地址的某些位（掩码中被复位的位）在与 watchpoint 地址匹配时应被忽略。因此，masked watchpoint 同时监视许多地址——那些未被掩码掩码的位与 watchpoint 地址未被掩码的位相同的地址。mask 参数隐含了-location 参数。例子：

::: smallexample

```bash
(gdb) watch foo mask 0xffff00ff
(gdb) watch *0xdeadbeef mask 0xffffff00
```

:::

`rwatch [-l|-location] expr [thread thread-id] [mask maskvalue]`

Set a watchpoint that will break when the value of `expr` is read by the program.

> 设置一个断点，当程序读取 `expr` 的值时将中断。

`awatch [-l|-location] expr [thread thread-id] [mask maskvalue]`

Set a watchpoint that will break when `expr` is either read from or written into by the program.

> 设置一个断点，当程序读取或写入 `expr` 时断点就会被触发。

`info watchpoints [list…]`

This command prints a list of watchpoints, using the same format as `info break` (see [Set Breaks](Set-Breaks.html#Set-Breaks)).

> 这个命令使用和 `info break` 相同的格式打印出一个断点列表（参见[设置断点](Set-Breaks.html#Set-Breaks)）。

If you watch for a change in a numerically entered address you need to dereference it, as the address itself is just a constant number which will never change. [GDB] refuses to create a watchpoint that watches a never-changing value:

> 如果您要监视输入的数字地址的变化，则需要取消对其的引用，因为该地址本身只是一个永不改变的常量。[GDB]拒绝创建一个监视永不改变的值的断点：

::: smallexample

```bash
(gdb) watch 0x600850
Cannot watch constant value 0x600850.
(gdb) watch *(int *) 0x600850
Watchpoint 1: *(int *) 6293584
```

:::

[GDB] cannot set a hardware watchpoint, it sets a software watchpoint, which executes more slowly and reports the change in value at the next *statement*, not the instruction, after the change occurs.

> GDB 无法设置硬件断点，它会设置软件断点，这会导致执行速度变慢，并且只能在变量值发生变化后的下一个语句处报告变化，而不是变化发生后的指令处。

You can force [GDB] will never try to use hardware watchpoints, even if the underlying system supports them. (Note that hardware-assisted watchpoints that were set *before* setting `can-use-hw-watchpoints` to zero will still use the hardware mechanism of watching expression values.)

> 你可以强制 GDB 永远不尝试使用硬件断点，即使底层系统支持它们也是如此（请注意，在将 `can-use-hw-watchpoints` 设置为零之前设置的硬件辅助断点仍会使用监视表达式值的硬件机制）。

`set can-use-hw-watchpoints`

:

```
Set whether or not to use hardware watchpoints.
```

`show can-use-hw-watchpoints`

:

```
Show the current mode of using hardware watchpoints.
```

For remote targets, you can restrict the number of hardware watchpoints [GDB] will use, see [set remote hardware-breakpoint-limit](Remote-Configuration.html#set-remote-hardware_002dbreakpoint_002dlimit).

> 对于远程目标，您可以限制 GDB 将使用的硬件断点数量，请参见[设置远程硬件断点限制](Remote-Configuration.html#set-remote-hardware_002dbreakpoint_002dlimit)。

When you issue the `watch` command, [GDB] reports

> 当你输入 `watch` 命令时，[GDB]报告

::: smallexample

```bash
Hardware watchpoint num: expr
```

:::

if it was able to set a hardware watchpoint.

> 如果能够设置硬件断点，就好了。

Currently, the `awatch` and `rwatch` commands can only set hardware watchpoints, because accesses to data that don't change the value of the watched expression cannot be detected without examining every instruction as it is being executed, and [GDB] finds that it is unable to set a hardware breakpoint with the `awatch` or `rwatch` command, it will print a message like this:

> 目前，`awatch` 和 `rwatch` 命令只能设置硬件断点，因为不改变被监视表达式值的数据访问无法在每条指令执行时进行检查，而[GDB]发现无法使用 `awatch` 或 `rwatch` 命令设置硬件断点，它将打印类似这样的消息：

::: smallexample

```bash
Expression cannot be implemented with read/access watchpoint.
```

:::

Sometimes, [GDB] cannot set a hardware watchpoint because the data type of the watched expression is wider than what a hardware watchpoint on the target machine can handle. For example, some systems can only watch regions that are up to 4 bytes wide; on such systems you cannot set hardware watchpoints for an expression that yields a double-precision floating-point number (which is typically 8 bytes wide). As a work-around, it might be possible to break the large region into a series of smaller ones and watch them with separate watchpoints.

> 有时，[GDB]无法设置硬件断点，因为被监视表达式的数据类型比目标机器上可以处理的硬件断点宽。例如，一些系统只能监视最多 4 个字节宽的区域；在这样的系统上，您无法为产生双精度浮点数（通常为 8 个字节宽）的表达式设置硬件断点。作为一种解决方法，可以将大型区域分成一系列较小的区域，并用单独的断点监视它们。

If you set too many hardware watchpoints, [GDB] might not be able to warn you about this when you set the watchpoints, and the warning will be printed only when the program is resumed:

> 如果你设置了太多硬件断点，GDB 可能无法在你设置断点时警告你，只有在程序恢复时才会打印警告。

::: smallexample

```bash
Hardware watchpoint num: Could not insert watchpoint
```

:::

If this happens, delete or disable some of the watchpoints.

> 如果发生这种情况，请删除或禁用一些断点。

Watching complex expressions that reference many variables can also exhaust the resources available for hardware-assisted watchpoints. That's because [GDB] needs to watch every variable in the expression with separately allocated resources.

> 观察引用许多变量的复杂表达式也可能耗尽硬件辅助断点所提供的资源。这是因为[GDB]需要用单独分配的资源来监视表达式中的每个变量。

If you call a function interactively using `print` or `call`, any watchpoints you have set will be inactive until [GDB] reaches another kind of breakpoint or the call completes.

> 如果您使用 `print` 或 `call` 以交互方式调用函数，则在[GDB]到达另一种断点或调用完成之前，您设置的任何观察点都将处于不活动状态。

[GDB] automatically deletes watchpoints that watch local (automatic) variables, or expressions that involve such variables, when they go out of scope, that is, when the execution leaves the block in which these variables were defined. In particular, when the program being debugged terminates, *all* local variables go out of scope, and so only watchpoints that watch global variables remain set. If you rerun the program, you will need to set all such watchpoints again. One way of doing that would be to set a code breakpoint at the entry to the `main` function and when it breaks, set all the watchpoints.

> GDB 会自动删除监视本地（自动）变量或涉及这些变量的表达式的观察点，当它们超出范围时，也就是当执行离开定义这些变量的块时。特别是，当被调试的程序终止时，*所有*本地变量都超出范围，因此只有监视全局变量的观察点仍然被设置。如果你重新运行程序，你需要重新设置所有这些观察点。一种做法是在进入 `main` 函数时设置代码断点，当它中断时，设置所有观察点。

In multi-threaded programs, watchpoints will detect changes to the watched expression from every thread.

> 在多线程程序中，监视点将从每个线程检测被监视表达式的变化。

> *Warning:* In multi-threaded programs, software watchpoints have only limited usefulness. If [GDB] may not notice when a non-current thread's activity changes the expression. (Hardware watchpoints, in contrast, watch an expression in all threads.)

See [set remote hardware-watchpoint-limit](Remote-Configuration.html#set-remote-hardware_002dwatchpoint_002dlimit).

> 请参阅[设置远程硬件断点限制](Remote-Configuration.html#set-remote-hardware_002dwatchpoint_002dlimit)。

---

::: header
Next: [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)]
:::
