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

- A reference to the value of a single variable.
- An address cast to an appropriate data type. For example, '`*(int *)0x12345678`' will watch a 4-byte region at the specified address (assuming an `int` occupies 4 bytes).
- An arbitrarily complex expression, such as '`a*b + c/d`'. The expression can use any operators valid in the program's native language (see [Languages](Languages.html#Languages)).

You can set a watchpoint on an expression even if the expression can not be evaluated yet. For instance, you can set a watchpoint on '`*global_ptr` may not stop until the next time the expression changes.

Depending on your system, watchpoints may be implemented in software or hardware. [GDB] does software watchpointing by single-stepping your program and testing the variable's value each time, which is hundreds of times slower than normal execution. (But this may still be worth it, to catch errors where you have no clue what part of your program is the culprit.)

On some systems, such as most PowerPC or x86-based targets, [GDB] includes support for hardware watchpoints, which do not slow down the running of your program.

`watch [-l|-location] expr [thread thread-id] [mask maskvalue] [task task-id]`

Set a watchpoint for an expression. [GDB] is written into by the program and its value changes. The simplest (and the most popular) use of this command is to watch the value of a single variable:

::: smallexample

```bash
(gdb) watch foo
```

:::

If the command includes a `[thread thread-id]` argument, [GDB] will not break. Note that watchpoints restricted to a single thread in this way only work with Hardware Watchpoints.

Similarly, if the `task` argument is given, then the watchpoint will be specific to the indicated Ada task (see [Ada Tasks](Ada-Tasks.html#Ada-Tasks)).

Ordinarily a watchpoint respects the scope of variables in `expr` will print an error.

The `[mask maskvalue]` argument allows creation of masked watchpoints, if the current architecture supports this feature (e.g., PowerPC Embedded architecture, see [PowerPC Embedded](PowerPC-Embedded.html#PowerPC-Embedded).) A *masked watchpoint* specifies a mask in addition to an address to watch. The mask specifies that some bits of an address (the bits which are reset in the mask) should be ignored when matching the address accessed by the inferior against the watchpoint address. Thus, a masked watchpoint watches many addresses simultaneously---those addresses whose unmasked bits are identical to the unmasked bits in the watchpoint address. The `mask` argument implies `-location`. Examples:

::: smallexample

```bash
(gdb) watch foo mask 0xffff00ff
(gdb) watch *0xdeadbeef mask 0xffffff00
```

:::

`rwatch [-l|-location] expr [thread thread-id] [mask maskvalue]`

Set a watchpoint that will break when the value of `expr` is read by the program.

`awatch [-l|-location] expr [thread thread-id] [mask maskvalue]`

Set a watchpoint that will break when `expr` is either read from or written into by the program.

`info watchpoints [list…]`

This command prints a list of watchpoints, using the same format as `info break` (see [Set Breaks](Set-Breaks.html#Set-Breaks)).

If you watch for a change in a numerically entered address you need to dereference it, as the address itself is just a constant number which will never change. [GDB] refuses to create a watchpoint that watches a never-changing value:

::: smallexample

```bash
(gdb) watch 0x600850
Cannot watch constant value 0x600850.
(gdb) watch *(int *) 0x600850
Watchpoint 1: *(int *) 6293584
```

:::

[GDB] cannot set a hardware watchpoint, it sets a software watchpoint, which executes more slowly and reports the change in value at the next *statement*, not the instruction, after the change occurs.

You can force [GDB] will never try to use hardware watchpoints, even if the underlying system supports them. (Note that hardware-assisted watchpoints that were set *before* setting `can-use-hw-watchpoints` to zero will still use the hardware mechanism of watching expression values.)

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

When you issue the `watch` command, [GDB] reports

::: smallexample

```bash
Hardware watchpoint num: expr
```

:::

if it was able to set a hardware watchpoint.

Currently, the `awatch` and `rwatch` commands can only set hardware watchpoints, because accesses to data that don't change the value of the watched expression cannot be detected without examining every instruction as it is being executed, and [GDB] finds that it is unable to set a hardware breakpoint with the `awatch` or `rwatch` command, it will print a message like this:

::: smallexample

```bash
Expression cannot be implemented with read/access watchpoint.
```

:::

Sometimes, [GDB] cannot set a hardware watchpoint because the data type of the watched expression is wider than what a hardware watchpoint on the target machine can handle. For example, some systems can only watch regions that are up to 4 bytes wide; on such systems you cannot set hardware watchpoints for an expression that yields a double-precision floating-point number (which is typically 8 bytes wide). As a work-around, it might be possible to break the large region into a series of smaller ones and watch them with separate watchpoints.

If you set too many hardware watchpoints, [GDB] might not be able to warn you about this when you set the watchpoints, and the warning will be printed only when the program is resumed:

::: smallexample

```bash
Hardware watchpoint num: Could not insert watchpoint
```

:::

If this happens, delete or disable some of the watchpoints.

Watching complex expressions that reference many variables can also exhaust the resources available for hardware-assisted watchpoints. That's because [GDB] needs to watch every variable in the expression with separately allocated resources.

If you call a function interactively using `print` or `call`, any watchpoints you have set will be inactive until [GDB] reaches another kind of breakpoint or the call completes.

[GDB] automatically deletes watchpoints that watch local (automatic) variables, or expressions that involve such variables, when they go out of scope, that is, when the execution leaves the block in which these variables were defined. In particular, when the program being debugged terminates, *all* local variables go out of scope, and so only watchpoints that watch global variables remain set. If you rerun the program, you will need to set all such watchpoints again. One way of doing that would be to set a code breakpoint at the entry to the `main` function and when it breaks, set all the watchpoints.

In multi-threaded programs, watchpoints will detect changes to the watched expression from every thread.

> *Warning:* In multi-threaded programs, software watchpoints have only limited usefulness. If [GDB] may not notice when a non-current thread's activity changes the expression. (Hardware watchpoints, in contrast, watch an expression in all threads.)

See [set remote hardware-watchpoint-limit](Remote-Configuration.html#set-remote-hardware_002dwatchpoint_002dlimit).

---

::: header
Next: [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)]
:::
