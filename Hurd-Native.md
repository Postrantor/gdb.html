---
description: Hurd Native (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Hurd Native (Debugging with GDB)
lang: en
resource-type: document
title: Hurd Native (Debugging with GDB)
---
::: header
Next: [Darwin](Darwin.html#Darwin)]
:::

---

#### 21.1.5 Commands Specific to [GNU]

This subsection describes [GDB] Hurd native debugging.

`set signals`
`set sigs`

:

```
This command toggles the state of inferior signal interception by [GDB]. Mach exceptions, such as breakpoint traps, are not affected by this command. `sigs` is a shorthand alias for `signals`.
```

`show signals`
`show sigs`

:

```
Show the current state of intercepting inferior's signals.
```

`set signal-thread`
`set sigthread`

:

```
This command tells [GDB] which thread is the `libc` signal thread. That thread is run when a signal is delivered to a running process. `set sigthread` is the shorthand alias of `set signal-thread`.
```

`show signal-thread`
`show sigthread`

:

```
These two commands show which thread will run when the inferior is delivered a signal.
```

`set stopped`

:

```
This commands tells [GDB] that the inferior process is stopped, as with the `SIGSTOP` signal. The stopped process can be continued by delivering a signal to it.
```

`show stopped`

:

```
This command shows whether [GDB] thinks the debuggee is stopped.
```

`set exceptions`

:

```
Use this command to turn off trapping of exceptions in the inferior. When exception trapping is off, neither breakpoints nor single-stepping will work. To restore the default, set exception trapping on.
```

`show exceptions`

:

```
Show the current state of trapping exceptions in the inferior.
```

`set task pause`

:

```
This command toggles task suspension when [GDB] gets control. Setting it to off will take effect the next time the inferior is continued. If this option is set to off, you can use `set thread default pause on` or `set thread pause on` (see below) to pause individual threads.
```

`show task pause`

:

```
Show the current state of task suspension.
```

`set task detach-suspend-count`

:

```
This command sets the suspend count the task will be left with when [GDB] detaches from it.
```

`show task detach-suspend-count`

:   Show the suspend count the task will be left with when detaching.

`set task exception-port`
`set task excp`

:

```
This command sets the task exception port to which [GDB] will forward exceptions. The argument should be the value of the *send rights* of the task. `set task excp` is a shorthand alias.
```

`set noninvasive`

:

```
This command switches [GDB] to a mode that is the least invasive as far as interfering with the inferior is concerned. This is the same as using `set task pause`, `set exceptions`, and `set signals` to values opposite to the defaults.
```

`info send-rights`
`info receive-rights`
`info port-rights`
`info port-sets`
`info dead-names`
`info ports`
`info psets`

:

```
These commands display information about, respectively, send rights, receive rights, port rights, port sets, and dead names of a task. There are also shorthand aliases: `info ports` for `info port-rights` and `info psets` for `info port-sets`.
```

`set thread pause`

:

```
This command toggles current thread suspension when [GDB] has control, the whole task is suspended. However, if you used `set task pause off` (see above), this command comes in handy to suspend only the current thread.
```

`show thread pause`

:

```
This command shows the state of current thread suspension.
```

`set thread run`

:   This command sets whether the current thread is allowed to run.

`show thread run`

:   Show whether the current thread is allowed to run.

`set thread detach-suspend-count`

:

```
This command sets the suspend count [GDB] when it notices the thread; use `set thread takeover-suspend-count` to force it to an absolute value.
```

`show thread detach-suspend-count`

:   Show the suspend count [GDB] will leave on the thread when detaching.

`set thread exception-port`
`set thread excp`

:   Set the thread exception port to which to forward exceptions. This overrides the port set by `set task exception-port` (see above). `set thread excp` is the shorthand alias.

`set thread takeover-suspend-count`

:   Normally, [GDB] finds when it notices each thread. This command changes the suspend counts to be absolute instead.

`set thread default`
`show thread default`

:

```
Each of the above `set thread` commands has a `set thread default` counterpart (e.g., `set thread default pause`, `set thread default exception-port`, etc.). The `thread default` variety of commands sets the default thread properties for all threads; you can then change the properties of individual threads with the non-default commands.
```

---

::: header
Next: [Darwin](Darwin.html#Darwin)]
:::
