---
tip: translate by openai@2023-06-23 14:42:11
...
---
description: Trace State Variables (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Trace State Variables (Debugging with GDB)
lang: en
resource-type: document
title: Trace State Variables (Debugging with GDB)
-------------------------------------------------

::: header
Next: [Tracepoint Actions](Tracepoint-Actions.html#Tracepoint-Actions)]
:::

---

#### 13.1.5 Trace State Variables

A *trace state variable* is a special type of variable that is created and managed by target-side code. The syntax is the same as that for GDB's convenience variables (a string prefixed with "\$"), but they are stored on the target. They must be created explicitly, using a `tvariable` command. They are always 64-bit signed integers.

> 一个*跟踪状态变量*是由目标端代码创建和管理的特殊类型变量。语法与 GDB 的便利变量（以"\$"为前缀的字符串）相同，但是它们存储在目标上。它们必须使用 `tvariable` 命令显式创建。它们总是 64 位有符号整数。

Trace state variables are remembered by [GDB], and downloaded to the target along with tracepoint information when the trace experiment starts. There are no intrinsic limits on the number of trace state variables, beyond memory limitations of the target.

> GDB 记住跟踪状态变量，并在跟踪实验开始时将其下载到目标机器上，同时也下载跟踪点信息。除了目标机器的内存限制外，跟踪状态变量的数量没有固定的限制。

Although trace state variables are managed by the target, you can use them in print commands and expressions as if they were convenience variables; [GDB] will get the current value from the target while the trace experiment is running. Trace state variables share the same namespace as other "\$" variables, which means that you cannot have trace state variables with names like `$23` or `$pc`, nor can you have a trace state variable and a convenience variable with the same name.

> 雖然跟蹤狀態變數由目標管理，但您可以像使用方便變數一樣在列印指令和表達式中使用它們；[GDB] 在跟蹤實驗運行時將從目標獲取當前值。跟蹤狀態變數與其他“\$”變數共享相同的命名空間，這意味着您不能有像 `$23` 或 `$pc` 之類的跟蹤狀態變數，也不能有具有相同名稱的跟蹤狀態變數和方便變數。

`tvariable $name [ = expression ]`

:

```
The `tvariable` command creates a new trace state variable named `$name`, and optionally gives it an initial value of `expression` will report an error. A subsequent `tvariable` command specifying the same name does not create a variable, but instead assigns the supplied initial value to the existing variable of that name, overwriting any previous initial value. The default initial value is 0.
```

`info tvariables`

:

```
List all the trace state variables along with their initial values. Their current values may also be displayed, if the trace experiment is currently running.
```

`delete tvariable [ $name … ]`

:

```
Delete the given trace state variables, or all of them if no arguments are specified.
```

---

::: header
Next: [Tracepoint Actions](Tracepoint-Actions.html#Tracepoint-Actions)]
:::
