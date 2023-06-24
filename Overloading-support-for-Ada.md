---
tip: translate by openai@2023-06-24 00:57:38
...
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

> 调试器支持有限的过载。给定一个子程序调用，其中函数符号具有多个定义，它将使用实际参数的数量以及有关其类型的一些信息，以尝试缩小定义集合。它还在`call`命令的上下文中优先使用过程，在其他地方优先使用函数。


If, after narrowing, the set of matching definitions still contains more than one definition, [GDB] will display a menu to query which one it should use, for instance:

> 如果经过缩小范围后，匹配的定义仍然包含多个定义，[GDB]将显示一个菜单以查询应使用哪个定义，例如：

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

> 在这种情况下，可以选择一个菜单项来取消表达式评估（输入[0]并按下RET）或继续使用特定实例进行评估（输入相应的数字并按下RET）。

Here are a couple of commands to customize [GDB]'s behavior in this case:

`set ada print-signatures`


Control whether parameter types and return types are displayed in overloads selection menus. It is `on` by default. See [Overloading support for Ada](#Overloading-support-for-Ada).

> 控制是否在重载选择菜单中显示参数类型和返回类型。默认情况下是`开`的。请参阅[Ada的重载支持](#Overloading-support-for-Ada)。

`show ada print-signatures`


Show the current setting for displaying parameter types and return types in overloads selection menu. See [Overloading support for Ada](#Overloading-support-for-Ada).

> 查看重载选择菜单中的参数类型和返回类型的当前设置。请参阅[Ada的重载支持](#Overloading-support-for-Ada)。
