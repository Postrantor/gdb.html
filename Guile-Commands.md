---
description: Guile Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile Commands (Debugging with GDB)
lang: en
resource-type: document
title: Guile Commands (Debugging with GDB)
---
::: header
Next: [Guile API](Guile-API.html#Guile-API)]
:::

---

#### 23.4.2 Guile Commands

[GDB] provides two commands for accessing the Guile interpreter:

`guile-repl`

`gr`

The `guile-repl` command can be used to start an interactive Guile prompt or *repl*. To return to [GDB] on an empty prompt). These commands do not take any arguments.

`guile [scheme-expression]`

`gu [scheme-expression]`

The `guile` command can be used to evaluate a Scheme expression.

If given an argument, [GDB] will pass the argument to the Guile interpreter for evaluation.

::: smallexample

```bash
(gdb) guile (display (+ 20 3)) (newline)
23
```

:::

The result of the Scheme expression is displayed using normal Guile rules.

::: smallexample

```bash
(gdb) guile (+ 20 3)
23
```

:::

If you do not provide an argument to `guile`, it will act as a multi-line command, like `define`. In this case, the Guile script is made up of subsequent command lines, given after the `guile` command. This command list is terminated using a line containing `end`. For example:

::: smallexample

```bash
(gdb) guile
>(display 23)
>(newline)
>end
23
```

:::

It is also possible to execute a Guile script from the [GDB] interpreter:

`source script-name`

:   The script name must end with '`.scm` must be configured to recognize the script language based on filename extension using the `script-extension` setting. See [Extending GDB](Extending-GDB.html#Extending-GDB).

`guile (load "script-name")`

:   This method uses the `load` Guile function. It takes a string argument that is the name of the script to load. See the Guile documentation for a description of this function. (see [Loading](http://www.gnu.org/software/guile/manual/html_node/Loading.html#Loading) in GNU Guile Reference Manual).

---

::: header
Next: [Guile API](Guile-API.html#Guile-API)]
:::
