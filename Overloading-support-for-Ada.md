---
description: Overloading support for Ada (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Overloading support for Ada (Debugging with GDB)
lang: en
resource-type: document
title: Overloading support for Ada (Debugging with GDB)
---
::: header
Next: [Stopping Before Main Program](Stopping-Before-Main-Program.html#Stopping-Before-Main-Program)]
:::

---

#### 15.4.10.4 Overloading support for Ada

The debugger supports limited overloading. Given a subprogram call in which the function symbol has multiple definitions, it will use the number of actual parameters and some information about their types to attempt to narrow the set of definitions. It also makes very limited use of context, preferring procedures to functions in the context of the `call` command, and functions to procedures elsewhere.

If, after narrowing, the set of matching definitions still contains more than one definition, [GDB] will display a menu to query which one it should use, for instance:

::: smallexample

```bash
(gdb) print f(1)
Multiple matches for f
[0] cancel
[1] foo.f (integer) return boolean at foo.adb:23
[2] foo.f (foo.new_integer) return boolean at foo.adb:28
> 
```

:::

In this case, just select one menu entry either to cancel expression evaluation (type [0] and press RET) or to continue evaluation with a specific instance (type the corresponding number and press RET).

Here are a couple of commands to customize [GDB]'s behavior in this case:

`set ada print-signatures`

Control whether parameter types and return types are displayed in overloads selection menus. It is `on` by default. See [Overloading support for Ada](#Overloading-support-for-Ada).

`show ada print-signatures`

Show the current setting for displaying parameter types and return types in overloads selection menu. See [Overloading support for Ada](#Overloading-support-for-Ada).
