---
description: Trace State Variables (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Trace State Variables (Debugging with GDB)
lang: en
resource-type: document
title: Trace State Variables (Debugging with GDB)
---
::: header
Next: [Tracepoint Actions](Tracepoint-Actions.html#Tracepoint-Actions)]
:::

---

#### 13.1.5 Trace State Variables

A *trace state variable* is a special type of variable that is created and managed by target-side code. The syntax is the same as that for GDB's convenience variables (a string prefixed with "\$"), but they are stored on the target. They must be created explicitly, using a `tvariable` command. They are always 64-bit signed integers.

Trace state variables are remembered by [GDB], and downloaded to the target along with tracepoint information when the trace experiment starts. There are no intrinsic limits on the number of trace state variables, beyond memory limitations of the target.

Although trace state variables are managed by the target, you can use them in print commands and expressions as if they were convenience variables; [GDB] will get the current value from the target while the trace experiment is running. Trace state variables share the same namespace as other "\$" variables, which means that you cannot have trace state variables with names like `$23` or `$pc`, nor can you have a trace state variable and a convenience variable with the same name.

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
