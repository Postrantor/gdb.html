---
tip: translate by openai@2023-06-24 02:49:38
...
---
description: Set Watchpoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Set Watchpoints (Debugging with GDB)
lang: en
resource-type: document
title: Set Watchpoints (Debugging with GDB)
---
::: header
Next: [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)]
:::

---

#### 5.1.2 Setting Watchpoints


You can use a watchpoint to stop execution whenever the value of an expression changes, without having to predict a particular place where this may happen. (This is sometimes called a *data breakpoint*.) The expression may be as simple as the value of a single variable, or as complex as many variables combined by operators. Examples include:

> 你可以使用观察点来停止执行，只要表达式的值发生变化，而不必预测可能发生变化的特定位置。（这有时被称为*数据断点*。）该表达式可以是单个变量的值，也可以是由操作符组合多个变量的值。例子包括：

- A reference to the value of a single variable.

- An address cast to an appropriate data type. For example, '`*(int *)0x12345678`' will watch a 4-byte region at the specified address (assuming an `int` occupies 4 bytes).

> *(int *)0x12345678`将会检查指定地址处（假设一个`int`占据4个字节）的4个字节区域。

- An arbitrarily complex expression, such as '`a*b + c/d`'. The expression can use any operators valid in the program's native language (see [Languages](Languages.html#Languages)).

> 一个任意复杂的表达式，例如'a*b + c/d'。该表达式可以使用程序本地语言中的任何有效运算符（参见[语言]（Languages.html#Languages））。


You can set a watchpoint on an expression even if the expression can not be evaluated yet. For instance, you can set a watchpoint on '`*global_ptr` may not stop until the next time the expression changes.

> 你可以在一个表达式上设置一个观察点，即使这个表达式还不能被评估。例如，你可以在'*global_ptr'上设置一个观察点，直到表达式改变下次才会停止。


Depending on your system, watchpoints may be implemented in software or hardware. [GDB] does software watchpointing by single-stepping your program and testing the variable's value each time, which is hundreds of times slower than normal execution. (But this may still be worth it, to catch errors where you have no clue what part of your program is the culprit.)

> 根据您的系统，可以使用软件或硬件实现断点。[GDB] 通过单步执行程序并每次测试变量的值来实现软件断点，这比正常执行慢数百倍。（但是，这可能仍然值得，以捕获您不知道程序的哪部分是罪魁祸首的错误。）


On some systems, such as most PowerPC or x86-based targets, [GDB] includes support for hardware watchpoints, which do not slow down the running of your program.

> 在一些系统上，如大多数基于PowerPC或x86的目标，[GDB]包括对硬件断点的支持，这不会减慢程序的运行。

`watch [-l|-location] expr [thread thread-id] [mask maskvalue] [task task-id]`


Set a watchpoint for an expression. [GDB] is written into by the program and its value changes. The simplest (and the most popular) use of this command is to watch the value of a single variable:

> 设置一个表达式的断点。[GDB]被程序写入，其值会发生变化。使用此命令的最简单（也是最受欢迎的）方法是监视单个变量的值：

::: smallexample

```bash
(gdb) watch foo
```

:::


If the command includes a `[thread thread-id]` argument, [GDB] will not break. Note that watchpoints restricted to a single thread in this way only work with Hardware Watchpoints.

> 如果命令包含一个`[thread thread-id]`参数，[GDB]将不会中断。请注意，以这种方式限制为单个线程的观察点只适用于硬件观察点。


Similarly, if the `task` argument is given, then the watchpoint will be specific to the indicated Ada task (see [Ada Tasks](Ada-Tasks.html#Ada-Tasks)).

> 如果给出`task`参数，那么监视点将特定于指定的Ada任务（请参阅[Ada任务](Ada-Tasks.html#Ada-Tasks)）。


Ordinarily a watchpoint respects the scope of variables in `expr` will print an error.

> 通常情况下，观察点会遵守变量范围，如果在`expr`中打印一个错误将会发生什么。


The `[mask maskvalue]` argument allows creation of masked watchpoints, if the current architecture supports this feature (e.g., PowerPC Embedded architecture, see [PowerPC Embedded](PowerPC-Embedded.html#PowerPC-Embedded).) A *masked watchpoint* specifies a mask in addition to an address to watch. The mask specifies that some bits of an address (the bits which are reset in the mask) should be ignored when matching the address accessed by the inferior against the watchpoint address. Thus, a masked watchpoint watches many addresses simultaneously---those addresses whose unmasked bits are identical to the unmasked bits in the watchpoint address. The `mask` argument implies `-location`. Examples:

> [mask maskvalue]参数允许在当前架构支持这个功能的情况下创建masked watchpoints（例如PowerPC嵌入式架构，请参见[PowerPC嵌入式]（PowerPC-Embedded.html#PowerPC-Embedded））。 *Masked watchpoint*指定了除了地址之外的掩码。掩码指定地址的某些位（在掩码中复位的位）在与观察点地址匹配时应被忽略。因此，masked watchpoint可以同时观察多个地址-那些未掩码位与观察点地址的未掩码位相同的地址。 `mask`参数意味着`-location`。 例子：

::: smallexample

```bash
(gdb) watch foo mask 0xffff00ff
(gdb) watch *0xdeadbeef mask 0xffffff00
```

:::

`rwatch [-l|-location] expr [thread thread-id] [mask maskvalue]`


Set a watchpoint that will break when the value of `expr` is read by the program.

> 设置一个断点，当程序读取`expr`的值时会中断。

`awatch [-l|-location] expr [thread thread-id] [mask maskvalue]`


Set a watchpoint that will break when `expr` is either read from or written into by the program.

> 设置一个断点，当程序读取或写入`expr`时会中断。

`info watchpoints [list…]`


This command prints a list of watchpoints, using the same format as `info break` (see [Set Breaks](Set-Breaks.html#Set-Breaks)).

> 这个命令使用与`info break`相同的格式打印出一个断点列表（参见[设置断点](Set-Breaks.html#Set-Breaks)）。


If you watch for a change in a numerically entered address you need to dereference it, as the address itself is just a constant number which will never change. [GDB] refuses to create a watchpoint that watches a never-changing value:

> 如果你想监视一个输入的数字地址的变化，你需要解除引用，因为地址本身只是一个永远不变的数字。GDB拒绝创建一个监视永不变值的监视点。

::: smallexample

```bash
(gdb) watch 0x600850
Cannot watch constant value 0x600850.
(gdb) watch *(int *) 0x600850
Watchpoint 1: *(int *) 6293584
```

:::


[GDB] cannot set a hardware watchpoint, it sets a software watchpoint, which executes more slowly and reports the change in value at the next *statement*, not the instruction, after the change occurs.

> GDB无法设置硬件断点，只能设置软件断点，这种断点的执行速度比较慢，它只能在值发生变化之后的下一条语句处报告变化，而不是指令。


You can force [GDB] will never try to use hardware watchpoints, even if the underlying system supports them. (Note that hardware-assisted watchpoints that were set *before* setting `can-use-hw-watchpoints` to zero will still use the hardware mechanism of watching expression values.)

> 你可以强制GDB永远不会尝试使用硬件断点，即使底层系统支持它们也是如此。（注意，在将`can-use-hw-watchpoints`设置为零之前设置的硬件辅助断点仍将使用硬件机制来监视表达式值。）

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

> 对于远程目标，您可以限制GDB使用的硬件断点的数量，请参见[设置远程硬件断点限制](Remote-Configuration.html#set-remote-hardware_002dbreakpoint_002dlimit)。

When you issue the `watch` command, [GDB] reports

::: smallexample

```bash
Hardware watchpoint num: expr
```

:::

if it was able to set a hardware watchpoint.


Currently, the `awatch` and `rwatch` commands can only set hardware watchpoints, because accesses to data that don't change the value of the watched expression cannot be detected without examining every instruction as it is being executed, and [GDB] finds that it is unable to set a hardware breakpoint with the `awatch` or `rwatch` command, it will print a message like this:

> 目前，`awatch`和`rwatch`命令只能设置硬件断点，因为不改变被监视表达式的值的访问无法在执行每条指令时检查，[GDB]发现无法使用`awatch`或`rwatch`命令设置硬件断点，将打印出类似此类消息：

::: smallexample

```bash
Expression cannot be implemented with read/access watchpoint.
```

:::


Sometimes, [GDB] cannot set a hardware watchpoint because the data type of the watched expression is wider than what a hardware watchpoint on the target machine can handle. For example, some systems can only watch regions that are up to 4 bytes wide; on such systems you cannot set hardware watchpoints for an expression that yields a double-precision floating-point number (which is typically 8 bytes wide). As a work-around, it might be possible to break the large region into a series of smaller ones and watch them with separate watchpoints.

> 有时，[GDB]无法设置硬件断点，因为被监视表达式的数据类型比目标机器上的硬件断点处理能力更宽。例如，某些系统只能观察最多4个字节宽的区域；在这样的系统上，您不能为产生双精度浮点数（通常为8个字节宽）的表达式设置硬件断点。作为一种解决方案，可以将大型区域拆分为一系列较小的区域，并用单独的断点进行观察。


If you set too many hardware watchpoints, [GDB] might not be able to warn you about this when you set the watchpoints, and the warning will be printed only when the program is resumed:

> 如果你设置了太多的硬件断点，[GDB] 在你设置断点时可能无法警告你，只有在程序恢复时才会打印警告。

::: smallexample

```bash
Hardware watchpoint num: Could not insert watchpoint
```

:::

If this happens, delete or disable some of the watchpoints.


Watching complex expressions that reference many variables can also exhaust the resources available for hardware-assisted watchpoints. That's because [GDB] needs to watch every variable in the expression with separately allocated resources.

> 观察引用多个变量的复杂表达式也会耗尽可用于硬件辅助断点的资源。这是因为[GDB]需要以单独分配的资源监视表达式中的每个变量。


If you call a function interactively using `print` or `call`, any watchpoints you have set will be inactive until [GDB] reaches another kind of breakpoint or the call completes.

> 如果您使用`print`或`call`以交互方式调用函数，则在GDB到达另一种断点或调用完成之前，您设置的任何断点都将处于非活动状态。


[GDB] automatically deletes watchpoints that watch local (automatic) variables, or expressions that involve such variables, when they go out of scope, that is, when the execution leaves the block in which these variables were defined. In particular, when the program being debugged terminates, *all* local variables go out of scope, and so only watchpoints that watch global variables remain set. If you rerun the program, you will need to set all such watchpoints again. One way of doing that would be to set a code breakpoint at the entry to the `main` function and when it breaks, set all the watchpoints.

> GDB会自动删除监视局部（自动）变量或包含这些变量的表达式的观察点，当它们超出作用域时，也就是当执行离开定义这些变量的块时。特别是，当调试的程序终止时，所有局部变量都超出作用域，因此只有监视全局变量的观察点仍被设置。如果您重新运行程序，则需要重新设置所有此类观察点。一种做法是在进入`main`函数时设置代码断点，当它中断时，设置所有观察点。


In multi-threaded programs, watchpoints will detect changes to the watched expression from every thread.

> 在多线程程序中，监视点将检测来自每个线程的被监视表达式的变化。

> *Warning:* In multi-threaded programs, software watchpoints have only limited usefulness. If [GDB] may not notice when a non-current thread's activity changes the expression. (Hardware watchpoints, in contrast, watch an expression in all threads.)


See [set remote hardware-watchpoint-limit](Remote-Configuration.html#set-remote-hardware_002dwatchpoint_002dlimit).

> 请参见[设置远程硬件监视点限制](Remote-Configuration.html#set-remote-hardware_002dwatchpoint_002dlimit)。

---

::: header
Next: [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)]
:::
